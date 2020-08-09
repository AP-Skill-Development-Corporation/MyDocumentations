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

ListenerType	    Typical Usage

OnProgressListener	This listener is called periodically as data is transferred and can be used to populate an upload/download indicator.

OnPausedListener	This listener is called any time the task is paused.

OnSuccessListener	This listener is called when the task has successfully completed.

OnFailureListener	This listener is called any time the upload has failed. This can happen due to network timeouts, authorization failures, or if you cancel the task.

OnFailureListener is called with an Exception instance. Other listeners are called with an UploadTask.TaskSnapshot object. This object is an immutable view of the task at the 
time the event occurred. An UploadTask.TaskSnapshot contains the following properties:

getDownloadUrl	Type(String):

A URL that can be used to download the object. This is a public unguessable URL that can be shared with other clients. This value is populated once an upload is complete.

getError	Type(Exception):

If the task failed, this will have the cause as an Exception.

getBytesTransferred	Type(long):

The total number of bytes that have been transferred when this snapshot was taken.

getTotalByteCount	Type(long):

The total number of bytes expected to be uploaded.

getUploadSessionUri	Type(String):

A URI that can be used to continue this task via another call to putFile.

getMetadata	Type(StorageMetadata):

Before an upload completes, this is the metadata being sent to the server. After the upload completes, this is the metadata returned by the server.

getTask	Type(UploadTask):

The task that created this snapshot. Use this task to cancel, pause, or resume the upload.

getStorage	Type(StorageReference):

The StorageReference used to create the UploadTask.

The UploadTask event listeners provide a simple and powerful way to monitor upload events.



```

```
