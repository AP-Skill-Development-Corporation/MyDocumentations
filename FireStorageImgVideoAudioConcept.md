
# Get Started with Cloud Storage on Android

Cloud Storage for Firebase lets you upload and share user generated content, such as images and video, which allows you to build rich media content into your apps. Your data is stored in a Google Cloud Storage bucket, an exabyte scale object storage solution with high availability and global redundancy. Cloud Storage lets you securely upload these files directly from mobile devices and web browsers, handling spotty networks with ease.

## Prerequisites

If you haven't already, add Firebase to your Android project.

In your project-level build.gradle file, make sure to include Google's Maven repository in both your buildscript and allprojects sections.

## Create a default Storage bucket

1. From the navigation pane of the Firebase console, select Storage, then click Get started.

2. Review the messaging about securing your Storage data using security rules. During development, consider setting up your rules for public access.

3. Select a location for your default Storage bucket.

* This location setting is your project's default Google Cloud Platform (GCP) resource location. Note that this location will be used for GCP services in your project that require a location setting, specifically, your Cloud Firestore database and your App Engine app (which is required if you use Cloud Scheduler).

* If you aren't able to select a location, then your project already has a default GCP resource location. It was set either during project creation or when setting up another service that requires a location setting.

If you're on the Blaze plan, you can create multiple buckets, each with its own location.

### Warning: After you set your project's default GCP resource location, you cannot change it.

4. Click Done.

## Set up public access

Cloud Storage for Firebase provides a declarative rules language that allows you to define how your data should be structured, how it should be indexed, and when your data can be read from and written to. By default, read and write access to Storage is restricted so only authenticated users can read or write data. To get started without setting up Authentication, you can configure your rules for public access.

This does make Storage open to anyone, even people not using your app, so be sure to restrict your Storage again when you set up authentication.

## Add the Cloud Storage for Firebase SDK to your app

Add the dependency for the Cloud Storage for Firebase Android library to your module (app-level) Gradle file (usually app/build.gradle):

```
implementation 'com.google.firebase:firebase-storage:19.1.1'

```
## Set up Cloud Storage

The first step in accessing your storage bucket is to create an instance of FirebaseStorage:

```
FirebaseStorage storage = FirebaseStorage.getInstance();

```

You're ready to start using Cloud Storage!

First, let's learn how to create a Cloud Storage reference.

## Advanced setup

There are a few use cases that require additional setup:

* Using storage buckets in multiple geographic regions

* Using storage buckets in different storage classes

* Using storage buckets with multiple authenticated users in the same app

The first use case is perfect if you have users across the world, and want to store their data near them. For instance, you can create buckets in the US, Europe, and Asia to store data for users in those regions to reduce latency.

he second use case is helpful if you have data with different access patterns. For instance: you can set up a multi-regional or regional bucket that stores pictures or other frequently accessed content, and a nearline or coldline bucket that stores user backups or other infrequently accessed content.

In either of these use cases, you'll want to use multiple storage buckets.

The third use case is useful if you're building an app, like Google Drive, which lets users have multiple logged in accounts (for instance, a personal account and a work account). You can use a custom Firebase App instance to authenticate each additional account.

## Use multiple storage buckets

If you want to use a storage bucket other than the default provided above, or use multiple storage buckets in a single app, you can create an instance of FirebaseStorage that references your custom bucket:

```
// Get a non-default Storage bucket
FirebaseStorage storage = FirebaseStorage.getInstance("gs://my-custom-bucket");

```
## Working with imported buckets

When importing an existing Cloud Storage bucket into Firebase, you'll have to grant Firebase the ability to access these files using the gsutil tool, included in the Google Cloud SDK:

```
gsutil -m acl ch -r -u firebase-storage@system.gserviceaccount.com:O gs://<your-cloud-storage-bucket>

```
This does not affect newly created buckets, as those have the default access control set to allow Firebase. This is a temporary measure, and will be performed automatically in the future.

## Use a custom Firebase App

If you're building a more complicated app using a custom FirebaseApp, you can create an instance of FirebaseStorage initialized with that app:

```
// Get the default bucket from a custom FirebaseApp
FirebaseStorage storage = FirebaseStorage.getInstance(customApp);

// Get a non-default bucket from a custom FirebaseApp
FirebaseStorage customStorage = FirebaseStorage.getInstance(customApp, "gs://my-custom-bucket");

```

