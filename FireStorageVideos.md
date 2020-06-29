
# FireStorage Video Upload And Retrive In TabNavigation

# TabLayout Example using ViewPager and Fragments in Android''

If you are using the latest android application then you have noticed that now days android is following a design pattern. This is material design and it came with Android Lollipop (5.0). Though we can still use this design pattern for the older versions (>4.0) by using the support libraries. One of the component of material design is TabLayout. So in this TablLayout Example we will see how we can implement it in our android application.

# What is TabLayout ?

Android TabLayout provides horizontal layout to display tabs. We can display more screens in a single screen using tabs. User can swipe the tabs quickly as you can see in the image below.

![Screenshot_20200627_135527](https://user-images.githubusercontent.com/51777024/85918661-66500180-b882-11ea-9255-c9054e1eb3e2.jpg)
![Screenshot_20200627_135558](https://user-images.githubusercontent.com/51777024/85918664-6cde7900-b882-11ea-98ce-b0bfe97b500f.jpg)



# Creating a new project and add necessary libraries

Open Android Studio and create a new project. I have created DemoTabLayout.

After create a new project, First of all we have to need include design libraries in the dependencies section of our build.gradle file so include this libraries in your build.gradle file by below line.

```
implementation 'com.android.support:design:28.0.0'
```

# Create Two Fragments

## Goto java first package right click select New  Select Fragment -Fragment_blank

* Upload Fragment
```
package com.vikas.demotablayout;
import android.os.Bundle;
import android.support.v4.app.Fragment;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
class Upload extends Fragment {
   @Override
   public View onCreateView(LayoutInflater inflater, ViewGroup container,
               Bundle savedInstanceState) {
           return inflater.inflate(R.layout.fragment_upload, container, false);
         }
   }
```
# It’s layout

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
     
    <TextView
      android:id="@+id/textView"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:layout_centerInParent="true"
      android:text="Video"
      android:textAppearance="?android:attr/textAppearanceLarge"/>

 </RelativeLayout>
```


* Upload Fragment
```
package com.vikas.demotablayout;
import android.os.Bundle;
import android.support.v4.app.Fragment;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
class Video extends Fragment {
   @Override
   public View onCreateView(LayoutInflater inflater, ViewGroup container,
               Bundle savedInstanceState) {
           return inflater.inflate(R.layout.fragment_video, container, false);
         }
   }
```
# It’s layout

```
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">
     
    <TextView
      android:id="@+id/textView"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:layout_centerInParent="true"
      android:text="Video"
      android:textAppearance="?android:attr/textAppearanceLarge"/>

 </RelativeLayout>
```
# goto activity_video.xml file


```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    tools:context=".VediosActivity">

    <android.support.design.widget.TabLayout
        android:background="@drawable/shape"
        app:tabIndicatorColor="#FF5722"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/vtab">

    </android.support.design.widget.TabLayout>
    <android.support.v4.view.ViewPager
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:id="@+id/vpager">

    </android.support.v4.view.ViewPager>
</LinearLayout>
```

# Goto VideoActivity get the id for ViewPager and TabLayout,and Create the VideoMyAdapter

```
package com.example.findapp;

import android.os.Bundle;
import android.support.annotation.Nullable;
import android.support.design.widget.TabLayout;
import android.support.v4.app.Fragment;
import android.support.v4.app.FragmentManager;
import android.support.v4.app.FragmentStatePagerAdapter;
import android.support.v4.view.ViewPager;
import android.support.v7.app.AppCompatActivity;

public class VediosActivity extends AppCompatActivity {

   ViewPager pager;
   TabLayout layout;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_vedios);
        pager=findViewById(R.id.vpager);
        layout=findViewById(R.id.vtab);
        pager.setAdapter(new VedioMyAdapter(getSupportFragmentManager()));
        layout.setupWithViewPager(pager);

    }

    public class VedioMyAdapter extends FragmentStatePagerAdapter
    {
        public VedioMyAdapter(FragmentManager fm)
        {
            super(fm);
        }

        @Override
        public Fragment getItem(int i)
        {
            switch (i)
            {
                case 0:return new VideoFragment();
                case 1:return new ShowVdeioFragment();

            }
            return null;
        }

        @Override
        public int getCount() {
            return 2;
        }

        @Nullable
        @Override
        public CharSequence getPageTitle(int position) {
            switch (position)
            {
                case 0:return "Upload";
                case 1:return "Vedios";

            }
            return super.getPageTitle(position);
        }
    }
}

```
# Right click on java first package Select New Class Name Video

```
package com.example.findapp;

public class Video
{
    private String about;
    private String video_url;

    public Video() {

    }

    public Video(String about, String video_url) {
        this.about = about;
        this.video_url = video_url;
    }

    public String getAbout() {
        return about;
    }

    public String getVideo_url() {
        return video_url;
    }
}

