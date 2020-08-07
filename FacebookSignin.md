
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


```

```

```

```