# Create a Storage Reference on Android
Your files are stored in a Google Cloud Storage bucket. The files in this bucket are presented in a hierarchical structure, just like the file system on your local hard disk, or the data in the Firebase Realtime Database. By creating a reference to a file, your app gains access to it. These references can then be used to upload or download data, get or update metadata or delete the file. A reference can either point to a specific file or to a higher level node in the hierarchy.

If you've used the Firebase Realtime Database, these paths should seem very familiar to you. However, your file data is stored in Google Cloud Storage, not in the Realtime Database.

## Create a Reference

Create a reference to upload, download, or delete a file, or to get or update its metadata. A reference can be thought of as a pointer to a file in the cloud. References are lightweight, so you can create as many as you need. They are also reusable for multiple operations.

References are created using the FirebaseStorage singleton instance and calling its getReference() method.

```
// Create a storage reference from our app
StorageReference storageRef = storage.getReference();

```

You can create a reference to a location lower in the tree, say 'images/space.jpg' by using the child() method on an existing reference.

```
// Create a child reference
// imagesRef now points to "images"
StorageReference imagesRef = storageRef.child("images");

// Child references can also take paths
// spaceRef now points to "images/space.jpg
// imagesRef still points to "images"
StorageReference spaceRef = storageRef.child("images/space.jpg");

```

## Navigate with References

You can also use the getParent() and getRoot() methods to navigate up in our file hierarchy. getParent() navigates up one level, while getRoot() navigates all the way to the top.

```
// getParent allows us to move our reference to a parent node
// imagesRef now points to 'images'
imagesRef = spaceRef.getParent();

// getRoot allows us to move all the way back to the top of our bucket
// rootRef now points to the root
StorageReference rootRef = spaceRef.getRoot();

```
child(), getParent(), and getRoot() can be chained together multiple times, as each returns a reference. But calling getRoot().getParent() returns null.

```
// References can be chained together multiple times
// earthRef points to 'images/earth.jpg'
StorageReference earthRef = spaceRef.getParent().child("earth.jpg");

// nullRef is null, since the parent of root is null
StorageReference nullRef = spaceRef.getRoot().getParent();

```
## Reference Properties

You can inspect references to better understand the files they point to using the getPath(), getName(), and getBucket() methods. These methods get the file's full path, name and bucket.

```
// Reference's path is: "images/space.jpg"
// This is analogous to a file path on disk
spaceRef.getPath();

// Reference's name is the last segment of the full path: "space.jpg"
// This is analogous to the file name
spaceRef.getName();

// Reference's bucket is the name of the storage bucket that the files are stored in
spaceRef.getBucket();

```
## Limitations on References

Reference paths and names can contain any sequence of valid Unicode characters, but certain restrictions are imposed including:

1. Total length of reference.fullPath must be between 1 and 1024 bytes when UTF-8 encoded.
2. No Carriage Return or Line Feed characters.
3. Avoid using #, [, ], *, or ?, as these do not work well with other tools such as the Firebase Realtime Database or gsutil.

## Full Example

```
// Points to the root reference
storageRef = storage.getReference();

// Points to "images"
imagesRef = storageRef.child("images");

// Points to "images/space.jpg"
// Note that you can use variables to create child values
String fileName = "space.jpg";
spaceRef = imagesRef.child(fileName);

// File path is "images/space.jpg"
String path = spaceRef.getPath();

// File name is "space.jpg"
String name = spaceRef.getName();

// Points to "images"
imagesRef = spaceRef.getParent();

```

# Upload Files on Android

Cloud Storage allows developers to quickly and easily upload files to a Google Cloud Storage bucket provided and managed by Firebase.

### Note: By default, Cloud Storage buckets require Firebase Authentication to upload files. You can change your Firebase Security Rules for Cloud Storage to allow unauthenticated access. Since the default Google App Engine app and Firebase share this bucket, configuring public access may make newly uploaded App Engine files publicly accessible as well. Be sure to restrict access to your Storage bucket again when you set up authentication.

# Upload Files

To upload a file to Cloud Storage, you first create a reference to the full path of the file, including the file name.

```
// Create a storage reference from our app
StorageReference storageRef = storage.getReference();

// Create a reference to "mountains.jpg"
StorageReference mountainsRef = storageRef.child("mountains.jpg");

// Create a reference to 'images/mountains.jpg'
StorageReference mountainImagesRef = storageRef.child("images/mountains.jpg");

// While the file names are the same, the references point to different files
mountainsRef.getName().equals(mountainImagesRef.getName());    // true
mountainsRef.getPath().equals(mountainImagesRef.getPath());    // false

```