```
# Goto fragment_video Xml file

```

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    tools:context=".VideoFragment">

    <VideoView
        android:id="@+id/videoView"
        android:layout_width="match_parent"
        android:layout_height="250dp">
    </VideoView>

    <android.support.design.widget.TextInputLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="35dp"
        app:passwordToggleTint="@color/colorAccent">

    <EditText
        android:id="@+id/editText"
        android:hint="Enter Workshop Name"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

    </EditText>
    </android.support.design.widget.TextInputLayout>
    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:gravity="center"
        android:layout_margin="10dp"
        android:orientation="horizontal">
        <Button
            android:id="@+id/button2"
            android:text="choose\nvedio"
            android:layout_margin="20dp"
            android:background="@drawable/shape1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content">

        </Button>
        <Button
            android:id="@+id/button"
            android:text="upload\nvedio"
            android:layout_margin="20dp"
            android:background="@drawable/shape1"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content">

        </Button>
    </LinearLayout>

</LinearLayout>
```
# Goto VideoFragment Activity File get the id's and implement the upload the images into firebase storage

```
package com.example.findapp;


import android.app.ProgressDialog;
import android.content.Intent;
import android.database.Cursor;
import android.net.Uri;
import android.os.Bundle;
import android.provider.MediaStore;
import android.support.annotation.NonNull;
import android.support.v4.app.Fragment;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.Button;
import android.widget.EditText;
import android.widget.MediaController;
import android.widget.Toast;
import android.widget.VideoView;
import com.google.android.gms.tasks.OnFailureListener;
import com.google.android.gms.tasks.OnSuccessListener;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.storage.FirebaseStorage;
import com.google.firebase.storage.StorageReference;
import com.google.firebase.storage.UploadTask;
import java.util.HashMap;
import java.util.Map;

public class VideoFragment extends Fragment {


    private StorageReference mStorageRef;
    DatabaseReference database;
    Button choose, upload;
    EditText text;
    Uri mainUri, dbstoredPath;
    VideoView videoView;
    private static final int SELECT_VIDEO = 1;
    private String selectedVideoPath;
    MediaController videoMediaController;
    int RESULT_OK;
    ProgressDialog progressDialog;

    public VideoFragment() {
        // Required empty public constructor
    }
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState) {
        View view = inflater.inflate(R.layout.fragment_video, container, false);

        videoView = view.findViewById(R.id.videoView);
        text = view.findViewById(R.id.editText);
        videoMediaController = new MediaController(getActivity());
        choose = view.findViewById(R.id.button2);
        choose.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Intent i = new Intent(Intent.ACTION_PICK, android.provider.MediaStore.Video.Media.EXTERNAL_CONTENT_URI);
                startActivityForResult(i, SELECT_VIDEO);
            }
        });
        
        upload=view.findViewById(R.id.button);
        upload.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                if (mainUri!=null){
                    showProgress();
                    text.getText().toString();
                    mStorageRef = FirebaseStorage.getInstance().getReference().child("Videos").child(mainUri.getLastPathSegment());
                    database = FirebaseDatabase.getInstance().getReference("Videos");

                    mStorageRef.putFile(mainUri)
                            .addOnSuccessListener(new OnSuccessListener<UploadTask.TaskSnapshot>() {
                                @Override
                                public void onSuccess(UploadTask.TaskSnapshot taskSnapshot) {
                                    mStorageRef.getDownloadUrl().addOnSuccessListener(new OnSuccessListener<Uri>() {
                                        @Override
                                        public void onSuccess(Uri uri) {
                                            dbstoredPath = uri;
                                            Toast.makeText(getActivity(), "Uploaded!!!", Toast.LENGTH_SHORT).show();
                                            Log.i("Upload:",""+uri.toString());

                                            Map<String,Object> map = new HashMap<>();
                                            map.put("about",text.getText().toString());
                                            map.put("video_url",uri.toString());
                                            database.child(text.getText().toString()).setValue(map);
                                            Toast.makeText(getActivity(), "Saved", Toast.LENGTH_SHORT).show();

                                            progressDialog.dismiss();
                                            getActivity().finish();
                                        }
                                    });

                                }
                            })
                            .addOnFailureListener(new OnFailureListener() {
                                @Override
                                public void onFailure(@NonNull Exception e) {
                                    Log.i("Upload:","Failed :"+e.getMessage());
                                }
                            });

                }else {
                    Toast.makeText(getActivity(), "Please Select video!!!", Toast.LENGTH_SHORT).show();
                }

            }
        });
        return view;
    }
    public void showProgress(){
        progressDialog = new ProgressDialog(getActivity());
        progressDialog.setTitle("Uploading..");
        progressDialog.setMessage("please wait uploading in progress...");
        progressDialog.show();
    }

    @ Override
    public void onActivityResult(int requestCode,
                                 int resultCode, Intent data) {
        Toast.makeText(getActivity(), "onActivityResult..."+requestCode, Toast.LENGTH_SHORT).show();
        /*if (resultCode == RESULT_OK) {*/
            selectedVideoPath = getPath(data.getData());

            Log.i("Check:::", "onActivityResult: "+selectedVideoPath);
            if (requestCode == SELECT_VIDEO) {
                selectedVideoPath = getPath(data.getData());
                if(selectedVideoPath == null) {
                    Log.e("selected video path ","= null!");
                    getActivity().finish();
                } else {

                    Log.i("URI",selectedVideoPath);

                    videoView.setVideoURI(data.getData());
                    mainUri = data.getData();
                    videoMediaController.setMediaPlayer(videoView);
                    videoView.setMediaController(videoMediaController);
                    videoView.requestFocus();
                }
            }
    }

    private String getPath(Uri data) {
        String[] projection = { MediaStore.Images.Media.DATA };
        Cursor cursor = getActivity().managedQuery(data, projection, null, null, null);
        if(cursor!=null) {
            int column_index = cursor.getColumnIndexOrThrow(MediaStore.Video.Media.DATA);
            cursor.moveToFirst();
            return cursor.getString(column_index);
        }
        else return null;
    }
}
```
# Retrive the Video Into A FireBase Storage To Display the Recyclerview.


# Step1:Create A ShowVdeioFragment 

# Step2:goto fragment_show_vdeio xml file


```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:orientation="vertical"
    tools:context=".ShowVdeioFragment">

    <android.support.v7.widget.RecyclerView
        android:layout_width="match_parent"
        android:id="@+id/rec"
        android:layout_height="wrap_content"
   />


