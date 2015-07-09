# Augmented reality for archaeology with Vuforia SDK and Unity3d

In the presentation, we saw a number of potential use cases for AR in archaeology. In this tutorial, we'll build a simple AR app that overlays content on the real world, tied to an image or pattern viewed through your smartphone/tablet's camera. 

That is, an AR pop-up book!

(By the way, since the latest version of Unity3d comes with 'stereoscopic' abilities natively enabled, as a further step one could package what we are going to build, with some tweaking, as a google cardboard app). 

## Ingredients

+ [Unity3d (version 5)](http://unity3d.com/get-unity/download?ref=personal). **nb** the documentation for Unity is excellent. After you've completed this tutorial, try the '[Rollaball](https://developer.vuforia.com/downloads/sdk)' tutorial to explore in more depth concepts such as scripting.
+ [Vudoria SDK](https://developer.vuforia.com/downloads/sdk)  You will need to register with their site, which you will be prompted to do when you download. This only takes a few moments.
+ some tracking images
+ [A license key](https://developer.vuforia.com/license-manager) Login using your vuforia login to create and manage a license key.
+ images [to turn into tracking targets](https://developer.vuforia.com/target-manager). Again, you need to login with your vuforia login to use their  Why not use these images? **link** . [Here's some guidance on what makes a good image, for future reference.](https://developer.vuforia.com/library/articles/Best_Practices/Attributes-of-an-Ideal-Image-Target)

(While not necessary for this tutorial, you might like to know how to augment 3d objects, in the manner Eve does in the 'Roman fort' video we looked at. You use [this tool](https://developer.vuforia.com/downloads/tool) in conjunction with an android device, to turn the 3d object into xml that the Vuforia sdk can associate with your augmentations.)

## Thinking about metaphors

What makes a pop-up book compelling? Watch this short video - 

[![Dr. Jekyll and Mr. Hyde]((https://img.youtube.com/vi/7d7tTcSFZas/0.jpg))](https://www.youtube.com/embed/7d7tTcSFZas)

What I like about this is that the augmentations _enhance_ the content of the book. They make _sense_, and it's almost as if sublter, deeper meanings of the text are brought out by the augmentations. They play with, and enhance, the idea of transformation and the monster within. Like for Dr. Jekyll, the monster within can only be brought out using the potion, that is, the magic eye of the AR camera. Digital technology is at its most _affective_ when its metaphors are congruent with the materials.

In this tutorial then I started wondering, what material would it be _most meaningful_ to augment? We're used to the idea of publishing a talk as an essay. The written text conveys something of the show, the performance. We're used to the idea of video or audio taping the talk. But what if the talk was published as an augmented reality book?  