Once you've created an appropriate reference, you then call the putBytes(), putFile(), or putStream() method to upload the file to Cloud Storage.

You cannot upload data with a reference to the root of your Google Cloud Storage bucket. Your reference must point to a child URL.

## Upload from data in memory

The putBytes() method is the simplest way to upload a file to Cloud Storage. putBytes() takes a byte[] and returns an UploadTask that you can use to manage and monitor the status of the upload.

```
// Get the data from an ImageView as bytes
imageView.setDrawingCacheEnabled(true);
imageView.buildDrawingCache();
Bitmap bitmap = ((BitmapDrawable) imageView.getDrawable()).getBitmap();
ByteArrayOutputStream baos = new ByteArrayOutputStream();
bitmap.compress(Bitmap.CompressFormat.JPEG, 100, baos);
byte[] data = baos.toByteArray();

UploadTask uploadTask = mountainsRef.putBytes(data);
uploadTask.addOnFailureListener(new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception exception) {
        // Handle unsuccessful uploads
    }
}).addOnSuccessListener(new OnSuccessListener<UploadTask.TaskSnapshot>() {
    @Override
    public void onSuccess(UploadTask.TaskSnapshot taskSnapshot) {
        // taskSnapshot.getMetadata() contains file metadata such as size, content-type, etc.
        // ...
    }
});

```
Because putBytes() accepts a byte[], it requires your app to hold the entire contents of a file in memory at once. Consider using putStream() or putFile() to use less memory.

## Upload from a stream

The putStream() method is the most versatile way to upload a file to Cloud Storage. putStream() takes an InputStream and returns an UploadTask that you can use to manage and monitor the status of the upload.

```
InputStream stream = new FileInputStream(new File("path/to/images/rivers.jpg"));

uploadTask = mountainsRef.putStream(stream);
uploadTask.addOnFailureListener(new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception exception) {
        // Handle unsuccessful uploads
    }
}).addOnSuccessListener(new OnSuccessListener<UploadTask.TaskSnapshot>() {
    @Override
    public void onSuccess(UploadTask.TaskSnapshot taskSnapshot) {
        // taskSnapshot.getMetadata() contains file metadata such as size, content-type, etc.
        // ...
    }
});

```
## Upload from a local file

You can upload local files on the device, such as photos and videos from the camera, with the putFile() method. putFile() takes a File and returns an UploadTask which you can use to manage and monitor the status of the upload.

```
Uri file = Uri.fromFile(new File("path/to/images/rivers.jpg"));
StorageReference riversRef = storageRef.child("images/"+file.getLastPathSegment());
uploadTask = riversRef.putFile(file);

// Register observers to listen for when the download is done or if it fails
uploadTask.addOnFailureListener(new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception exception) {
        // Handle unsuccessful uploads
    }
}).addOnSuccessListener(new OnSuccessListener<UploadTask.TaskSnapshot>() {
    @Override
    public void onSuccess(UploadTask.TaskSnapshot taskSnapshot) {
        // taskSnapshot.getMetadata() contains file metadata such as size, content-type, etc.
        // ...
    }
});

```
## Get a download URL

After uploading a file, you can get a URL to download the file by calling the getDownloadUrl() method on the StorageReference:


```
final StorageReference ref = storageRef.child("images/mountains.jpg");
uploadTask = ref.putFile(file);

Task<Uri> urlTask = uploadTask.continueWithTask(new Continuation<UploadTask.TaskSnapshot, Task<Uri>>() {
    @Override
    public Task<Uri> then(@NonNull Task<UploadTask.TaskSnapshot> task) throws Exception {
        if (!task.isSuccessful()) {
            throw task.getException();
        }

        // Continue with the task to get the download URL
        return ref.getDownloadUrl();
    }
}).addOnCompleteListener(new OnCompleteListener<Uri>() {
    @Override
    public void onComplete(@NonNull Task<Uri> task) {
        if (task.isSuccessful()) {
            Uri downloadUri = task.getResult();
        } else {
            // Handle failures
            // ...
        }
    }
});

```
## Add File Metadata

