
# Firebase

Firebase is a Backend-as-a-Service, and it is a real-time database which is basically designed for mobile applications. This tutorial is designed in such a way that we can easily understand or can perform the service of Firebase in a very efficient way.

![firebase](https://user-images.githubusercontent.com/51777024/89666430-f9f00580-d8f7-11ea-813d-9041762d6a63.png)

# Features of Firebase

Firebase has several features that make this platform essential. These features include unlimited reporting, cloud messaging, authentication and hosting, etc. Let's take a look at these features to understand how these features make Firebase essential:

![fib](https://user-images.githubusercontent.com/51777024/89666776-974b3980-d8f8-11ea-8a11-de6713402119.png)

# Incredibly Built-In Analytics

The analytics dashboard is one of the best features of Firebase, which is equipped with. It is free and can report 500 event types, each with 25 attributes. The dashboard is top-notch for observing user behavior and measuring various user characteristics. Ultimately it helps us to understand how people use our app so that we can better optimize it in the future.

# Key features

## Unlimited Reporting

It allows for reporting of 500 distinct events.

## Audience Segmentation

We can identify custom audiences in the Firebase console based on device data, custom events, or user properties. After that, we can use these audiences that we specified with other Firebase attributes when targeting new features or notifications.

## Integration with Other Services

We can integrate Firebase with other services that can utilize our business apps such as Big Query, Firebase Notifications, Firebase Remote Configuration, Firebase CrashReporting, and Google Tag Manager.

# App Development Made Easy

With Firebase, we can focus our time and attention on developing the best possible applications for our business. The operation and internal functions are very solid. They have taken care of the Firebase Interface. We can spend more time in developing high-quality apps that users want to use.

There are the following features which we can develop:

## Cloud Messaging

Firebase allows us to deliver and receive messages in a more reliable way across platforms.

## Authentication

Firebase has little friction with acclaimed authentication.

## Test Lab

Test in the lab instead on your users.

## Hosting

Firebase delivers web content faster.

## Remote Configuration

It allows us to customize our app on the go.

## Dynamic Links

Dynamic Links are smart URLs which dynamically change behavior for providing the best experience across different platforms. These links allow app users to take directly to the content of their interest after installing the app - no matter whether they are completely new or lifetime customers.

## Crash Reporting

It keeps our app stable.

## Real-time Database

It can store and sync app data in real-time.

## Storage

We can easily store the file in the database.

# Growth and User Engagement

One of the most important aspects of application development is being able to develop and engage with users over time. Firebase has a lot of built-in features, which ensures that it is exactly what we do. With the platform leading to commercial apps, it is really at the center of what makes Firebase so great.

Here are some user interaction aspects which make development a piece of cake:

## AdWords

Linking AdWords is very easy, and with it, we can segment and define our user base using Firebase Analytics. Also, it is easy to improve our targeting in marketing advertising campaigns. Some other benefits include conversion tracking, cross-network, attribution networks, and LTV (Calculating Customer Lifetime Value).

## App Indexing

With app indexing, we can work on aspects like re-engaging with our app, especially by surfing the in-app content within Google search results. It will also help in ranking our application in Google search results.

## Invites

It is a perfect tool for referrals and sharing. Get the help of our users to develop our app easily via email or SMS, allowing their existing users to share our app or in-app content. If we use this feature in combination with promotions, then we can also work towards acquiring new customers and retaining our existing customers.

## Notifications

We can manage information campaigns very easily, including the ability to set and schedule messages to engage users at the right time of day. These notifications are completely free. These are unlimited for both iOS and Android. There is only one dashboard to worry about, and if we integrate with Firebase Analytics, we can use various user segmentation features.

# Increase Your Earnings

Of course, the thing about having an app or any other business strategy is that we can increase our earnings. With the feature of AdMob, we can monetize our app, considering the best possible experience for our users. Showing real-time ads to millions of Google advertisers, choosing a format which suits our app, and working with over 40 top ads networks using AdMob Mediation, we can make app development well worth it, while speaking silently.

We can also cross-promote between our apps with AdMob House ads for free!

# Connect an Android app to FireBase

how to connect an Android app to Firebase

## Step 1

Open Firebase Console and click on Add Project.

![pic1](https://user-images.githubusercontent.com/51777024/89710452-d208ac80-d9a0-11ea-9bde-e13d87f365b7.png)


## Step 2

Enter your project name, check the user agreement and click on Continue.

![pic2](https://user-images.githubusercontent.com/51777024/89710453-d5039d00-d9a0-11ea-86bd-1be487f87851.png)


## Step 3

Make sure the option Enable Google Analytics for this project is enabled. Click Continue.

![pic3](https://user-images.githubusercontent.com/51777024/89710455-d92fba80-d9a0-11ea-976f-aba4a9407207.png)


## Step 4

On the Configure Google Analytics screen, select Default Account for Firebase from the dropdown and click Create project.

![pic4](https://user-images.githubusercontent.com/51777024/89710457-dc2aab00-d9a0-11ea-8c7e-823c2782d2e6.png)


## Step 5

Now, click on the Android icon to proceed with adding your Android app to this Firebase project.

![pic5](https://user-images.githubusercontent.com/51777024/89710458-df259b80-d9a0-11ea-8952-5b9846f96d25.png)

## Step 6

Enter the package name of your app and click on Register app.

![pic6](https://user-images.githubusercontent.com/51777024/89710459-e187f580-d9a0-11ea-9cc4-1a59b9086012.png)


## Step 7

Click on the Download google-services.json button and once the JSON file gets downloaded, place it inside the app folder of your Android project.

![pic7](https://user-images.githubusercontent.com/51777024/89710463-e3ea4f80-d9a0-11ea-95f9-c9f1de528bf5.png)


## Step 8

Click on next and it will show you the dependencies that you need to add to your Android project.

![pic8](https://user-images.githubusercontent.com/51777024/89710467-e6e54000-d9a0-11ea-89c0-134511145afc.png)


Copy the dependency marked with number 1 to your project level build.gradle file and copy the dependencies marked with number 2 and 3 to your app level build.gradle file as shown in the screenshots below.

![pic9](https://user-images.githubusercontent.com/51777024/89710468-e9479a00-d9a0-11ea-8996-98b7165120c4.png)

Finally, click on Sync Now in the bar that appears in Android Studio.

We will be using FirebaseUI Auth module for integrating Email and Google authentication in our Android app.

Add the following dependency to your app-level build.gradle file to use FirebaseUI Auth.

```
implementation 'com.firebaseui:firebase-ui-auth:6.2.1'

```
## Email Authentication

Go to Firebase Console, select your project and click on Authentication tab. Click on Sign-in method, select Email/Password and enable it.

![save](https://user-images.githubusercontent.com/51777024/89710692-e8176c80-d9a2-11ea-8644-2f9f426d0cc4.png)

Now add the following permission to your manifest file.

```
<uses-permission android:name="android.permission.INTERNET"/>

```

## Check Current Auth State

Declare an instance of FirebaseAuth

```
private FirebaseAuth mAuth;

```

## In the onCreate() method, initialize the FirebaseAuth instance.

```
// Initialize Firebase Auth
mAuth = FirebaseAuth.getInstance();

```

## Sign up new Users

Create a new createAccount method which takes in an email address and password, validates them and then creates a new user with the createUserWithEmailAndPassword method.

```
mAuth.createUserWithEmailAndPassword(email, password)
        .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {
                if (task.isSuccessful()) {
                    Toast Here
                } else {
                    Toast Here
                }

                // ...
            }
        });

```
Add a form to register new users with their email and password and call this new method when it is submitted. You can see an example in our quickstart sample .

## Sign In Existing Users

Create a new signIn method which takes in an email address and password, validates them, and then signs a user in with the signInWithEmailAndPassword method.

```

mAuth.signInWithEmailAndPassword(email, password)
        .addOnCompleteListener(this, new OnCompleteListener<AuthResult>() {
            @Override
            public void onComplete(@NonNull Task<AuthResult> task) {
                if (task.isSuccessful()) {
                    //Toast here
                } else {
                   //Toast here
                }

                // ...
            }
        });

```






