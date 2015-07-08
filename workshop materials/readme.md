# Workshop Materials

There are three options that I think we can explore in this workshop. 
	+ Building an AR app in Unity3d with the Vuforia SDK
	+ Hacking Twine to make a location-based game
	+ Building 3d models using 123d catch, and then making them Oculus Rift or Google Cardboard-ready on Sketchfab

The first option involves making a simple augmented reality pop-up book. AR pop-up books traditionally (if we can speak of tradition) tie 3d objects, sound, or video to tracking images on the page. One holds one's device over the page to see the augmentations. Unity3d is a game engine that is often used for authoring these kinds of things. (Unity3d also has plugins for working with stereoscopic viewers such as Google cardboard. Looking through your device in this way is more _elegant_ than holding it, but for the purposes of this workshop, we'll keep it simple for now). 

The second option uses the Twine interactive-fiction authoring platform. Twine is actually a kind of highly modified wiki page. The nice thing is, using it allows you to rapidly build a gameful/interactive environment that lives as a single webpage, and can be served up via github pages or a public dropbox folder or what have you. You can use javascript within a Twine story to access a device's geolocation, and so we can use geotriggers to reveal passages of text or sound or indeed embedded 3d models. In my imagination, I see this as a way of doing something rather similar to the [Ghosts in the Garden](http://www.react-hub.org.uk/heritagesandbox/projects/2012/ghosts-in-the-garden/) or as a portal to some sort of alternate reality game experience.

Since so much of augmented reality (as it is currently imagined) depends on fitting 3d models into the 'real' world, the third option is an opportunity to explore making 3d models via 123d catch, cleaning them up (and reducing them in complexity to fit through the AR pipeline) with Meshlab, and sharing them via Sketchfab or p3d.in. Models can also be stored in your github space, and rendered (without textures) on your repo's webpage. 3d modesl can also be printed, of course, and this opens up another front in that smearing continuum of reality - mixed reality - augmented reality - virtual reality. What could 'augmented reality' mean for someone who has limited sight?   ![pinboard](https://pbs.twimg.com/media/CJT5-0fWcAAe5PZ.jpg) (see this tweet from [Lawrence Shaw](https://twitter.com/lawrence_shaw/status/618393921941585921)). (Also, do a Google search for Stu Eve's 'Dead Man's Nose'.)

## Augmented reality platforms

While we will be building our own app from scratch via Unity3d, there are many platforms out there that (if you're willing to stay within their product) can get you up and running much quicker.

+ *Aurasma*  Aurasma has an editor that allows you to tie text, links, sound files, or models to tracking images. You upload your desired tracking images and your assets to a file system, and then create associations between the images and the assets (which augment the image). One thing I've found when working with Aurasma is that the models have to be in Collada .dae format (a kind of xml). Oddly enough, the dae files produced by Meshlab don't seem to get recognized by Aurasma's system. You have to produce with 3ds Max using the OpenCollada plugin for best results.  To view your materials, you have to put the Aurasma app on your device, and search for your username.

+ *Augmentedev* Augment is a similar app with web based editor. It has a 30 day free trial (although educational accounts are possible at reduced price or free; contact them). Models and tracking images are loaded and then associated one with another through the web editor. On your device, you hit the 'scan' button within the app and hold it over an image. Augment will search its database of all tracking images, finding yours, and revealing your asset. In terms of 3d models, Augment is nice because you can manipulate them (rotating, resizing, etc) once they're revealed. 

+ *Junaio* I spent a lot of time working with Junaio, which though powerful, was not user friendly. It did allow you to hold all of the assets on your own server space, which was good. Junaio and its parent Metaio have been bought by Apple, and there is no point in discussing them any further until we find out what Apple intends to do.

## Ancillary programs

+ *Meshlab*