You can also include metadata when you upload files. This metadata contains typical file metadata properties such as name, size, and contentType (commonly referred to as MIME type). The putFile() method automatically infers the MIME type from the File extension, but you can override the auto-detected type by specifying contentType in the metadata. If you do not provide a contentType and Cloud Storage cannot infer a default from the file extension, Cloud Storage uses application/octet-stream. See the Use File Metadata section for more information about file metadata.

```

// Create file metadata including the content type
StorageMetadata metadata = new StorageMetadata.Builder()
        .setContentType("image/jpg")
        .build();

// Upload the file and metadata
uploadTask = storageRef.child("images/mountains.jpg").putFile(file, metadata);


```
## Manage Uploads

In addition to starting uploads, you can pause, resume, and cancel uploads using the pause(), resume(), and cancel() methods. Pause and resume events raise pause and progress state changes respectively. Canceling an upload causes the upload to fail with an error indicating that the upload was canceled.

```
uploadTask = storageRef.child("images/mountains.jpg").putFile(file);

// Pause the upload
uploadTask.pause();

// Resume the upload
uploadTask.resume();

// Cancel the upload
uploadTask.cancel();

```
## Monitor Upload Progress

You can add listeners to handle success, failure, progress, or pauses in your upload task:


### ListenerType(OnProgressListener):

This listener is called periodically as data is transferred and can be used to populate an upload/download indicator.

### ListenerType(OnPausedListener):

This listener is called any time the task is paused.

### ListenerType(OnSuccessListener):

This listener is called when the task has successfully completed.

### ListenerType(OnFailureListener):

This listener is called any time the upload has failed. This can happen due to network timeouts, authorization failures, or if you cancel the task.

OnFailureListener is called with an Exception instance. Other listeners are called with an UploadTask.TaskSnapshot object. This object is an immutable view of the task at the 
time the event occurred. An UploadTask.TaskSnapshot contains the following properties:

### getDownloadUrl	Type(String):

A URL that can be used to download the object. This is a public unguessable URL that can be shared with other clients. This value is populated once an upload is complete.

### getError	Type(Exception):

If the task failed, this will have the cause as an Exception.

### getBytesTransferred	Type(long):

The total number of bytes that have been transferred when this snapshot was taken.

### getTotalByteCount	Type(long):

The total number of bytes expected to be uploaded.

### getUploadSessionUri	Type(String):

A URI that can be used to continue this task via another call to putFile.

### getMetadata	Type(StorageMetadata):

Before an upload completes, this is the metadata being sent to the server. After the upload completes, this is the metadata returned by the server.

### getTask	Type(UploadTask):

The task that created this snapshot. Use this task to cancel, pause, or resume the upload.

### getStorage	Type(StorageReference):

The StorageReference used to create the UploadTask.

The UploadTask event listeners provide a simple and powerful way to monitor upload events.

```
// Observe state change events such as progress, pause, and resume
uploadTask.addOnProgressListener(new OnProgressListener<UploadTask.TaskSnapshot>() {
    @Override
    public void onProgress(UploadTask.TaskSnapshot taskSnapshot) {
        double progress = (100.0 * taskSnapshot.getBytesTransferred()) / taskSnapshot.getTotalByteCount();
        System.out.println("Upload is " + progress + "% done");
    }
}).addOnPausedListener(new OnPausedListener<UploadTask.TaskSnapshot>() {
    @Override
    public void onPaused(UploadTask.TaskSnapshot taskSnapshot) {
        System.out.println("Upload is paused");
    }
});

```
## Handle Activity Lifecycle Changes

Uploads continue in the background even after activity lifecycle changes (such as presenting a dialog or rotating the screen). Any listeners you had attached will also remain attached. This could cause unexpected results if they get called after the activity is stopped.

You can solve this problem by subscribing your listeners with an activity scope to automatically unregister them when the activity stops. Then, use the getActiveUploadTasks method when the activity restarts to obtain upload tasks that are still running or recently completed.

The example below demonstrates this and also shows how to persist the storage reference path used.

