

Kotlin Android

Kotlin is a programming language that can run on JVM. Google has announced

Kotlin as one of its officially supported programming languages in Android Studio;

and the Android community is migrating at a pace from Java to Kotlin.

**Prerequisites**

Reader should know Kotlin Programming, have expertise to

use an Android Phone, Windows/Ubuntu/Mac to follow the articles and examples

for Android App Development using Kotlin language.

**Getting Started**

To get started with Android Application Development, we have to setup the

development environment. [Download](https://developer.android.com/studio/index.html)[ ](https://developer.android.com/studio/index.html)[Android](https://developer.android.com/studio/index.html)[ ](https://developer.android.com/studio/index.html)[Studio](https://developer.android.com/studio/index.html)[ ](https://developer.android.com/studio/index.html)for your Operating System

and follow the below topics to create an Android application with Kotlin Support.

If you already know Java and started building Android Applications with it, you

may convert them to Kotlin using Android Studio. Also, we put forth some

differences between Java and Kotlin with development.

● Basic Walk Through Android Studio

● Example Android Application with Kotlin Support

● Convert Java Files to Kotlin Files

● Kotlin vs Java for Android Development

● Using Java8 features for Android Development





**Kotlin Android Application Example – Hello World**

In this [Android](https://www.tutorialkart.com/kotlin-android-tutorial/)[ ](https://www.tutorialkart.com/kotlin-android-tutorial/)[Tutorial](https://www.tutorialkart.com/kotlin-android-tutorial/), we shall learn to use [Kotlin](https://www.tutorialkart.com/kotlin-tutorial/)[ ](https://www.tutorialkart.com/kotlin-tutorial/)language support in Android

Application. with the help an an example Android Project. When we create a

new Android project with Kotlin support, the Activity file shall be created with

Kotlin code.

Following is a screenshot of what we shall achieve by the end of this tutorial.









**Kotlin Android Application Example**

For following this example, we need Android Studio 3.0. At the time of writing this

demo application, we have Android Studio 3.0 Canary 2, which is a kind of

preview version of Android Studio 3.0.

Download the latest preview version from <https://developer.android.com/studio/>.

Once you got the Android Studio 3.x in place, follow the below steps to build our

first Kotlin Android Application.

● **Step 1 : Start Android Studio 3.0.**

●

●

Android Studio Welcome Screen





● **Step 2 : Include Kotlin Support**

● Provide Application Name, Company Domain and check the option

“Include Kotlin Support” and click on “Next”.

●

●

Android Application Name and Location

● **Step 3 : Minimum SDK**

● Select the “Minimum SDK” and to continue, click on “Next”.





●

●

Selection of Application Parameters

● **Step 4 : Select Activity**

● Select “Empty Activity” and click on Next.





●

●

Select Empty Activity

● **Step 5 : Activity Name**

● Remain “Activity Name” as is and click on Finish. We are half-way

there.





●

●

Activity Name

● Android

Studio

starts

building

project

information

for

“KotlinAndroidDemo”. For the first build, it may take some time.





●

●

Building Project Information

● **Step 6 : Install missing platform(s)**

● If Gradle project sync fails when the project is opened for the first

time, click on the link “Install missing platform(s) and sync project” in

“Messages” window the missing components are downloaded and

installed by Android Studio.





●

●

Install missing platform(s)

● Once the installing of platforn(s) is finished, Gradle sync is tried

again, and this time it should be successful.

● The MainActivity in the java folder is a Kotlin file and yaaay, we are

using Kotlin language in our Android Application.

● **Step 7 : Run**

● Run the application by connecting an Android Smart Phone to the

computer in Debugging mode or with the help of emulator.

\------------------------------------------------------------------------------------------------------------------





**Basic walk through Android Studio IDE**

**Android Studio IDE**

The base of Android Studio is IntelliJ IDEA. If you have already worked with

IntelliJ IDEA, then most of the Android Studio would be familiar.

Android Studio provides Menus and ToolBars to run android applications, debug

android applications, modify project structure, manage Android Virtual Devices,

manage SDK, code editor in Text and Design modes etc.

**Android Studio Main Window Overview**

Android Studio Main Window contains

● Menu Bar

● Tool Bar

● Project Window

● Code Editor Window





**Android File Menu**

Some of the useful and regularly used items in File Menu are

● New – Creates new Android Application

● Open – Opens existing Android Application

● Open Recent – Shows the list of recently opened projects and clicking on

one of them would open the project.





**Android XML Design Editor**

In addition to Text Editor, Activity Layout files could be edited using XML Design

Editor. The UI elements could be drag and dropped to the Layout at center. Yo u

can also select the device, API, Application Theme, etc. When you select a UI

element, its properties could be modified in the Attributes window.





**Android Tool Bar – Run, Debug**





There are many useful actions provided in the toolbar. Some of the most

frequently used are :

● dRun

● Debug

● Android Virtual Device Manager

● Android SDK Manager

When you click on the Run button, if there are any android devices connected to

your PC in debug mode, they would appear under ‘Connected Devices’. Virtual

devices that were created through AVD Manager appear under Avaialable Virtual

Devices.





\---------------------------------------------------------------------------------------------------------

**Convert Java Files in Android Application to Kotlin Files**

**or Classes**

Now, we shall see a step by step process of how to convert Java Files in Android

Application to Kotlin Files and Run the Application on an Android Phone.

\1. **Open existing Android Studio project**

\2. Start Android Studio 3.0 and click on “Open an existing Android

Studio project”.





\3.

\4. Open existing Android Studio project





\5.

\6. Browse Existing Android Studio project

\7. In this already existing Android Studio project, we have two activities

namely “MainActivity.java” and “SecondActivity.java”





\8.

\9. Existing Android Studio project with Java files

10.**Convert Java File to Kotlin File**

\11. Open MainActivity.java. Click on “Code” in Menu bar, and then on

“Convert Java File to Kotlin File”. Repeat the process for all the Java

Classes in your Android project that you want to be converted to

Kotlin Classes.





\12.

13.Convert Java Files in Android Application to Kotlin Files or Classes

14.**Configure Kotlin**

15.If you get a message “Kotlin not configured”, Click on “Configure” link

provided in the message. Keep the defaults in the dialogue box

“Configure Kotlin in Project” and click “OK”.

\16.





17.Configure Kotlin

18.If Gradle Sync is required, proceed with the sync.

19.Once the Gradle sync is done, the project should be without any

errors as shown below.

\20.

21.All Java Files converted to Kotlin Files

22.**Run the application.**





\25.

26.Android Application

SecondActivity

\23.

24.Android Application MainActivity





**Kotlin vs Java in Android Application Development**

Following are the differences between [Kotlin](https://www.tutorialkart.com/kotlin-tutorial/)[ ](https://www.tutorialkart.com/kotlin-tutorial/)and [Java](https://www.tutorialkart.com/java-tutorials/)[ ](https://www.tutorialkart.com/java-tutorials/)in Android Application

Development :

Property

Java

Kotlin

Android Application Code

Not Concise

Relatively Concise

You have to

Kotlin [Null](https://www.tutorialkart.com/kotlin/null-safety-in-kotlin/)[ ](https://www.tutorialkart.com/kotlin/null-safety-in-kotlin/)[Safety](https://www.tutorialkart.com/kotlin/null-safety-in-kotlin/)

feature could be

Handle [NullPointerException](https://www.tutorialkart.com/java/handle-java-lang-nullpointerexception/)

explicitly handle





this exception all

the times

used or you may

handle it explicitly.

You may have to

create a new

class that

Kotlin [extension](https://www.tutorialkart.com/kotlin/extension-functions-in-kotlin/)

extends the class

and the new

[functions](https://www.tutorialkart.com/kotlin/extension-functions-in-kotlin/)[ ](https://www.tutorialkart.com/kotlin/extension-functions-in-kotlin/)could be

used to extend the

functionality of a

functionality

Extend a class with new

functionality

should be added

in new class.

New class

class and use the

same class name in

your code without

and mess and fuss.

reference should

be used in your

code. It becomes

messy.





You may create

coroutines.

A background

thread (like

Coroutines perform

high computationally

tasks without

blocking main

thread, but

AsyncTask) has

to be used. And if

multiple such

threads are

Handle high computation

tasks without blocking UI

thread

background tasks

are required,

managing

suspending

execution at a

certain point.

Coroutines being

stackless, have a

lower memory

usage.

multiple threads

may become

difficult.

You may need to

catch and handle

these exceptions.

However, this

Kotlin does not have

checked Exception,

hence no need to

catch an exception.

Code becomes clear

and concise.

Checked Exceptions

may make your

code robust.





Kotlin’s Class

Delegation could be

used as an

Multiple Inheritance

Not supported.

alternative to

multiple inheritance.

Java supports

implicit widening

conversion like

you may assign a

byte value to an

int, an int value to

a double.

Kotlin does not

support implicit

widening

Implicit widening conversion

conversion, Atleast

as of now. You may

need to type cast for

any conversion.

Also, an officially

supported language,

latest addition to the

list.

An officially

supported

language.

Android Studio Support

Getters, Setters,

equals(),

Getters, Setters,

equals(),

[Data](https://www.tutorialkart.com/kotlin/data-class-in-kotlin/)[ ](https://www.tutorialkart.com/kotlin/data-class-in-kotlin/)[Classes](https://www.tutorialkart.com/kotlin/data-class-in-kotlin/)

hashCode() and

toString() are

hashCode() and

toString() have to

implicit. No need to





be explicity

written.

write them

separately.

