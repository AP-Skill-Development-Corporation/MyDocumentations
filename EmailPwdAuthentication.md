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
# Sample Example Application


**Step 1:acivity_main.xml**

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

  <TextView
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:text="Firebase User Register\nwith email and password"
      android:textSize="30sp"
      android:gravity="center"
      android:textColor="@color/colorPrimary"/>
    <EditText
        android:id="@+id/email"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter User Email Id"
        android:textSize="20sp"
        android:textColorHint="#000"/>
    <EditText
        android:id="@+id/password"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter User Password"
        android:textSize="20sp"
        android:textColorHint="#000"/>
    <Button
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Register"
        android:onClick="registerhere"/>
  <TextView
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:text="Firebase signin with\nuser emailid and password"
      android:textSize="25sp"
      android:textColor="@color/colorPrimary"
      android:gravity="center"/>
  <EditText
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:id="@+id/et1"
      android:hint="Enter Registered User email id"
      android:textColorHint="#000"/>
  <EditText
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:id="@+id/et2"
      android:hint="Enter Your User Password"
      android:textColorHint="#000"/>
  <Button
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:text="Signin"
      android:onClick="signinhere"/>
  <TextView
      android:layout_width="match_parent"
      android:textSize="25sp"
      android:layout_height="wrap_content"
      android:textColor="@color/colorPrimary"
      android:gravity="center"
      android:text="Firebase forgot email Password"/>
  <EditText
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:id="@+id/resetemailid"
      android:hint="Enter Registered Email Id"
      android:textColorHint="#000"
      />
  <Button
      android:layout_width="match_parent"
      android:layout_height="wrap_content"
      android:text="resetpasswordemail"
      android:onClick="reset"/>

</LinearLayout>

```

**Step 2:MainAcivity.java**

```
package com.example.firebaseemailpwdauth;

import androidx.annotation.NonNull;
import androidx.appcompat.app.AppCompatActivity;
import android.app.ProgressDialog;
import android.content.Intent;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;
import android.widget.Toast;
import com.google.android.gms.tasks.OnCompleteListener;
import com.google.android.gms.tasks.Task;
import com.google.firebase.auth.AuthResult;
import com.google.firebase.auth.FirebaseAuth;

public class MainActivity extends AppCompatActivity {

    EditText editemail,editpwd;
    FirebaseAuth auth;
    ProgressDialog dialog;
    EditText editsignin,editpassword;
    EditText remail;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        remail=findViewById(R.id.resetemailid);
        editsignin=findViewById(R.id.et1);
        editpassword=findViewById(R.id.et2);
        dialog=new ProgressDialog(this);
        auth=FirebaseAuth.getInstance();
        editemail=findViewById(R.id.email);
        editpwd=findViewById(R.id.password);
    }

    public void registerhere(View view) {

       String e= editemail.getText().toString();
       String p= editpwd.getText().toString();
        if (e.isEmpty()||p.isEmpty())
        {
            Toast.makeText(this, "please enter the details", Toast.LENGTH_SHORT).show();
        }
        else
        {
            dialog.setTitle("Registrating the user");
            dialog.setMessage("please wait");
            dialog.setProgressStyle(ProgressDialog.STYLE_SPINNER);
            dialog.show();
            auth.createUserWithEmailAndPassword(e,p).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
                @Override
                public void onComplete(@NonNull Task<AuthResult> task) {

                   if (task.isSuccessful())
                    {
                        editemail.setText("");
                        editpwd.setText("");
                        Toast.makeText(MainActivity.this, "Registration Sucess", Toast.LENGTH_SHORT).show();
                    }
                    else
                    {
                        Toast.makeText(MainActivity.this, "Registration Failed", Toast.LENGTH_SHORT).show();
                    }
                    dialog.dismiss();

                }
            });

        }

    }

    public void signinhere(View view)
    {
        String se=editsignin.getText().toString();
        String sp=editpassword.getText().toString();

        dialog.setTitle("Sign In the user");
        dialog.setMessage("please wait");
        dialog.setProgressStyle(ProgressDialog.STYLE_SPINNER);
        dialog.show();
        auth.signInWithEmailAndPassword(se,sp).addOnCompleteListener(new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {

                if (task.isSuccessful())
                {
                    Intent i=new Intent(getApplicationContext(),Profile.class);
                    startActivity(i);
                }
                else {
                    Toast.makeText(MainActivity.this, "invalid creadentials", Toast.LENGTH_SHORT).show();
                }
                dialog.dismiss();

            }
        });

    }

    public void reset(View view)
    {

      String re=  remail.getText().toString();
      dialog.setTitle("Forgot pwd send email");
      dialog.setMessage("please wait");
      dialog.show();
      auth.sendPasswordResetEmail(re).addOnCompleteListener(new OnCompleteListener<Void>() {
          @Override
          public void onComplete(@NonNull Task<Void> task) {

              if (task.isSuccessful())
              {
                  Toast.makeText(MainActivity.this, "reset link send to email id", Toast.LENGTH_SHORT).show();
              }
              else {
                  Toast.makeText(MainActivity.this, "Invalid email id", Toast.LENGTH_SHORT).show();
              }
              dialog.dismiss();
          }
      });
    }
}

```

**Step 3:Sample OutPut**

![WhatsApp Image 2020-08-17 at 16 34 47](https://user-images.githubusercontent.com/51777024/90389810-d7a07980-e0a7-11ea-871f-b432d54e2078.jpeg)