```
@Override
protected void onSaveInstanceState(Bundle outState) {
    super.onSaveInstanceState(outState);

    // If there's an upload in progress, save the reference so you can query it later
    if (mStorageRef != null) {
        outState.putString("reference", mStorageRef.toString());
    }
}

@Override
protected void onRestoreInstanceState(Bundle savedInstanceState) {
    super.onRestoreInstanceState(savedInstanceState);

    // If there was an upload in progress, get its reference and create a new StorageReference
    final String stringRef = savedInstanceState.getString("reference");
    if (stringRef == null) {
        return;
    }
    mStorageRef = FirebaseStorage.getInstance().getReferenceFromUrl(stringRef);

    // Find all UploadTasks under this StorageReference (in this example, there should be one)
    List<UploadTask> tasks = mStorageRef.getActiveUploadTasks();
    if (tasks.size() > 0) {
        // Get the task monitoring the upload
        UploadTask task = tasks.get(0);

        // Add new listeners to the task using an Activity scope
        task.addOnSuccessListener(this, new OnSuccessListener<UploadTask.TaskSnapshot>() {
            @Override
            public void onSuccess(UploadTask.TaskSnapshot state) {
                // Success!
                // ...
            }
        });
    }
}

```
getActiveUploadTasks retrieves all active upload tasks at and below the provided reference, so you may need to handle multiple tasks.

## Continuing Uploads Across Process Restarts

If your process is shut down, any uploads in progress will be interrupted. However, you can continue uploading once the process restarts by resuming the upload session with the server. This can save time and bandwidth by not starting the upload from the start of the file.

To do this, begin uploading via putFile. On the resulting StorageTask, call getUploadSessionUri and save the resulting value in persistent storage (such as SharedPreferences).

```
uploadTask = mStorageRef.putFile(localFile);
uploadTask.addOnProgressListener(new OnProgressListener<UploadTask.TaskSnapshot>() {
    @Override
    public void onProgress(UploadTask.TaskSnapshot taskSnapshot) {
        Uri sessionUri = taskSnapshot.getUploadSessionUri();
        if (sessionUri != null && !mSaved) {
            mSaved = true;
            // A persisted session has begun with the server.
            // Save this to persistent storage in case the process dies.
        }
    }
});

```
After your process restarts with an interrupted upload, call putFile again. But this time also pass the Uri that was saved.

```
//resume the upload task from where it left off when the process died.
//to do this, pass the sessionUri as the last parameter
uploadTask = mStorageRef.putFile(localFile,
        new StorageMetadata.Builder().build(), sessionUri);

```
Sessions last one week. If you attempt to resume a session after it has expired or if it had experienced an error, you will receive a failure callback. It is your responsibility to ensure the file has not changed between uploads.

## Error Handling

There are a number of reasons why errors may occur on upload, including the local file not existing, or the user not having permission to upload the desired file. You can find more information about errors in the Handle Errors section of the docs.

## Full Example

A full example of an upload with progress monitoring and error handling is shown below:

```
// Observe state change events such as progress, pause, and resume
uploadTask.addOnProgressListener(new OnProgressListener<UploadTask.TaskSnapshot>() {
    @Override
    public void onProgress(UploadTask.TaskSnapshot taskSnapshot) {
        double progress = (100.0 * taskSnapshot.getBytesTransferred()) / taskSnapshot.getTotalByteCount();
        System.out.println("Upload is " + progress + "% done");
    }
}).addOnPausedListener(new OnPausedListener<UploadTask.TaskSnapshot>() {
    @Override
    public void onPaused(UploadTask.TaskSnapshot taskSnapshot) {
        System.out.println("Upload is paused");
    }
});

```

# Download Files on Android

Cloud Storage allows developers to quickly and easily download files from a Google Cloud Storage bucket provided and managed by Firebase.

### Note: By default, Cloud Storage buckets require Firebase Authentication to download files. You can change your Firebase Security Rules for Cloud Storage to allow unauthenticated access. Since the default Google App Engine app and Firebase share this bucket, configuring public access may make newly uploaded App Engine files publicly accessible as well. Be sure to restrict access to your Storage bucket again when you set up authentication.

## Create a Reference

To download a file, first create a Cloud Storage reference to the file you want to download.

You can create a reference by appending child paths to the storage root, or you can create a reference from an existing gs:// or https:// URL referencing an object in Cloud Storage.

```
// Create a storage reference from our app
StorageReference storageRef = storage.getReference();

// Create a reference with an initial file path and name
StorageReference pathReference = storageRef.child("images/stars.jpg");

// Create a reference to a file from a Google Cloud Storage URI
StorageReference gsReference = storage.getReferenceFromUrl("gs://bucket/images/stars.jpg");

// Create a reference from an HTTPS URL
// Note that in the URL, characters are URL escaped!
StorageReference httpsReference = storage.getReferenceFromUrl("https://firebasestorage.googleapis.com/b/bucket/o/images%20stars.jpg");

```
# Download Files

