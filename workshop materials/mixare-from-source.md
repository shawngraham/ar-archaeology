## Building Mixare from Source

I followed this tutorial: [https://sashageekette.wordpress.com/2012/12/02/getting-started-with-mixare-on-eclipse/](https://sashageekette.wordpress.com/2012/12/02/getting-started-with-mixare-on-eclipse/). What follows are my notes to myself as I worked through them. This isn't a tutorial, but between this and Sasha's tutorial, you should be able to build the app. And of course, once you see how to built it, you can begin to modify it! A good place to look for help is [Stack Overflow](http://stackoverflow.com/search?q=mixare)

+ Get android SDK and know where it is (on my machine, `users/shawngraham/library/android-macos`)
+ Get [eclipse java](https://eclipse.org/downloads/)
+ Get adt for eclipse [http://developer.android.com/sdk/installing/installing-adt.html]

1. open eclipse
2. set new workspace 
3. click on 'workbench' if you get the welcome screen
4. file - new project - android - android project from existing code
5. select the unzipped github package for mixare (ie, the folder you downloaded, unzipped; on my machine it unzipped as 'mixare-master')
6. tick off the 'copy projects into workspace' button. Hit finish.

  Your console probably fills up with errors like this:
`[2015-08-05 11:59:36 - mixare-arena-splashscreen-plugin] Unable to resolve target 'Google Inc.:Google APIs:10'`

  Which means we have to get the Google APIs (in addition to the SDK)

7. Look for the Android SDK Manager in your tool ribbon - it's a little android in a box with a down arrow. If you don't have that, you can find it within the Android SDK at 
`/Users/shawngraham/library/android/sdk/tools`

  You can launch it by typing `./android sdk` at the prompt (assuming you're on a mac)

  Now, you're looking for the Google API revision 10 (Android 2.3.3) - since Mixare is old software that hasn't been updated in a while, you'll have to tick off the `obsolete` button to find the right API. 

8. Right click in the project, select 'properties' then 'api' and select the google api.

9. Now, we need to import mixare - plugins - mixare-library as its own project.  Right-click in the project explorer pane and select import. Then under `general` select `existing projects into workspace`. Select the `browse` button and find mixare-library. 

  Eclipse might throw an error saying there is no `res` folder under mixarelib. If so, right-click on mixarelib (the new project one) and select 'new' folder and call it `res`.

10. Right-click on mixarelib and select 'properties'. Set the API level appropriately; also tick off the 'is library' box.

11. Right-click on `buil.xml` and select `run as` - `ant build`. If all goes according to plan, you'll see `BUILD SUCCESFUL` in the console window, and a new file called `mixarelib.jar` in the project explorer.

Then, export as Android application.

