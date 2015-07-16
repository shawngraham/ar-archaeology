# Make your AR app Cardboard-able

Google Cardboard's viewer is a wonderful, lo-tech device. One of the biggest issues with smartphone augmented reality is the sheer awkwardness of trying to hold a camera or a tablet over whatever it is you've augmented. Cardboard solves this problem for us by using the magic of stereoscopy, or showing slightly off-set versions of the same scene at the right distance from the eyes that our brains turn it into 3d.

![img](https://developer.vuforia.com/sites/default/files/Screenshot_2015-06-26-16-49-05.png)
<small> This screenshot was posted by user 'Okirokai' in a Vuforia discussion forum on stereoscopy. Look at [his post](https://developer.vuforia.com/forum/unity-3-extension-technical-discussion/two-stereo-cameras-independent-ar-camera#comment-2051448); looks simple, eh? The devil is in the details...</small>

You can imagine possible use cases - a diorama of Pompeii at a museum for instance, where the major buildings are recognized by the Vuforia SDK (you'd use the 'objectTarget' prefab); visitors could put their phones into Cardboard and 'excavate' the city. Or perhaps visitor panels or historic plaques at a site are augmented; since the AR app allows you to see the real world beyond, there'd be no colliding with benches... Your ideas will no doubt be better than mine.
 
As it turns out, it is quite easy to turn our AR experience we created in the previous tutorial into a stereoscopic experience which we can load onto our smartphones, viewed through the Cardboard viewer. The trick, as with all things computational, are the silences, the bits left unsaid that can drive you nuts as you try to figure out why only the left eye is working, or why the screen is fritzing out...

### Step 1

Let's address the fritzing out issue first. You might have noticed that there's a great big 'play' button in your Unity editor (ie, a right-pointing triangle). You can use this to test your app without building it. When you hit it, your app will display on your computer's monitor, with the AR being overlaind on the computer's webcam. You can hold up your image target (I've printed out all of mine) to your webcam, to see how your AR looks. We will be using **three** camera components in your scene (more on that in a moment); when there's more than one camera and we hit the 'play' button, the screen can start to flicker madly as it tries to draw our augmentation. This will also happen on your device; we can reduce this by going to `File > build settings` and ticking off the 'development build' box. **Even with this ticked off** what you see on your computer's monitor will not be quite the same as on your device, but it will make your app on your device run much much clearer, and eliminate most (if not all) that flickering/fritzing. You can experiment with 'development build' on and off after you've built the app.

### Step 2

In your hierarchy, hit the `ARCamera` item. ARCamera is a label for all the different components that build the view you see. Think of it as a folder. In "normal" ar, you only have the 'Camera' component inside this folder. Right-click on 'Camera' and select 'duplicate'. This will make a new component called `Camera (1)`. Duplicate `Camera` again. Ta da, a new component called `Camera (2)` appears.

### Step 3

Click on the first `Camera` component. In the inspector panel that opens (mine's on the right hand side of the screen) there are a number of subpanels, including one called 'Camera' (it has a little movie-film camera icon). **Uncheck** the radio button beside the word 'Camera' in this subpanel.

### Step 4

Click on `Camera (1)`. In the inspector, you can rename it 'CameraLeft'. Notice in the Camera sub panel in the inspector panel a setting called 'Viewport Rect'. We're going to shift the view to the left a wee bit. Have these settings: 

---
|x|0|
|y|0|
|w|0.5|
|h|1|

and set the Dept to -1. Do not touch any of the other settings.