Once you have a reference, you can download files from Cloud Storage by calling the getBytes() or getStream(). If you prefer to download the file with another library, you can get a download URL with getDownloadUrl().

## Download in memory

Download the file to a byte[] with the getBytes() method. This is the easiest way to download a file, but it must load the entire contents of your file into memory. If you request a file larger than your app's available memory, your app will crash. To protect against memory issues, getBytes() takes a maximum amount of bytes to download. Set the maximum size to something you know your app can handle, or use another download method.

```
StorageReference islandRef = storageRef.child("images/island.jpg");

final long ONE_MEGABYTE = 1024 * 1024;
islandRef.getBytes(ONE_MEGABYTE).addOnSuccessListener(new OnSuccessListener<byte[]>() {
    @Override
    public void onSuccess(byte[] bytes) {
        // Data for "images/island.jpg" is returns, use this as needed
    }
}).addOnFailureListener(new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception exception) {
        // Handle any errors
    }
});

```
## Download to a local file

The getFile() method downloads a file directly to a local device. Use this if your users want to have access to the file while offline or to share the file in a different app. getFile() returns a DownloadTask which you can use to manage your download and monitor the status of the download.

```
islandRef = storageRef.child("images/island.jpg");

File localFile = File.createTempFile("images", "jpg");

islandRef.getFile(localFile).addOnSuccessListener(new OnSuccessListener<FileDownloadTask.TaskSnapshot>() {
    @Override
    public void onSuccess(FileDownloadTask.TaskSnapshot taskSnapshot) {
        // Local temp file has been created
    }
}).addOnFailureListener(new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception exception) {
        // Handle any errors
    }
});

```
If you want to actively manage your download, see Manage Downloads for more information.

## Download Data via URL

If you already have download infrastructure based around URLs, or just want a URL to share, you can get the download URL for a file by calling the getDownloadUrl() method on a storage reference.

```
storageRef.child("users/me/profile.png").getDownloadUrl().addOnSuccessListener(new OnSuccessListener<Uri>() {
    @Override
    public void onSuccess(Uri uri) {
        // Got the download URL for 'users/me/profile.png'
    }
}).addOnFailureListener(new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception exception) {
        // Handle any errors
    }
});

```
## Downloading Images with FirebaseUI

FirebaseUI provides simple, customizable, and production-ready native mobile bindings to eliminate boilerplate code and promote Google best practices. Using FirebaseUI you can quickly and easily download, cache, and display images from Cloud Storage using our integration with Glide.

First, add FirebaseUI to your app/build.gradle:

```
dependencies {
    // FirebaseUI Storage only
    implementation 'com.firebaseui:firebase-ui-storage:6.2.0'
}

```
Then you can load images directly from Storage into an ImageView:

```
// Reference to an image file in Cloud Storage
StorageReference storageReference = FirebaseStorage.getInstance().getReference();

// ImageView in your Activity
ImageView imageView = findViewById(R.id.imageView);

// Download directly from StorageReference using Glide
// (See MyAppGlideModule for Loader registration)
Glide.with(this /* context */)
        .load(storageReference)
        .into(imageView);
        
```
## Handle Activity Lifecycle Changes

Downloads continue in the background even after activity lifecycle changes (such as presenting a dialog or rotating the screen). Any listeners you had attached will also remain attached. This could cause unexpected results if they get called after the activity is stopped.

You can solve this problem by subscribing your listeners with an activity scope to automatically unregister them when the activity stops. Then, use the getActiveDownloadTasks method when the activity restarts to obtain download tasks that are still running or recently completed.

The example below demonstrates this and also shows how to persist the storage reference path used.


```
@Override
protected void onSaveInstanceState(Bundle outState) {
    super.onSaveInstanceState(outState);

    // If there's a download in progress, save the reference so you can query it later
    if (mStorageRef != null) {
        outState.putString("reference", mStorageRef.toString());
    }
}

@Override
protected void onRestoreInstanceState(Bundle savedInstanceState) {
    super.onRestoreInstanceState(savedInstanceState);

    // If there was a download in progress, get its reference and create a new StorageReference
    final String stringRef = savedInstanceState.getString("reference");
    if (stringRef == null) {
        return;
    }
    mStorageRef = FirebaseStorage.getInstance().getReferenceFromUrl(stringRef);

    // Find all DownloadTasks under this StorageReference (in this example, there should be one)
    List<FileDownloadTask> tasks = mStorageRef.getActiveDownloadTasks();
    if (tasks.size() > 0) {
        // Get the task monitoring the download
        FileDownloadTask task = tasks.get(0);

        // Add new listeners to the task using an Activity scope
        task.addOnSuccessListener(this, new OnSuccessListener<FileDownloadTask.TaskSnapshot>() {
            @Override
            public void onSuccess(FileDownloadTask.TaskSnapshot state) {
                // Success!
                // ...
            }
        });
    }
}

```
## Handle Errors

