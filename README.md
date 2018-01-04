# LinkedIn-Login
To integrate LinkedIn with your mobile application, we need to create an new application in LinkedIn Developer’s Account. Go to https://www.linkedin.com/developer/apps and click on the Create Application button and a form will open that need to be filled to successfully create application on LinkedIn.

<h3>Set the Permission</h3>
We need to set the permission to get the access to retrieve the user’s LinkedIn profile details. We need to select the r_basicprofile and r_emailaddress and click on the update button to set the permission.

<h3>Download & add Mobile LinkedIn SDK</h3>
Download the Mobile LinkedIn SDK from https://developer.linkedin.com/downloads#androidsdk. Unzip the downloaded file and add the linkedin-sdk directory in your project. linkedin-sdk already exist in the unziped directory.

<h3>Include linked-sdk library in the setting.gradle file</h3>
Open setting.gradle file in your project and include linked-sdk directory in your project.

```
include ':app', ':linkedin-sdk'
```

<h3>Adding support library in dependencies</h3>
To compile LinkedIn SDK, add the sdk in the dependencies. Open your build.gradle(app module) file and add linkedin-sdk in the dependencies. Also add the Picasso library to display Image.

```
compile project(':linkedin-sdk')
compile 'com.squareup.picasso:picasso:2.5.2'
```

<h3>Create Hash Key Layout</h3>
To integrate linkedin with Android App, we will generate hash key to integrate your app with linkedin account by adding the hash key into application that is created on LinkedIn Developer Account. To display hash key, we use TextView. So add the TextView in the activity_main.xml file.

```
<TextView
      android:id="@+id/hashKey"
      android:layout_width="wrap_content"
      android:layout_height="wrap_content"
      android:textSize="20dp"/>
     
 ```
 
<h3>Generate Hash Key</h3>
Generate the has key to integrate your app with LinkedIn Developer Account. Use the following code to generate hash key:

```public class MainActivity extends AppCompatActivity {
    //replace package string with your package string
    public static final String PACKAGE = "Your Package";
 
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
 
        generateHashkey();
    }
   
    public void generateHashkey(){
        try {
            PackageInfo info = getPackageManager().getPackageInfo(
                    PACKAGE,
                    PackageManager.GET_SIGNATURES);
            for (Signature signature : info.signatures) {
                MessageDigest md = MessageDigest.getInstance("SHA");
                md.update(signature.toByteArray());
 
                ((TextView) findViewById(R.id.hashKey))
                            .setText(Base64.encodeToString(md.digest(),
                            Base64.NO_WRAP));
            }
        } catch (PackageManager.NameNotFoundException e) {
            Log.d("Name not found", e.getMessage(), e);
 
        } catch (NoSuchAlgorithmException e) {
            Log.d("Error", e.getMessage(), e);
        }
    }
}
```

<h3>Add hash key in LinkedIn Developer Account</h3>
We will add the hash key in LinkedIn Developer account. Goto https://www.linkedin.com/developer/apps and click on your application name and select mobile tab. Add the Package name and hash key in the Android Setting. It will integrate your app with LinkedIn Developer Application.

<br></br>
<a href="url"><img src="https://github.com/sambhaji213/LinkedIn-Login/blob/master/screenshot/device.png" align="left" height="480" width="250"></a>
