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





```

```




```

```





```

```
