# Authenticate with Firebase on Android using a Phone Number

You can use Firebase Authentication to sign in a user by sending an SMS message to the user's phone. The user signs in using a one-time code contained in the SMS message.

The easiest way to add phone number sign-in to your app is to use FirebaseUI, which includes a drop-in sign-in widget that implements sign-in flows for phone number sign-in, as well as password-based and federated sign-in. This document describes how to implement a 
phone number sign-in flow using the Firebase SDK.

Phone numbers that end users provide for authentication will be sent and stored by Google to improve our spam and abuse prevention across Google services, 
including but not limited to Firebase. Developers should ensure they have appropriate end-user consent prior to using the Firebase Authentication phone number
sign-in service.

# Before you begin

1. If you haven't already, add Firebase to your Android project.

2. In your project-level build.gradle file, make sure to include Google's Maven repository in both your buildscript and allprojects sections.

3. Add the dependency for the Firebase Authentication Android library to your module (app-level) Gradle file (usually app/build.gradle):

```
implementation 'com.google.firebase:firebase-auth:19.3.2'

```

4. If you haven't yet connected your app to your Firebase project, do so from the Firebase console.

5. If you haven't already set your app's SHA-1 hash in the Firebase console, do so. See Authenticating Your Client for information about finding your app's SHA-1 hash.

Also, note that phone number sign-in requires a physical device and won't work on an emulator.

# Security concerns

Authentication using only a phone number, while convenient, is less secure than the other available methods, because possession of a phone number can be easily transferred between users. Also, on devices with multiple user profiles, any user that can receive SMS messages can sign in to an account using the device's phone number.

If you use phone number based sign-in in your app, you should offer it alongside more secure sign-in methods, and inform users of the security tradeoffs of using phone number sign-in.

# Enable Phone Number sign-in for your Firebase project

To sign in users by SMS, you must first enable the Phone Number sign-in method for your Firebase project:

1. In the Firebase console, open the Authentication section.

2. On the Sign-in Method page, enable the Phone Number sign-in method.

Firebase's phone number sign-in request quota is high enough that most apps won't be affected. However, if you need to sign in a very high volume of users with phone authentication, you might need to upgrade your pricing plan. See the pricing page.

# Send a verification code to the user's phone

To initiate phone number sign-in, present the user an interface that prompts them to type their phone number. Legal requirements vary, but as a best practice and to set expectations for your users, you should inform them that if they use phone sign-in, they might receive an SMS message for verification and standard rates apply.

Then, pass their phone number to the PhoneAuthProvider.verifyPhoneNumber method to request that Firebase verify the user's phone number. For example:

```
PhoneAuthProvider.getInstance().verifyPhoneNumber(
        phoneNumber,        // Phone number to verify
        60,                 // Timeout duration
        TimeUnit.SECONDS,   // Unit of timeout
        this,               // Activity (for callback binding)
        mCallbacks);        // OnVerificationStateChangedCallbacks

```
The verifyPhoneNumber method is reentrant: if you call it multiple times, such as in an activity's onStart method, the verifyPhoneNumber method will not send a second SMS unless the original request has timed out.

You can use this behavior to resume the phone number sign in process if your app closes before the user can sign in (for example, while the user is using their SMS app). After you call verifyPhoneNumber, set a flag that indicates verification is in progress. Then, save the flag in your Activity's onSaveInstanceState method and restore the flag in onRestoreInstanceState. Finally, in your Activity's onStart method, check if verification is already in progress, and if so, call verifyPhoneNumber again. Be sure to clear the flag when verification completes or fails (see Verification callbacks).

To easily handle screen rotation and other instances of Activity restarts, pass your Activity to the verifyPhoneNumber method. The callbacks will be auto-detached when the Activity stops, so you can freely write UI transition code in the callback methods.

The SMS message sent by Firebase can also be localized by specifying the auth language via the setLanguageCode method on your Auth instance.

```
auth.setLanguageCode("fr");
// To apply the default app language instead of explicitly setting it.
// auth.useAppLanguage();

```
When you call PhoneAuthProvider.verifyPhoneNumber, you must also provide an instance of OnVerificationStateChangedCallbacks, which contains implementations of the callback functions that handle the results of the request. For example:

