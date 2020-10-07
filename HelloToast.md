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

# Task 2: Add views to "Hello Toast" in the Layout Editor

In this task, you will create and configure a user interface for the "Hello Toast" app by arranging view UI components on the screen.

Why: Every app should start with the user experience, even if the initial implementation is very basic.

Views used for Hello Toast are:

* TextView - A view that displays text.
* Button - A button with a label that is usually associated with a click handler.
* LinearLayout - A view that acts as a container to arrange other view. This type of view extends the ViewGroup class and is also called a view group. LinearLayout is a basic * view group that arranges its collection of views in a horizontal or vertical row.

Here is a rough sketch of the UI you will build in this exercise. Simple UI sketches can be very useful for deciding which views to use and how to arrange them, especially when your layouts become more sophisticated.


# 2.1 Explore the Layout Editor

Use the Layout Editor to create the layout of the user interface elements, and to preview your app using different devices and app themes, resolutions, and orientations.

Refer to the screenshot below to match

1.In the app > res > layout folder, open the activiy_main.xml file (1).

The Android Studio Screen should look similar to the screenshot below. If you see the XML code for the UI layout, click the Design tab below the Component Tree (8).

2.Using the annotated screenshot below as a guideline, explore the Layout Editor.


3.Find the different ways in which the "Hello World" string's UI element, a TextView, is represented.

* In the Palette of UI elements (2) developers can create a text view by dragging it into the design pane.

* Visually, in the Design pane (6).

* In the Component Tree (7), as a component in a hierarchy of UI elements called the View Hierarchy. That is, views are organized into a tree hierarchy of parents and children, where children inherit properties of their parents.

* In the Properties pane (4), as a list of its properties, where "Hello Toast" is the value of the text property of the TextView (5).

4.Use the selectors above the virtual device (3) to do the following:

* Change the theme for your app.
* Change the rotation to landscape.
* Use a different version of the SDK.
* Preview layout variants such as a right-to-left layout direction.
* Use the tooltips on the icons to help you discover their function.

5.Switch between the Design and Text tabs (8). Some UI changes can only be made in code, and some are quicker to accomplish in the virtual device.

6.When you're done, undo the changes (for UI changes, use Edit > Undo or the keyboard shortcut for the operating system).

See the Android Studio User Guide for the full Android Studio documentation.

```
Note: If you get an error about a missing App Theme, try File > Invalidate Caches / Restart or choose a theme that does not generate the error. Additional help can be found in this stackoverflow post.

```


```

```
```

```