There are a number of reasons why errors may occur on download, including the file not existing, or the user not having permission to access the desired file. More information on errors can be found in the Handle Errors section of the docs.

## Full Example

A full example of a download with error handling is shown below:

```
storageRef.child("users/me/profile.png").getBytes(Long.MAX_VALUE).addOnSuccessListener(new OnSuccessListener<byte[]>() {
    @Override
    public void onSuccess(byte[] bytes) {
        // Use the bytes to display the image
    }
}).addOnFailureListener(new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception exception) {
        // Handle any errors
    }
});

```
# Delete Files on Android

you can also delete files from Cloud Storage.

### Note: By default, Cloud Storage buckets require Firebase Authentication to delete files. You can change your Firebase Security Rules for Cloud Storage to allow unauthenticated access. Since the default Google App Engine app and Firebase share this bucket, configuring public access may make newly uploaded App Engine files publicly accessible as well. Be sure to restrict access to your Storage bucket again when you set up authentication.

# Delete a File

To delete a file, first create a reference. to that file. Then call the delete() method on that reference.

```
// Create a storage reference from our app
StorageReference storageRef = storage.getReference();

// Create a reference to the file to delete
StorageReference desertRef = storageRef.child("images/desert.jpg");

// Delete the file
desertRef.delete().addOnSuccessListener(new OnSuccessListener<Void>() {
    @Override
    public void onSuccess(Void aVoid) {
        // File deleted successfully
    }
}).addOnFailureListener(new OnFailureListener() {
    @Override
    public void onFailure(@NonNull Exception exception) {
        // Uh-oh, an error occurred!
    }
});

```
### Note: Deleting a file is a permanent action! If you care about restoring deleted files, make sure to back up your files, or enable Object Versioning on your Google Cloud Storage bucket.

# Handle Errors

There are a number of reasons why errors may occur on file deletes, including the file not existing, or the user not having permission to delete the desired file. More information on errors can be found in the Handle Errors section of the docs.

## List Files on Android

Cloud Storage allows you to list the contents of your Storage Bucket. The SDKs return both the items and the prefixes of objects under the current Storage reference.

Projects that use the List API require Firebase Storage Rules Version 2. If you have an existing Firebase Project, please follow the steps in the Security Rules Guide.

### Note: The List API is only allowed for Rules version 2. In Rules version 2, allow read is the shorthand for allow get, list.

List() uses Google Cloud Storage’s List API. In Firebase Storage, we use / as a delimiter, which allows us to emulate file system semantics. To allow for efficient traversal of large, hierarchical Storage Buckets, the List API returns prefixes and items separately. For example, if you upload one file /images/uid/file1,

* root.child('images').listAll() will return /images/uid as a prefix.

* root.child('images/uid').listAll() will return the file as an item.

The Firebase Storage SDK does not return object paths that contain two consecutive /s or end with a /.. For example, if a bucket has the following objects:

* correctPrefix/happyItem

* wrongPrefix//sadItem

* lonelyItem/

List operations on items in this bucket will give the following results:

* The list operation at the root returns the references to correctPrefix, wrongPrefix and lonelyItem as prefixes.

* The list operation at the correctPrefix/ returns the references to correctPrefix/happyItem as items.

* The list operation at the wrongPrefix/ doesn't return any references because wrongPrefix//sadItem contains two consecutive /s.

* The list operation at the lonelyItem/ doesn't return any references because the object lonelyItem/ ends with /.

## List all files

You can use listAll to fetch all results for a directory. This is best used for small directories as all results are buffered in memory. The operation also may not return a consistent snapshot if objects are added or removed during the process.

For a large list, use the paginated list() method as listAll() buffers all results in memory.

The following example demonstrates listAll.