```
mCallbacks = new PhoneAuthProvider.OnVerificationStateChangedCallbacks() {

    @Override
    public void onVerificationCompleted(PhoneAuthCredential credential) {
        // This callback will be invoked in two situations:
        // 1 - Instant verification. In some cases the phone number can be instantly
        //     verified without needing to send or enter a verification code.
        // 2 - Auto-retrieval. On some devices Google Play services can automatically
        //     detect the incoming verification SMS and perform verification without
        //     user action.
        Log.d(TAG, "onVerificationCompleted:" + credential);

        signInWithPhoneAuthCredential(credential);
    }

    @Override
    public void onVerificationFailed(FirebaseException e) {
        // This callback is invoked in an invalid request for verification is made,
        // for instance if the the phone number format is not valid.
        Log.w(TAG, "onVerificationFailed", e);

        if (e instanceof FirebaseAuthInvalidCredentialsException) {
            // Invalid request
            // ...
        } else if (e instanceof FirebaseTooManyRequestsException) {
            // The SMS quota for the project has been exceeded
            // ...
        }

        // Show a message and update the UI
        // ...
    }

    @Override
    public void onCodeSent(@NonNull String verificationId,
                           @NonNull PhoneAuthProvider.ForceResendingToken token) {
        // The SMS verification code has been sent to the provided phone number, we
        // now need to ask the user to enter the code and then construct a credential
        // by combining the code with a verification ID.
        Log.d(TAG, "onCodeSent:" + verificationId);

        // Save verification ID and resending token so we can use them later
        mVerificationId = verificationId;
        mResendToken = token;

        // ...
    }
};

```

# Verification callbacks

In most apps, you implement the onVerificationCompleted, onVerificationFailed, and onCodeSent callbacks. You might also implement onCodeAutoRetrievalTimeOut, depending on your app's requirements.

## onVerificationCompleted(PhoneAuthCredential)

* This method is called in two situations:

* Instant verification: in some cases the phone number can be instantly verified without needing to send or enter a verification code.
Auto-retrieval: on some devices, Google Play services can automatically detect the incoming verification SMS and perform verification without user action. (This capability might be unavailable with some carriers.)

In either case, the user's phone number has been verified successfully, and you can use the PhoneAuthCredential object that's passed to the callback to sign in the user.

## onVerificationFailed(FirebaseException)

This method is called in response to an invalid verification request, such as a request that specifies an invalid phone number or verification code.

## onCodeSent(String verificationId, PhoneAuthProvider.ForceResendingToken)

Optional. This method is called after the verification code has been sent by SMS to the provided phone number.

When this method is called, most apps display a UI that prompts the user to type the verification code from the SMS message. (At the same time, auto-verification might be proceeding in the background.) Then, after the user types the verification code, you can use the verification code and the verification ID that was passed to the method to create a PhoneAuthCredential object, which you can in turn use to sign in the user. However, some apps might wait until onCodeAutoRetrievalTimeOut is called before displaying the verification code UI (not recommended).

## onCodeAutoRetrievalTimeOut(String verificationId)

Optional. This method is called after the timeout duration specified to verifyPhoneNumber has passed without onVerificationCompleted triggering first. On devices without SIM cards, this method is called immediately because SMS auto-retrieval isn't possible.

Some apps block user input until the auto-verification period has timed out, and only then display a UI that prompts the user to type the verification code from the SMS message (not recommended).

This method is called in response to an invalid verification request, such as a request that specifies an invalid phone number or verification code.

onCodeSent(String verificationId, PhoneAuthProvider.ForceResendingToken)
Optional. This method is called after the verification code has been sent by SMS to the provided phone number.

When this method is called, most apps display a UI that prompts the user to type the verification code from the SMS message. (At the same time, auto-verification might be proceeding in the background.) Then, after the user types the verification code, you can use the verification code and the verification ID that was passed to the method to create a PhoneAuthCredential object, which you can in turn use to sign in the user. However, some apps might wait until onCodeAutoRetrievalTimeOut is called before displaying the verification code UI (not recommended).

# onCodeAutoRetrievalTimeOut(String verificationId)

Optional. This method is called after the timeout duration specified to verifyPhoneNumber has passed without onVerificationCompleted triggering first. On devices without SIM cards, this method is called immediately because SMS auto-retrieval isn't possible.

Some apps block user input until the auto-verification period has timed out, and only then display a UI that prompts the user to type the verification code from the SMS message (not recommended).

```
PhoneAuthCredential credential = PhoneAuthProvider.getCredential(verificationId, code);

```

To prevent abuse, Firebase enforces a limit on the number of SMS messages that can be sent to a single phone number within a period of time. If you exceed this limit, phone number verification requests might be throttled. If you encounter this issue during development, use a different phone number for testing, or try the request again later.

# Sign in the user

After you get a PhoneAuthCredential object, whether in the onVerificationCompleted callback or by calling PhoneAuthProvider.getCredential, complete the sign-in flow by passing the PhoneAuthCredential object to FirebaseAuth.signInWithCredential:

