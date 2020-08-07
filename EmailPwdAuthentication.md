# Authenticate with Firebase using Password-Based Accounts on Android

You can use Firebase Authentication to let your users authenticate with Firebase using their email addresses and passwords, and to manage your app's password-based accounts.

# Before you begin

1. If you haven't already, add Firebase to your Android project.

2. In your project-level build.gradle file, make sure to include Google's Maven repository in both your buildscript and allprojects sections.

3. Add the dependency for the Firebase Authentication Android library to your module (app-level) Gradle file (usually app/build.gradle):

```
implementation 'com.google.firebase:firebase-auth:19.3.2'

```
4. If you haven't yet connected your app to your Firebase project, do so from the Firebase console.

5. Enable Email/Password sign-in:

1. In the Firebase console, open the Auth section.

2. On the Sign in method tab, enable the Email/password sign-in method and click Save.

# Create a password-based account

To create a new user account with a password, complete the following steps in your app's sign-in activity:

1. In your sign-up activity's onCreate method, get the shared instance of the FirebaseAuth object:

```
private FirebaseAuth mAuth;
// ...
// Initialize Firebase Auth
mAuth = FirebaseAuth.getInstance();

```
2. When initializing your Activity, check to see if the user is currently signed in:

```
@Override
public void onStart() {
    super.onStart();
    // Check if user is signed in (non-null) and update UI accordingly.
    FirebaseUser currentUser = mAuth.getCurrentUser();
    updateUI(currentUser);
}

```
3. When a new user signs up using your app's sign-up form, complete any new account validation steps that your app requires, such as verifying that the new account's password was correctly typed and meets your complexity requirements.

4. Create a new account by passing the new user's email address and password to createUserWithEmailAndPassword:

```
mAuth.createUserWithEmailAndPassword(email, password)
        .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {
                if (task.isSuccessful()) {
                    // Sign in success, update UI with the signed-in user's information
                    Log.d(TAG, "createUserWithEmail:success");
                    FirebaseUser user = mAuth.getCurrentUser();
                    updateUI(user);
                } else {
                    // If sign in fails, display a message to the user.
                    Log.w(TAG, "createUserWithEmail:failure", task.getException());
                    Toast.makeText(EmailPasswordActivity.this, "Authentication failed.",
                            Toast.LENGTH_SHORT).show();
                    updateUI(null);
                }

                // ...
            }
        });

```

If the new account was created, the user is also signed in. In the callback, you can use the getCurrentUser method to get the user's account data.

To protect your project from abuse, Firebase limits the number of new email/password and anonymous sign-ups that your application can have from the same IP address in a short period of time. You can request and schedule temporary changes to this quota from the Firebase console.

# Sign in a user with an email address and password

The steps for signing in a user with a password are similar to the steps for creating a new account. In your app's sign-in activity, do the following:

1. In your sign-in activity's onCreate method, get the shared instance of the FirebaseAuth object:

```
private FirebaseAuth mAuth;
// ...
// Initialize Firebase Auth
mAuth = FirebaseAuth.getInstance();

```
2. When initializing your Activity, check to see if the user is currently signed in:

```
@Override
public void onStart() {
    super.onStart();
    // Check if user is signed in (non-null) and update UI accordingly.
    FirebaseUser currentUser = mAuth.getCurrentUser();
    updateUI(currentUser);
}

```
3. When a user signs in to your app, pass the user's email address and password to signInWithEmailAndPassword:

```
mAuth.signInWithEmailAndPassword(email, password)
        .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {
                if (task.isSuccessful()) {
                    // Sign in success, update UI with the signed-in user's information
                    Log.d(TAG, "signInWithEmail:success");
                    FirebaseUser user = mAuth.getCurrentUser();
                    updateUI(user);
                } else {
                    // If sign in fails, display a message to the user.
                    Log.w(TAG, "signInWithEmail:failure", task.getException());
                    Toast.makeText(EmailPasswordActivity.this, "Authentication failed.",
                            Toast.LENGTH_SHORT).show();
                    updateUI(null);
                    // ...
                }

                // ...
            }
        });

```

If sign-in succeeded, you can use the returned FirebaseUser to proceed.

# Next steps

After a user signs in for the first time, a new user account is created and linked to the credentials—that is, the user name and password, phone number, or auth provider information—the user signed in with. This new account is stored as part of your Firebase project, and can be used to identify a user across every app in your project, regardless of how the user signs in.

* In your apps, you can get the user's basic profile information from the FirebaseUser object. See Manage Users.

* In your Firebase Realtime Database and Cloud Storage Security Rules, you can get the signed-in user's unique user ID from the auth variable, and use it to control what data a user can access.

You can allow users to sign in to your app using multiple authentication providers by linking auth provider credentials to an existing user account.

To sign out a user, call signOut:

```
FirebaseAuth.getInstance().signOut();

```









