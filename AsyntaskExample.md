# AsyncTaskDocumentation

# Introduction:

A thread is an independent path of execution in a running program. When an Android program is launched, the Android Runtime system creates a thread called the "Main" thread. As your program runs, each line of code is executed in a serial fashion, line by line. This main thread is how your application interacts with components from the Android UI Toolkit, and it's why the main thread is sometimes called the "UI thread". However, sometimes an application needs to perform resource-intensive work, such as downloading files, database queries, playing media, or computing complex analytics. This type of intensive work can block the UI thread if all of the code executes serially on a single thread. When the app is performing resources intensive work, the app does not respond to the user or draw on the screen because it is waiting for that work to be done. This can yield poor performance, which negatively affects the user experience. Users may get frustrated and uninstall your Android app if the performance of the app is slow.
To keep the user experience (UX) running smoothly and responding quickly to user gestures, the Android Framework provides a helper class called AsyncTask which processes work off of the UI thread. An AsyncTask is an abstract Java class that provides one way to move this intensive processing onto a separate thread, thereby allowing the UI thread to remain very responsive. Since the separate thread is not synchronized with the calling thread, it is called an asynchronous thread. An AsyncTask also contains a callback that allows you to display the results of the computation back in the UI thread.
In this practical, you will learn how to add a background task to your Android app using an AsyncTask.

# Async-task for Android
This library does the same thing AsyncTask does – runs code on background thread and gets result back to the main thread. But it is simpler, cleaner, easier to understand, straightforward to use, reqires no arcane knowledge to be used. And it requires less boilerplate code than RxJava.
 
# Methods of AsyncTask

## onPreExecute() − Before doing background operation we should show something on screen like progressbar or any animation to user. we can directly comminicate background operation using on doInBackground() but for the best practice, we should call all asyncTask methods .

## doInBackground(Params) − In this method we have to do background operation on background thread. Operations in this method should not touch on any mainthread activities or fragments.

## onProgressUpdate(Progress…) − While doing background operation, if you want to update some information on UI, we can use this method.

## onPostExecute(Result) − In this method we can update ui of background operation result.

Generic Types in Async Task

## TypeOfVarArgParams − It contains information about what type of params used for execution.

## ProgressValue − It contains information about progress units. While doing background operation we can update information on ui using onProgressUpdate().

## ResultValue −It contains information about result type.


