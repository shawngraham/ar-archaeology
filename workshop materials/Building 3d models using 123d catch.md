# Generating a 3d model with 123D Catch

Autodesk has a suite of programs connected with 3d modeling. [123D Catch](http://www.123dapp.com/catch) is a free offering. The mobile apps let you take a series of photos which are then pushed to Autodesk HQ for processing; you can then log into their website to examine the model and download it (as .obj). So, install the app on your ios, android, or windows phone device. The first time you use it, you will have to do the usual registering and setting up of an account.

## Photography

Have someone sit as still as possible in a chair. Open the app, hit the big + button, and then the '+ start a new scan'. So start taking photographs. Move around your subject, move in and out, from on high and down low. You want to have a high degree of overlap - the software works by identifying matching overlapping points between photos. A point will end up in your final model if it is visible in at least three photographs ([see Peter Falkingham's helpful tips here](http://www.academia.edu/3649828/Generating_a_Photogrammetric_model_using_VisualSFM_and_post-processing_with_Meshlab)).

Don't use a flash; don't mount your object (or person, for that matter) on a turntable. You and the camera do the moving, not the object. 

When you think you have enough, press the checkmark. All of your photos will be displayed; you can delete any blurry ones. If you like what you've got, hit the check mark again. I have made decent models with as few as 12 photos. The app will then upload your photos to the servers for processing; a helpful little 'loading' doodad lets you know when they're all uploaded. When the status bar says 'ready' and there's another checkmark beside a thumbnail of your model, you can either review it in the app and make it public or you can log in to their website and work with it there. I'd suggest the latter.

If the upload fails, you have to close the app completely and relogin. This has been happening a lot to me lately.

When you're in the Autodesk website for 123D Catch, you go to your 'models' page, and hit the download button. They'll package everything up for you:
![Imgur](http://i.imgur.com/D8iRH8H.png)

...which, when unzipped, looks like this:

![Imgur](http://i.imgur.com/Rf790EX.png)

The .stl file can be used for 3d printing; the mesh folder contains the .obj file with the actual geometry of your model, an .mtl file that can be opened with a text editor (and describes which texture file goes with the mesh), and a .jpg that shows the model. We'll use all these in [Meshlab](http://meshlab.sourceforge.net/).

## Desktop PC app

The desktop PC app is an enormous pain in the rear. It too requires you to login to the autodesk servers before it will run, although if you hit 'create new' you can start working with it and login only when you're ready to upload. I'd suggest not bothering with it, as most times the mobile app works fine enough. If you do install it, it can be handy if you are working with photos you've taken with your own camera, or if you want to manually identify, one by one, points that appear in three different images. 

You can also add reference points (and thus volumes) to your 3d models using the desktop PC app - [this page](http://www.123dapp.com/howto/catch) has many video tutorials that can guide you through this process.

-----

That's all there is to it. It's possible to generate models from video stills too - you have to slice the video into individual frames. It's also possible to generate models from photographs from many different cameras. There are many different tools that can build point clouds and then meshes from photography - Ryan Baumann [does some comparison model building here](http://ryanfb.github.io/etc/2015/07/27/qualitative_photogrammetry_comparisons_gallery.html). [Photoscan from Agisoft](http://www.agisoft.com/) is good value for money, and is reasonably priced. You can use it for free - but the free version doesn't let you save your final model. Agisoft is good too when you want to create models that are dimensioned. The basic workflow in Photoscan is very straightforward. Start the program, and then in the toolbar click 'workflow'. The first item is 'select photos'. You do that. Indeed, you simply work through each option in turn as they become available:
![Imgur](http://i.imgur.com/XorKnvd.png)

Agisoft's [own tutorial](http://www.agisoft.com/pdf/PS_1.0.0%20-Tutorial%20(BL)%20-%203D-model.pdf) will get you started easily.

But - 123D catch uploads all your photos to servers who-knows-where (and do we ever read the TOS very carefully?) And maybe you don't have the money to purchase a tool like Photoscan. The VSFM package can be used (for free) and keeps everything under your own control. Getting it up and running is not easy, but it's not that hard. [Here's a tutorial that uses VSFM and also includes a workflow for downloading youtube drone videos, slicing the videos into stills, and stitches them altogether](3d%20model%20building%20with%20VSFM%20on%20the%20command%20line.md)



