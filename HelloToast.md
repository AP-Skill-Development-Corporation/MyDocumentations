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

![image9](https://user-images.githubusercontent.com/51777024/95292699-9e0e1280-088f-11eb-96d2-f97c93176a78.png)

# 2.1 Explore the Layout Editor

Use the Layout Editor to create the layout of the user interface elements, and to preview your app using different devices and app themes, resolutions, and orientations.

Refer to the screenshot below to match

1.In the app > res > layout folder, open the activiy_main.xml file (1).

The Android Studio Screen should look similar to the screenshot below. If you see the XML code for the UI layout, click the Design tab below the Component Tree (8).

2.Using the annotated screenshot below as a guideline, explore the Layout Editor.

![image10](https://user-images.githubusercontent.com/51777024/95292714-a49c8a00-088f-11eb-8071-66cc00895dcf.png)

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

Note: If you get an error about a missing App Theme, try File > Invalidate Caches / Restart or choose a theme that does not generate the error. Additional help can be found in this stackoverflow post.

# 2.2 Change the view group to a LinearLayout

The root of the view hierarchy is a view group, which as implied by the name, is a view that contains other views.

A vertical linear layout is one of the most common layouts. It is simple, fast, and always a good starting point. Change the view group to a vertical, LinearLayout as follows:

1.In the Component Tree pane (7 in the previous screenshot), find the top or root view directly below the Device Screen.

2.Click the Text tab (8) to switch to the code view of the layout.

3.In the second line of the code, change the root view group to LinearLayout. The second line of code now looks something like this:

```
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"

```

4.Make sure the closing tag at the end of the code has changed to </LinearLayout>. If it hasn't changed automatically, change it manually.

5.The android:layout_height is defined as part of the template. The default layout orientation a horizontal row. To change the layout to be vertical, add the following code inside LinearLayout, below android:layout_height.

```
android:orientation="vertical"
```
6.From the menu bar, select: Code > Reformat Code…

It may say "No lines changed: code is already properly formatted".

7.Run the code to make sure it still works.

8.Switch back to Design.

9.Verify in the Component Tree pane that the top element is now a LinearLayout with its orientation attribute set to "vertical".

## Solution Code: 

Depending on your version of Android Studio, your code will look something like the following.
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context="hellotoast.android.example.com.hellotoast.MainActivity">


    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Hello World!" />
</LinearLayout>
```
# 2.3 Add views to the Linear Layout in the Layout Editor

In this task you will delete the current TextView (for practice), and add a new TextView and two buttons to the LinearLayout as shown in the UI sketch for this task. Refer to the UI diagram above, if necessary.

## Add UI Elements
1.Click the Design tab (8) to show the virtual device layout.
2.Click the TextView whose text value is "Hello World" in the virtual device layout or the Component Tree pane (7).
3.Press the Delete key to remove that TextView.
4.From the Palette pane (2), drag and drop a Button element, a TextView, and another Button element, in that order, one below the other into the virtual device layout.

## Adjust the UI Elements

To identify each view uniquely within an activity, each view needs a unique ID. And to be of any use, the buttons need labels and the text view needs to show some text. Double-click each element in the Component Tree to see its properties and change the text and ID strings as follows:

Image11

1.Run your app.

## Solution Layout:

There should be three Views on your screen. They won't match the image below, but as long as you have three Views in a vertical layout, you are doing fine!

Image12

## Challenge:
Think of an app you might want and create a project and layout for it using Layout Editor. Explore more of the features of Layout Editor. As mentioned before, the Layout Editor has a rich set of features and coding shortcuts. Check the Android Studio documentation to dive deeper.

# Task 3: Edit the "Hello Toast" layout in XML

In this practical, you will edit the XML code for the Hello Toast app UI layout. You will also edit the properties of the views you have created. You can find the properties common to all views in the View class documentation.

Why: While the Layout Editor is a powerful tool, some changes are easier to make directly in the XML source code. It is a personal preference to use either the graphical LayoutEditor or edit the XML file directly.

1.Open res/layout/activity_main.xml in Text mode.
2.In the menu bar select Code > Reformat Code
3.Examine the code created by the Layout Editor.

Note that your code may not be an exact match, depending on what changes you made in the Layout Editor. Use the sample solutions as guidelines.

3.1 Examine LinearLayout properties
A LinearLayout is required to have these properties:

* layout_width
* layout_height
* orientation

The layout_width and layout_height can take one of three values:

* The match_parent attribute expands the view to fill its parent by width or height. When the LinearLayout is the root view, it expands to the size of the parent view.
* The wrap_content attribute shrinks the view dimensions just big enough to enclose its content. (If there is no content, the view becomes invisible.)
* Use a fixed number of dp (device independent pixels) to specify a fixed size, adjusted for the screen size of the device. For example, "16dp" means 16 device independent pixels.

The orientation can be:

* horizontal: views are arranged from left to right.
* vertical: views are arranged from top to bottom.

Change the LinearLayout of "Hello Toast" as follows:

image15

# 3.2 Create string resources

Instead of hard-coding strings into the XML code, it is a best practice to use string resources, which represent the strings

Why: Having the strings in a separate file makes it easier to manage them, especially if you use these strings more than once. Also, string resources are mandatory for translating and localizing your app as you will create one string resource file for each language.

1.Place the cursor on the word"Toast".
2.Press Alt-Enter (Option-Enter on the Mac).
3.Select Extract string resources.
4.Set the Resource name to button_label_toast and click OK. (If you make a mistake, undo the change with Ctrl-Z.)

This creates a string resource in the values/res/string.xml file, and the string in your code is replaced with a reference to the resource,

```
@string/button_label_toast
```
5.Extract and name the remaining strings from the views as follows

image16

6.In the Project view, navigate to values/strings.xml to find your strings. Now, you can edit all your strings in one place.

## 3.3 Resize

Similar to strings, it is a best practice to extract view dimensions from the main layout XML file into a dimensions resource located in a file.

Why: This makes it easier to manage dimensions, especially if you need to adjust your layout for different device resolutions. It also makes it easy to have consistent sizing, and change the size of multiple objects by changing one property.

Do the following:

1.Look at the dimens.xml resource file. There should be values for the default screen margins defined. For the dimensions of views, it is better not to use hard-coded values, because that prevents views from adjusting to the screen size.
If necessary, change the layout_width of all elements inside the LinearLayout to "match_parent".

2.If you want to use the graphical Layout Editor, click on the Design tab, select each element in the Component Tree pane and change the layout:width property in the Properties pane. If you want to directly edit the XML file, click on the Text tab, change the android:layout_width for the first Button, the TextView, and the last Button.

3.If necessary, change the layout_height of all elements inside the LinearLayout to "wrap_content".

# 3.4 Set colors and backgrounds

Styles and colors are additional properties that can be extracted into resources. All views can have backgrounds that can be colors or images.

Why: Extracting styles and colors makes it easy to use them consistently throughout the app, and straightforward to change across all UI elements.

Experiment with the following changes:

```
```
```
```
```
```