```

private void signInWithPhoneAuthCredential(PhoneAuthCredential credential) {
    mAuth.signInWithCredential(credential)
            .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
                @Override
                public void onComplete(@NonNull Task<AuthResult> task) {
                    if (task.isSuccessful()) {
                        // Sign in success, update UI with the signed-in user's information
                        Log.d(TAG, "signInWithCredential:success");

                        FirebaseUser user = task.getResult().getUser();
                        // ...
                    } else {
                        // Sign in failed, display a message and update the UI
                        Log.w(TAG, "signInWithCredential:failure", task.getException());
                        if (task.getException() instanceof FirebaseAuthInvalidCredentialsException) {
                            // The verification code entered was invalid
                        }
                    }
                }
            });
}

```
# Next steps

After a user signs in for the first time, a new user account is created and linked to the credentials—that is, the user name and password, phone number, or auth provider information—the user signed in with. This new account is stored as part of your Firebase project, and can be used to identify a user across every app in your project, regardless of how the user signs in.

* In your apps, you can get the user's basic profile information from the FirebaseUser object. See Manage Users.

* In your Firebase Realtime Database and Cloud Storage Security Rules, you can get the signed-in user's unique user ID from the auth variable, and use it to control what data a user can access.

You can allow users to sign in to your app using multiple authentication providers by linking auth provider credentials to an existing user account.

To sign out a user, call signOut:


```

FirebaseAuth.getInstance().signOut();

```
# Sample Example Application


**Step 1:acivity_main.xml**

```
XML

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".MainActivity">

    <EditText
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:hint="Enter Valid Phone No"
        android:inputType="phone"
        android:id="@+id/phone"/>
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="sendotp"
        android:id="@+id/sendotp"
        />
   <EditText
       android:layout_width="match_parent"
       android:layout_height="wrap_content"
       android:hint="Enter Otp Here"
       android:id="@+id/otp"/>
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="signin"
        android:id="@+id/sendsignin"/>
</LinearLayout>

```

**Step 2:MainAcivity.java**

```
package com.example.gopalotpauth;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.Toast;

import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.android.gms.tasks.TaskExecutors;
import com.google.firebase.FirebaseException;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;
import com.google.firebase.auth.FirebaseAuthInvalidCredentialsException;
import com.google.firebase.auth.PhoneAuthCredential;
import com.google.firebase.auth.PhoneAuthProvider;
import java.util.concurrent.TimeUnit;

public class MainActivity extends AppCompatActivity {

    EditText phone,otp;
    FirebaseAuth auth;
    String vid;
    private PhoneAuthProvider.ForceResendingToken mResendToken;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        auth=FirebaseAuth.getInstance();
        phone=findViewById(R.id.phone);
        otp=findViewById(R.id.otp);

        findViewById(R.id.sendotp).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                sendotpauth();
            }

            private void sendotpauth()
            {
                String ph=phone.getText().toString();
                if (ph.isEmpty())
                {
                    phone.setError("PHONE NO IS REQUIRED");
                    phone.requestFocus();
                    return;
                }
                if (phone.length()<10)
                {
                    phone.setError("ENTER VALID PHONE NUMBER");
                    phone.requestFocus();
                    return;
                }
                PhoneAuthProvider.getInstance().verifyPhoneNumber(ph,60,
                        TimeUnit.SECONDS, TaskExecutors.MAIN_THREAD,mcallback);
            }

            PhoneAuthProvider.OnVerificationStateChangedCallbacks mcallback=new
                    PhoneAuthProvider.OnVerificationStateChangedCallbacks() {

                        @Override
                        public void onCodeSent(String s, PhoneAuthProvider.ForceResendingToken forceResendingToken) {
                            super.onCodeSent(s, forceResendingToken);
                            vid=s;

                        }

                        @Override
                        public void onVerificationCompleted(PhoneAuthCredential phoneAuthCredential) {

                        }

                        @Override
                        public void onVerificationFailed(FirebaseException e) {

                        }
                    };



        });




        findViewById(R.id.sendsignin).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                signinAuth();
            }

            private void signinAuth() {

                String entercode=otp.getText().toString();
                PhoneAuthCredential credential=PhoneAuthProvider.getCredential(vid,entercode);

                signincredential(credential);
            }

            private void signincredential(PhoneAuthCredential credential) {
                auth.signInWithCredential(credential).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
                    @Override
                    public void onComplete(@NonNull Task<AuthResult> task) {

                        if (task.isSuccessful())
                        {
                            Toast.makeText(MainActivity.this, "sucess", Toast.LENGTH_SHORT).show();
                        }
                        else
                        {

                            if (task.getException() instanceof FirebaseAuthInvalidCredentialsException)
                            {
                                Toast.makeText(MainActivity.this, "wrong otp", Toast.LENGTH_SHORT).show();

                            }
                        }
                    }

                });

            }
        });
    }
}



```

