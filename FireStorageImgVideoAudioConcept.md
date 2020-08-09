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

# Upload from data in memory

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

# Upload from a stream

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
# Upload from a local file

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
# Get a download URL

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
# Add File Metadata

You can also include metadata when you upload files. This metadata contains typical file metadata properties such as name, size, and contentType (commonly referred to as MIME type). The putFile() method automatically infers the MIME type from the File extension, but you can override the auto-detected type by specifying contentType in the metadata. If you do not provide a contentType and Cloud Storage cannot infer a default from the file extension, Cloud Storage uses application/octet-stream. See the Use File Metadata section for more information about file metadata.

```

// Create file metadata including the content type
StorageMetadata metadata = new StorageMetadata.Builder()
        .setContentType("image/jpg")
        .build();

// Upload the file and metadata
uploadTask = storageRef.child("images/mountains.jpg").putFile(file, metadata);


```
# Manage Uploads

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
# Monitor Upload Progress

You can add listeners to handle success, failure, progress, or pauses in your upload task:


## ListenerType(OnProgressListener):

This listener is called periodically as data is transferred and can be used to populate an upload/download indicator.

## ListenerType(OnPausedListener):

This listener is called any time the task is paused.

## ListenerType(OnSuccessListener):

This listener is called when the task has successfully completed.

## ListenerType(OnFailureListener):

This listener is called any time the upload has failed. This can happen due to network timeouts, authorization failures, or if you cancel the task.

OnFailureListener is called with an Exception instance. Other listeners are called with an UploadTask.TaskSnapshot object. This object is an immutable view of the task at the 
time the event occurred. An UploadTask.TaskSnapshot contains the following properties:

## getDownloadUrl	Type(String):

A URL that can be used to download the object. This is a public unguessable URL that can be shared with other clients. This value is populated once an upload is complete.

## getError	Type(Exception):

If the task failed, this will have the cause as an Exception.

## getBytesTransferred	Type(long):

The total number of bytes that have been transferred when this snapshot was taken.

## getTotalByteCount	Type(long):

The total number of bytes expected to be uploaded.

## getUploadSessionUri	Type(String):

A URI that can be used to continue this task via another call to putFile.

## getMetadata	Type(StorageMetadata):

Before an upload completes, this is the metadata being sent to the server. After the upload completes, this is the metadata returned by the server.

## getTask	Type(UploadTask):

The task that created this snapshot. Use this task to cancel, pause, or resume the upload.

## getStorage	Type(StorageReference):

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
# Handle Activity Lifecycle Changes

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

# Continuing Uploads Across Process Restarts

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

# Error Handling

There are a number of reasons why errors may occur on upload, including the local file not existing, or the user not having permission to upload the desired file. You can find more information about errors in the Handle Errors section of the docs.

# Full Example

A full example of an upload with progress monitoring and error handling is shown below:

