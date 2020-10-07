# Hello Toast

The user interface displayed on the screen of a mobile Android device consists of a hierarchy of "views". Views are Android's basic user interface building blocks. You specify the views in XML layout files. For example, views can be components that:

* display text (TextView class)
* allow you to edit text (EditText class)
* represent clickable buttons (Button class) and other interactive components
* contain scrollable text (ScrollView) and scrollable items (RecyclerView)
* show images (ImageView)
* contain other views and position them (LinearLayout).
* pop up menus and other interactive components.
* You can explore the view hierarchy of your app in the Layout Editor's Component Tree pane.

The Java code that displays and drives the user interface is contained in a class that extends Activity and contains methods to inflate views, that is, take the XML layout of views and display it on the screen. For example, the MainActivity in the Hello World app inflates a text view and prints Hello World. In more complex apps, an activity might implement click and other event handlers, request data from a database or the internet, or draw graphical content.

Android makes it straightforward to clearly separate UI elements and data from each other, and use the activity to bring them back together. This separation is an implementation of an MVP (Model-View-Presenter) pattern.

You will work with Activities and Views throughout this book.

![image8](https://user-images.githubusercontent.com/51777024/95291325-ea0b8800-088c-11eb-9b58-46e8ff7aa196.png)


# What you should already KNOW

For this practical you should be familiar with:

* How to create a Hello World app with Android Studio.

# What you will LEARN

You will learn:

* How to create interactive user interfaces in the Layout Editor, in XML, and programmatically.

* A lot of new terminology. Check out the Vocabulary words and concepts glossary for friendly definitions.

# What you will DO

In this practical, you will:

* Create an app and add user interface elements such as buttons in the Layout Editor.
* Edit the app's layout in XML.
* Add a button to the app. Use a string resource for the label.
* Implement a click handler method for the button to display a message on the screen when the user clicks.

Change the click handler method to change the message shown on the screen.

# App Overview

The "Hello Toast" app will consist of two buttons and one text view. When you click on the first button, it will display a short message, or toast, on the screen. Clicking on the second button will increase a click counter; the total count of mouse clicks will be displayed in the text view.

Here's what the finished app will look like:


# Task 1. Create a new "Hello Toast" project

In this practical, you will design and implement a project for the "Hello Toast" app.


# 1.1. Create the "Hello Toast" project

* Start Android Studio and create a new project with the following parameters:

![image7](https://user-images.githubusercontent.com/51777024/95291335-ed9f0f00-088c-11eb-907f-e405dd41843d.PNG)

* Select Run > Run app or click the Run icon Run Icon in the toolbar to build and execute the app on the emulator or your device.


