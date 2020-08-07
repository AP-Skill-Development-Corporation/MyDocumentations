

# Authenticate Using Google Sign-In on Android

You can let your users authenticate with Firebase using their Google Accounts by integrating Google Sign-In into your app.

# Before you begin

1. If you haven't already, add Firebase to your Android project.

2. In your project-level build.gradle file, make sure to include Google's Maven repository in both your buildscript and allprojects sections.

3. Add the dependencies for the Firebase Authentication Android library and Google Play services to your module (app-level) Gradle file (usually app/build.gradle):

```
implementation 'com.google.firebase:firebase-auth:19.3.2'
implementation 'com.google.android.gms:play-services-auth:18.1.0'

```
4. If you haven't yet specified your app's SHA-1 fingerprint, do so from the Settings page of the Firebase console. Refer to Authenticating Your Client for details on how to get your app's SHA-1 fingerprint.

5. Enable Google Sign-In in the Firebase console:

a. In the Firebase console, open the Auth section.

b. On the Sign in method tab, enable the Google sign-in method and click Save.

# Authenticate with Firebase

1. Integrate Google Sign-In into your app by following the steps on the Integrating Google Sign-In into Your Android App page. When you configure the GoogleSignInOptions object, call requestIdToken:

```

// Configure Google Sign In
GoogleSignInOptions gso = new GoogleSignInOptions.Builder(GoogleSignInOptions.DEFAULT_SIGN_IN)
        .requestIdToken(getString(R.string.default_web_client_id))
        .requestEmail()
        .build();
        
```
You must pass your server's client ID to the requestIdToken method. To find the OAuth 2.0 client ID:

a. Open the Credentials page in the GCP Console.

b. The Web application type client ID is your backend server's OAuth 2.0 client ID.

After you integrate Google Sign-In, your sign-in activity has code similar to the following

```
private void signIn() {
    Intent signInIntent = mGoogleSignInClient.getSignInIntent();
    startActivityForResult(signInIntent, RC_SIGN_IN);
}

@Override
public void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    // Result returned from launching the Intent from GoogleSignInApi.getSignInIntent(...);
    if (requestCode == RC_SIGN_IN) {
        Task<GoogleSignInAccount> task = GoogleSignIn.getSignedInAccountFromIntent(data);
        try {
            // Google Sign In was successful, authenticate with Firebase
            GoogleSignInAccount account = task.getResult(ApiException.class);
            Log.d(TAG, "firebaseAuthWithGoogle:" + account.getId());
            firebaseAuthWithGoogle(account.getIdToken());
        } catch (ApiException e) {
            // Google Sign In failed, update UI appropriately
            Log.w(TAG, "Google sign in failed", e);
            // ...
        }
    }
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
4. After a user successfully signs in, get an ID token from the GoogleSignInAccount object, exchange it for a Firebase credential, and authenticate with Firebase using the Firebase credential:

```

private void firebaseAuthWithGoogle(String idToken) {
    AuthCredential credential = GoogleAuthProvider.getCredential(idToken, null);
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
                        Snackbar.make(mBinding.mainLayout, "Authentication Failed.", Snackbar.LENGTH_SHORT).show();
                        updateUI(null);
                    }

                    // ...
                }
            });
}


```
If the call to signInWithCredential succeeds you can use the getCurrentUser method to get the user's account data.

# Next steps

* After a user signs in for the first time, a new user account is created and linked to the credentials—that is, the user name and password, phone number, or auth provider information—the user signed in with. This new account is stored as part of your Firebase project, and can be used to identify a user across every app in your project, regardless of how the user signs in.

* In your apps, you can get the user's basic profile information from the FirebaseUser object. See Manage Users.

* In your Firebase Realtime Database and Cloud Storage Security Rules, you can get the signed-in user's unique user ID from the auth variable, and use it to control what data a user can access.

You can allow users to sign in to your app using multiple authentication providers by linking auth provider credentials to an existing user account.

# To sign out a user, call signOut:

```
FirebaseAuth.getInstance().signOut();

```