</LinearLayout>

```
# Step3:goto ShowVdeioFragment  file

```
package com.example.findapp;

import android.os.Bundle;
import android.support.annotation.NonNull;
import android.support.v4.app.Fragment;
import android.support.v7.widget.LinearLayoutManager;
import android.support.v7.widget.RecyclerView;
import android.util.Log;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import com.google.firebase.database.DataSnapshot;
import com.google.firebase.database.DatabaseError;
import com.google.firebase.database.DatabaseReference;
import com.google.firebase.database.FirebaseDatabase;
import com.google.firebase.database.ValueEventListener;
import java.util.ArrayList;

public class ShowVdeioFragment extends Fragment {


    RecyclerView recyclerView;
    DatabaseReference reference;

    public ShowVdeioFragment() {
    }
    @Override
    public View onCreateView(LayoutInflater inflater, ViewGroup container,
                             Bundle savedInstanceState)
    {
        View view=inflater.inflate(R.layout.fragment_show_vdeio,
                container, false);

        recyclerView = view.findViewById(R.id.rec);

        reference = FirebaseDatabase.getInstance().getReference("Videos");

        final ArrayList<Video> list = new ArrayList<>();
        reference.addValueEventListener(new ValueEventListener() {
            @Override
            public void onDataChange(@NonNull DataSnapshot dataSnapshot) {
                for (DataSnapshot ds : dataSnapshot.getChildren()){
                    Video model = ds.getValue(Video.class);
                    list.add(model);
                }
                Log.i("logs:","list size:"+list.size());
                recyclerView.setLayoutManager(new LinearLayoutManager(getActivity()));
                recyclerView.setAdapter(new VideoAdapter(getContext(),list));
            }

            @Override
            public void onCancelled(@NonNull DatabaseError databaseError) {

            }

        });

        return view;
    }

}

```

# Step4:Create the videorow.xml file

```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    >

    <ImageView
        android:id="@+id/video"
        android:layout_width="match_parent"
        android:layout_height="200dp"
        android:scaleType="fitXY"
        android:layout_gravity="center"
        android:src="@drawable/play"/>

    <TextView
        android:id="@+id/videoname"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:textStyle="bold"
        android:gravity="center"
        android:text="Video Name"
        android:textSize="25sp"/>
   
</LinearLayout>

```

# Step5:Create a Adapter Class name as VideoAdapter

```
package com.example.findapp;

import android.content.Context;
import android.content.Intent;
import android.support.annotation.NonNull;
import android.support.v7.widget.RecyclerView;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.ImageButton;
import android.widget.ImageView;
import android.widget.TextView;
import android.widget.Toast;
import com.bumptech.glide.Glide;

import java.util.ArrayList;

class VideoAdapter extends RecyclerView.Adapter<VideoAdapter.VHolder>
{
    Context context;
    ArrayList<Video> list;

    public VideoAdapter(Context fragment, ArrayList<Video> list)
    {
        this.context=fragment;
        this.list=list;
    }

    @NonNull
    @Override
    public VideoAdapter.VHolder onCreateViewHolder(@NonNull ViewGroup viewGroup, int i)
    {
        View view= LayoutInflater.from(context).inflate(R.layout.videorow,viewGroup,false);

        return new VHolder(view);
    }

    @Override
    public void onBindViewHolder(@NonNull VideoAdapter.VHolder vHolder, final int i)

    {
        vHolder.name.setText(list.get(i).getAbout());
        Glide.with(context).load(list.get(i).getVideo_url()).into(vHolder.video);
    }

    @Override
    public int getItemCount() {
        if (list!=null) {
            return list.size();
        }else {
            return 0;
        }
    }

    public class VHolder extends RecyclerView.ViewHolder 
        TextView name;
        ImageView video;
    
        public VHolder(@NonNull final View itemView)
        {
            super(itemView);
            name = itemView.findViewById(R.id.videoname);
            video = itemView.findViewById(R.id.video);
        }
    }
}

```


