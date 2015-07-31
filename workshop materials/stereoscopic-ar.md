# Make your AR app Cardboard-able

**update July 30th 2015** Vuforia has just released their SDK version 5, which renders this tutorial obsolete. The instructions below do work though for Unity 5 with Vuforia 4 SDK. To see the SDK 5 version, [download my 'diary in the attic' project](https://www.dropbox.com/s/kvb2b2kls7zq6js/diary-in-attic-project.zip?dl=0) and have a look about. You can install the built project by [downloading the .apk here](https://www.dropbox.com/s/t1tq7mzxscy3c0o/test-new-sdk5.apk?dl=0) (sorry ios users).

In essence, don't mess with the cameras, just slot my materials out (in the assets - models folder; also 'resources - splash' for the splash scene) and put your own in. You'll need to add your own license key & tracking images database. You might have to adjust player settings too. Watch out for doppler effects and logarithmic dropoffs in 3d sound. [see bottom for a few other things to note re sdk5](#some-settings-in-the-sdk-5-for-stereoscopy)

-----
*Stereoscopy in Vuforia SDK 4:*

[Google Cardboard's viewer](https://www.google.com/get/cardboard/) is a wonderful, lo-tech device. One of the biggest issues with smartphone augmented reality is the sheer awkwardness of trying to hold a camera or a tablet over whatever it is you've augmented. Cardboard solves this problem for us by using the magic of stereoscopy, or showing slightly off-set versions of the same scene at the right distance from the eyes that our brains turn it into 3d.

![img](https://developer.vuforia.com/sites/default/files/Screenshot_2015-06-26-16-49-05.png)
<small> _This screenshot was posted by user 'Okirokai' in a Vuforia discussion forum on stereoscopy. Look at [his post, how simple it appears](https://developer.vuforia.com/forum/unity-3-extension-technical-discussion/two-stereo-cameras-independent-ar-camera#comment-2051448) eh? The devil is in the details though..._</small>

You can imagine possible use cases - a diorama of Pompeii at a museum for instance, where the major buildings are recognized by the Vuforia SDK (you'd use the 'objectTarget' prefab); visitors could put their phones into Cardboard and 'excavate' the city. Or perhaps visitor panels or historic plaques at a site are augmented; since the AR app allows you to see the real world beyond, there'd be no colliding with benches... Your ideas will no doubt be better than mine.
 
As it turns out, it is quite easy to turn our AR experience we created in the previous tutorial into a stereoscopic experience which we can load onto our smartphones, to be viewed through the Cardboard viewer. The trick, as with all things computational, are the silences, the bits left unsaid that can drive you nuts as you try to figure out why only the left eye is working, or why the screen is fritzing out...

### Step 1

Let's address the fritzing out issue first. You might have noticed that there's a great big 'play' button in your Unity editor (ie, a right-pointing triangle). You can use this to test your app without building it. When you hit it, your app will display on your computer's monitor, with the AR being overlaind on the computer's webcam. You can hold up your image target (I've printed out all of mine) in front of your webcam, to see how your AR looks. We will be using **three** camera components in your scene (more on that in a moment); when there's more than one camera and we hit the 'play' button, the screen can start to flicker madly as it tries to draw our augmentation. This will also happen on your device; we can reduce this by going to `File > build settings` and ticking off the 'development build' box. **Even with this ticked off** what you see on your computer's monitor will not be quite the same as on your device. Nevertheless, we need to check it off; it will make your app on your device run much much clearer, and eliminate most (if not all) that flickering/fritzing. You can experiment with 'development build' on and off after you've built the app if you want (notice 'development build' at the bottom left of the screenshot above).

### Step 2

In your hierarchy, hit the `ARCamera` item. ARCamera is a label for all the different components that build the view you see. Think of it as a folder. In "normal" ar, you only have the 'Camera' component inside this folder. Right-click on the `Camera` inside `ARCamera` and select 'duplicate'. This will make a new component called `Camera (1)`. Duplicate `Camera` again. Ta da, a new component called `Camera (2)` appears.

### Step 3

Click on the first `Camera` component. In the inspector panel that opens (mine's on the right hand side of the screen) there are a number of subpanels, including one called 'Camera' (it has a little movie-film camera icon; you want this one, not the one at the top of the screen beside the cube icon). **Uncheck** the radio button beside the word 'Camera' in this subpanel.

![Imgur](http://i.imgur.com/spBz40J.png)

### Step 4

Click on `Camera (1)`. In the inspector, you can rename it 'CameraLeft' (you do this at the top of the inspector panel, beside the cube icon). Notice in the Camera sub panel in the inspector panel there is a setting called 'Viewport Rect'. We're going to shift the view to the left a wee bit. Change the default to these settings: 

+ x: 0
+ y: 0
+ w: 0.5
+ h: 1

and set the Depth to **-1**. Do not touch any of the other settings. (When you are done, and you see the result, you may wish to experiment with making the steroscopic effect more pronounced. You do this by adjusting the X value, ie, you could set it to x=-0.5 . Think of progression into negative numbers as moving further and further left.)

### Step 5

Click on `Camera (2)'. In the inspector, rename it 'CameraRight'. Change the 'Viewport Rect' settings to:

+ x: 0.5 
+ y: 0
+ w: 0.5
+ h: 1 

and set the Depth to **1**

![image](http://i.imgur.com/znieFFa.png)

### That's it.

Seriously. That's all there is to it. Press play and you should have a split screen, showing ever-so-slightly different views. Hold up one of your image targets. Your augmentation should be displayed (or played, in the case of audio). **You might notice a lot of flickering pixelation**. This is that issue I was talking about in step 1. If you tick 'development build' in your build settings, **the pixelation will probably still happen on your _desktop_ when you 'play' the app** but it will be **clean and tidy** when you push it to your device. 

Go to `file > save scene as` and give your scene a new name, eg 'stereobuild'. Then, when you go to `file > build settings` make sure to *unselect* your simple AR scene and select your 'stereobuild' scene. Make sure 'development build' is ticked off, and then hit `build and run`. When it runs on your device, there will be no pixelation.

(By the way, when you click on `Assets` in the project panel, you will now have two 'scenes' that you can flip between, just by clicking on them. Scenes use the Unity3d logo as their icon. One is your 'normal' AR, the other is your stereoscopic one. You should also save your project. When you come back to your project, you can then open whichever scene you wish to work on)

### But one camera is blank!

But what if you get a result like this:

![Imgur](http://i.imgur.com/GCOrXbe.png)

ie, one side is blank. One issue could be that that particular camera - in this case `Cameraright` - has been ticked off. Click on that camera in the Hierarchy view, and check to see if the radio box beside 'camera' in the inspector is ticked or not. 

So you've checked for that, and found that the camera is ticked on, but it's just not displaying. This happened to me. I discovered that the Camera, when we first duplicated it back in step 2, did not fully replicate; not all of its pieces came with me! Take a look at the image below, which shows a project I'm working on. In the Hierarchy, I've selected the first `Camera`. It's the one *we want* to be switched off in under 'camera' on the inspector panel (where the movie-camera icon is). But look in the scene in the middle of the image. Notice the white square and the white 'x'. This is the camera's view. Notice also the camera preview window in the bottom right of the scene - it shows my image targets. This camera is working correctly. 
![Imgur](http://i.imgur.com/PGxSCSA.png)

What we're going to do is check to see if that right-hand camera has its view, that white square and x. We're going to turn off `Camera` and `CameraLeft`. In this case, you'd uncheck 'Camera' **at the top of the inspector panel, beside the cube icon** which totally deactives this camera, for those two cameras. Then we'd select `CameraRight` in the hierarchy. When I did this, even though this camera was activated (and its camera compenent was activated too - both camera check boxes were ticked off), _there was no white square and white x_ in the scene, nor was there anything in the camera preview box. 

My right camera was completely borked. But I knew that the left camera was working fine. So I returned everything to how it had been, deleted the right camera, duplicated the left camera, and hit 'play' again. This time, it worked.

###some settings in the SDK 5 for stereoscopy
- get a new license key, set it for 'mobile'
- vuforia 5 works best with unity 4.6
- you have to add the android SDK again (or the ios sdk) to build settings (on my computer, android sdk lives at: user/shawngraham/library/androidsdkmacos)
- player settings have to set that com.yourdomain.yourappname (i use com.graeworks.myapp)
- build settings: enable development build for good measure.