```
StorageReference listRef = storage.getReference().child("files/uid");

listRef.listAll()
        .addOnSuccessListener(new OnSuccessListener<ListResult>() {
            @Override
            public void onSuccess(ListResult listResult) {
                for (StorageReference prefix : listResult.getPrefixes()) {
                    // All the prefixes under listRef.
                    // You may call listAll() recursively on them.
                }

                for (StorageReference item : listResult.getItems()) {
                    // All the items under listRef.
                }
            }
        })
        .addOnFailureListener(new OnFailureListener() {
            @Override
            public void onFailure(@NonNull Exception e) {
                // Uh-oh, an error occurred!
            }
        });
```
## Paginate list results

The list() API places a limit on the number of results it returns. list() provides a consistent pageview and exposes a pageToken that allows control over when to fetch additional results.

The pageToken encodes the path and version of the last item returned in the previous result. In a subsequent request using the pageToken, items that come after the pageToken are shown.

The following example demonstrates paginating a result:

```
public void listAllPaginated(@Nullable String pageToken) {
    FirebaseStorage storage = FirebaseStorage.getInstance();
    StorageReference listRef = storage.getReference().child("files/uid");

    // Fetch the next page of results, using the pageToken if we have one.
    Task<ListResult> listPageTask = pageToken != null
            ? listRef.list(100, pageToken)
            : listRef.list(100);

    listPageTask
            .addOnSuccessListener(new OnSuccessListener<ListResult>() {
                @Override
                public void onSuccess(ListResult listResult) {
                    List<StorageReference> prefixes = listResult.getPrefixes();
                    List<StorageReference> items = listResult.getItems();

                    // Process page of results
                    // ...

                    // Recurse onto next page
                    if (listResult.getPageToken() != null) {
                        listAllPaginated(listResult.getPageToken());
                    }
                }
            }).addOnFailureListener(new OnFailureListener() {
                @Override
                public void onFailure(@NonNull Exception e) {
                    // Uh-oh, an error occurred.
                }
            });
}

```
# Handle errors

list() and listAll() fail if you haven't upgraded the Security Rules to version 2. Upgrade your Security Rules if you see this error:

```
Listing objects in a bucket is disallowed for rules_version = "1".
Please update storage security rules to rules_version = "2" to use list.

```
## Handle Errors on Android

Sometimes things don't go as planned and an error occurs.

When in doubt, check the error returned and see what the error message says. The following code shows a custom error handler implementation that inspects the error code and error message returned by Firebase Storage. Such error handlers can be added to various objects used in the Storage API (for example, UploadTask and FileDownloadTask).

```
class MyFailureListener implements OnFailureListener {
    @Override
    public void onFailure(@NonNull Exception exception) {
        int errorCode = ((StorageException) exception).getErrorCode();
        String errorMessage = exception.getMessage();
        // test the errorCode and errorMessage, and handle accordingly
    }
}

```
If you've checked the error message and have Storage Security Rules that allow your action, but are still struggling to fix the error, visit our Support page and let us know how we can help.

## Handle Error Messages

There are a number of reasons why errors may occur, including the file not existing, the user not having permission to access the desired file, or the user cancelling the file upload.

To properly diagnose the issue and handle the error, here is a full list of all the errors our client will raise, and how they can occur. Error codes in this table are defined in the StorageException class as integer constants.

## ERROR_UNKNOWN	An unknown error occurred.

## ERROR_OBJECT_NOT_FOUND	No object exists at the desired reference.

## ERROR_BUCKET_NOT_FOUND	No bucket is configured for Cloud Storage

## ERROR_PROJECT_NOT_FOUND	No project is configured for Cloud Storage

## ERROR_QUOTA_EXCEEDED	Quota on your Cloud Storage bucket has been exceeded. If you're on the free tier, upgrade to a paid plan. If you're on a paid plan, reach out to Firebase support.

## ERROR_NOT_AUTHENTICATED	User is unauthenticated, please authenticate and try again.

## ERROR_NOT_AUTHORIZED	User is not authorized to perform the desired action, check your rules to ensure they are correct.

## ERROR_RETRY_LIMIT_EXCEEDED	The maximum time limit on an operation (upload, download, delete, etc.) has been excceded. Try again.

## ERROR_INVALID_CHECKSUM	File on the client does not match the checksum of the file received by the server. Try uploading again.

## ERROR_CANCELED	User canceled the operation.

Additionally, attempting to call getReferenceFromUrl() with an invalid URL will result in an IllegalArgumentException from being thrown. The argument to the above method must be of the form gs://bucket/object or https://firebasestorage.googleapis.com/v0/b/bucket/o/object?token=<TOKEN>
