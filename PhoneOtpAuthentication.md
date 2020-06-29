# Firebase Mobile Otp Authentication

# Firebase

* Firebase is a Backend-as-a-Service, and it is a real-time database which is basically designed for mobile applications.
* Google Firebase is a Google-backed application development software that enables developers to develop iOS,Android and Web apps. 
* Firebase provides tools for tracking analytics,reporting and fixing app crashes,creating marketing and product experiment.

![firebase](https://user-images.githubusercontent.com/51777024/85911219-814e5180-b841-11ea-8071-273f9b78c4f9.png)

# Features of Firebase
Firebase has several features that make this platform essential. These features include unlimited reporting, cloud messaging,
authentication and hosting, etc. Let's take a look at these features to understand how these features make Firebase essential.

![Bg4r7dI1Q2W3bX9Sf4oD_unnamed](https://user-images.githubusercontent.com/51777024/85911120-9d9dbe80-b840-11ea-873f-f30665d098ff.png)

# Firebase Authentication

* Authentication is the process of recognizing a user’s identity. 
* It is the mechanism of associating an incoming request with a set of identifying credentials. 
* The credentials are maintained authentication server.
* Mobile authentication is the verification of a user's identity through the use a mobile device and one or more authentication 
  methods for secure access.

![firebase-authentication](https://user-images.githubusercontent.com/51777024/85911439-d9398800-b842-11ea-99ef-9c5631ddb172.png)

# Types of Authentications

You can authenticate your app’s users through the following methods:

* Email & Password
* Phone numbers
* Google
* Facebook
* Twitter

![pasted image 0](https://user-images.githubusercontent.com/51777024/85911863-93ca8a00-b845-11ea-87ae-cd5ef11a840d.png)

# Sample Mobile Otp Authentication

![example](https://user-images.githubusercontent.com/51777024/85912071-35061000-b847-11ea-86fb-3a27ac3c92a6.jpg)

# Steps to Implementation Of Application

We create a new project by clicking on Start a new Android Studio project from Welcome to Android Studio dialog box.

![imag1](https://user-images.githubusercontent.com/51777024/85912182-400d7000-b848-11ea-81ec-e523965e1fae.jpg)

![image2](https://user-images.githubusercontent.com/51777024/85912231-9084cd80-b848-11ea-9595-56625b09fc58.png)

![image3](https://user-images.githubusercontent.com/51777024/85912239-a5616100-b848-11ea-8a43-03d311d44df3.png)

# Firebase Assistance

We can simply add Firebase using Firebase Assistance by selecting Firebase from the tools menu in Android Studio
When we click on Firebase, a new window will open that contains several Firebase features such as Analytics, Cloud
Messaging, Authentication,and Real-time Database, etc.

![f1](https://user-images.githubusercontent.com/51777024/85912347-78617e00-b849-11ea-949d-ecba0a0b447b.png)

Let's start with basics, i.e., Analytics. When we select Analytics, it gives us the step by step guide of what we need to do.

![f2](https://user-images.githubusercontent.com/51777024/85912353-7f888c00-b849-11ea-99e4-9bc3e1ca528a.png)

# Step 1:


So, in the first step, we will connect to Firebase. When we click on connect to Firebase, it may bring up our browser, and wemay have to log into our Google account.If we log in to our Google account, 
we may have to give access to Android Studio so that it can allow us to add stuff.

![f3](https://user-images.githubusercontent.com/51777024/85912357-86af9a00-b849-11ea-8712-b9f4bf0fe118.png)

When we click on allow, it will take us back to Android Studio. Because our project is already connected with Firebase, it will pop up a message, i.e., Firebase already connected. But if our project is not connected with Firebase, it will show the following window.

![f4](https://user-images.githubusercontent.com/51777024/85912364-8c0ce480-b849-11ea-8d3b-8c6263261c96.png)

Here, we have to create a new Firebase project or choosing the existing Firebase project. It completely depends on us. When we click on Connect to Firebase, our project will connect with Firebase successfully.

![f5](https://user-images.githubusercontent.com/51777024/85912367-8fa06b80-b849-11ea-8bd4-844f90d5aa53.png)

# Step 2:

In the next step, we will add analytics to our app by clicking on Add Analytics to your app. This will actually update our build.gradle files, which we did in the previous section.

![f6](https://user-images.githubusercontent.com/51777024/85912370-9202c580-b849-11ea-9d4c-050d9743335f.png)

When we click on Accept Changes, it will update our Gradle files, which we can verify by going to build. Gradle files.

![f7](https://user-images.githubusercontent.com/51777024/85912372-962ee300-b849-11ea-9077-e3a46ba7a437.png)

![f8](https://user-images.githubusercontent.com/51777024/85912373-9929d380-b849-11ea-848c-912f425b58c0.png)

# Step 3:

To sign in users by SMS, you must first enable the Phone Number sign-in method for your Firebase project:
* In the Firebase console, open the Authentication section.
* On the Sign-in Method page, enable the Phone Number sign-in method.

# Step 4: activity_main.xml file

```
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
# Step 5:create the methods and get the id edittext 

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
    
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
       
        phone=findViewById(R.id.phone);
        otp=findViewById(R.id.otp);

        findViewById(R.id.sendotp).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

              
            }

          
        findViewById(R.id.sendsignin).setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

               
            }
    }
}


```

# Step 6 :get the firebase instance at oncreate()

```
private FirebaseAuth mAuth;
// Initialize Firebase Auth
mAuth = FirebaseAuth.getInstance();

```
# Step 7: Send a Verification Code to the Users Phone

```
pass their phone number to the PhoneAuthProvider.verifyPhoneNumber method to request that Firebase verify the user's phone number.

PhoneAuthProvider.getInstance().verifyPhoneNumber(
        phoneNumber,        // Phone number to verify
        60,                 // Timeout duration
        TimeUnit.SECONDS,   // Unit of timeout
        this,               // Activity (for callback binding)
        mCallbacks);        // OnVerificationStateChangedCallbacks
```
# Step 8: implementation on callback functions

```
mCallbacks = new PhoneAuthProvider.OnVerificationStateChangedCallbacks() {@Override
    public void onVerificationCompleted(PhoneAuthCredential credential) 
   {      
Log.d(TAG, "onVerificationCompleted:" + credential);
 signInWithPhoneAuthCredential(credential);
    }
@Override
    public void onVerificationFailed(FirebaseException e) 
  {
          
    }

```
# Step 9 :implementation on callback functions

```
 @Override
    public void onCodeSent(@NonNull String verificationId,
                           @NonNull PhoneAuthProvider.ForceResendingToken token) {
            Log.d(TAG, "onCodeSent:" + verificationId);
        // Save verification ID and resending token so we can use them later
        mVerificationId = verificationId;
        mResendToken = token
        // ...
    }
};

```
# Step 10:Create the PhoneAuthCredential Object

```
To create the PhoneAuthCredential object, call PhoneAuthProvider.getCredential
PhoneAuthCredential credential = PhoneAuthProvider.getCredential(verificationId, code);

```

# Step 11: Signin with User

```
private void signInWithPhoneAuthCredential(PhoneAuthCredential credential) 
{
    mAuth.signInWithCredential(credential).addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
           @Override
           public void onComplete(@NonNull Task<AuthResult> task){
           if (task.isSuccessful()) 
          {
           //navigate new activity                                    
          } else 
          {
              //failed      
          }
          }
          }
            });}
            
```
# Step 12: MainActivity.java file

```
package com.example.gopalotpauth;
import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.os.Bundle;
import android.view.View;
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

# Download Code 

https://github.com/AP-Skill-Development-Corporation/AdvancedAndroid/tree/master/GopalOtpAuth



