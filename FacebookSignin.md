
# Authenticate Using Facebook Login on Android

You can let your users authenticate with Firebase using their Facebook accounts by integrating Facebook Login into your app.

# Before you begin

1. If you haven't already, add Firebase to your Android project.

2. In your project-level build.gradle file, make sure to include Google's Maven repository in both your buildscript and allprojects sections.

3. Add the dependency for the Firebase Authentication Android library to your module (app-level) Gradle file (usually app/build.gradle):

```
implementation 'com.google.firebase:firebase-auth:19.3.2'

```
4. On the Facebook for Developers site, get the App ID and an App Secret for your app.

5. Enable Facebook Login:

a. In the Firebase console, open the Auth section.

b. On the Sign in method tab, enable the Facebook sign-in method and specify the App ID and App Secret you got from Facebook.

c. Then, make sure your OAuth redirect URI (e.g. my-app-12345.firebaseapp.com/__/auth/handler) is listed as one of your OAuth redirect URIs in your Facebook app's settings page on the Facebook for Developers site in the Product Settings > Facebook Login config.

# Authenticate with Firebase

1. Integrate Facebook Login into your app by following the developer's documentation. When you configure the LoginButton or LoginManager object, request the public_profile and email permissions. If you integrated Facebook Login using a LoginButton, your sign-in activity has code similar to the following:

```
// Initialize Facebook Login button
mCallbackManager = CallbackManager.Factory.create();
LoginButton loginButton = mBinding.buttonFacebookLogin;
loginButton.setReadPermissions("email", "public_profile");
loginButton.registerCallback(mCallbackManager, new FacebookCallback<LoginResult>() {
    @Override
    public void onSuccess(LoginResult loginResult) {
        Log.d(TAG, "facebook:onSuccess:" + loginResult);
        handleFacebookAccessToken(loginResult.getAccessToken());
    }

    @Override
    public void onCancel() {
        Log.d(TAG, "facebook:onCancel");
        // ...
    }

    @Override
    public void onError(FacebookException error) {
        Log.d(TAG, "facebook:onError", error);
        // ...
    }
});
// ...
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    // Pass the activity result back to the Facebook SDK
    mCallbackManager.onActivityResult(requestCode, resultCode, data);
}

```
2. In your sign-in activity's onCreate method, get the shared instance of the FirebaseAuth object:

```
private FirebaseAuth mAuth;
// ...
// Initialize Firebase Auth
mAuth = FirebaseAuth.getInstance();

```
3. When initializing your Activity, check to see if the user is currently signed in:

```
@Override
public void onStart() {
    super.onStart();
    // Check if user is signed in (non-null) and update UI accordingly.
    FirebaseUser currentUser = mAuth.getCurrentUser();
    updateUI(currentUser);
}

```
4. After a user successfully signs in, in the LoginButton's onSuccess callback method, get an access token for the signed-in user, exchange it for a 
Firebase credential, and authenticate with Firebase using the Firebase credential:

```
private void handleFacebookAccessToken(AccessToken token) {
    Log.d(TAG, "handleFacebookAccessToken:" + token);

    AuthCredential credential = FacebookAuthProvider.getCredential(token.getToken());
    mAuth.signInWithCredential(credential)
            .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
                @Override
                public void onComplete(@NonNull Task<AuthResult> task) {
                    if (task.isSuccessful()) {
                        // Sign in success, update UI with the signed-in user's information
                        Log.d(TAG, "signInWithCredential:success");
                        FirebaseUser user = mAuth.getCurrentUser();
                        updateUI(user);
                    } else {
                        // If sign in fails, display a message to the user.
                        Log.w(TAG, "signInWithCredential:failure", task.getException());
                        Toast.makeText(FacebookLoginActivity.this, "Authentication failed.",
                                Toast.LENGTH_SHORT).show();
                        updateUI(null);
                    }

                    // ...
                }
            });
}

```
If the call to signInWithCredential succeeds, you can use the getCurrentUser method to get the user's account data.

```

```



