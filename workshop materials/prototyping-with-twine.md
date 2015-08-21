# An Exercise in Prototyping

The thought occurred to me - 

> maybe it'd be better to have folks sketch things out first - have 'em sketch out what an AR experience _could_ be that makes sense for them, for their research or outreach or teaching needs.

So here's what I propose to do. In the time we have available to us, let's code some quick interactive playable _sketches_ using Twine. (Some game design folks actually _do_ use Twine in this fashion (as for example [here](http://gersande.com/twine-as-a-prototyping-tool/) and [here](http://www.sibylmoon.com/twine-as-a-prototyping-tool/) ). 

Let's do this in small groups (if you'd like) - find someone you haven't had a chance to work with much yet.

# Framing questions

You've been tasked to create a new interactive _x_ at your work. 

- what is the story?
    - sum it up in 140 characters. Ish. ([rationale for that](http://epress.trincoll.edu/webwriting/chapter/graham/)) 
    - describe the interaction with the tech. 
    - describe the _flow_ of the interaction.

- what are the goals (outcomes)?  
    - what are the objectives (things that can be measured that lead to the goals)?
    - what are the assessment items (the things that do the measuring)?
    
# Build!

Go to [Twine](http://twinery.org/2/#stories) - you can install it on your machine or run it in your browser. Either way is fine.

Double-click on the passage. Begin writing text to describe your ideal user's first interaction with your application. You use double `[[` and `]]` to mark text that describes some kind of choice. For instance,

> `The cows are in the field. Do you try to [[tip them over]]?`

This will generate a new passage called `tip them over`, and make a line tying the passages together. When you're ready, hit the up-arrow at the bottom left of the interface to 'publish to file'. This will generate a single webpage with your complete mock up as html. Put it in a gh-pages branch of your Github repository, and you can share it with us. 

(Quick refresh on making Github serve your files: Remember the repository Ethan had you make? Save your html file in that folder on your machine. Open your github client. Click on that repository. It will know that you've added a file. Hit the changes button; put a message in the commit box; hit commit to master; hit sync. Go to the github website for your repository, in the branches box type `gh-pages` and it'll make a new branch with all of the existing stuff from the `master` branch in it. Hit settings to find the url, click on it, put the name of your prototype eg `shawn-prototype.html` at the end of the URL, and you've done it!)

Then we'll talk some more.

# The point

The point of this is to help you map out all the different kinds of mechanics that your vision needs. That way, you can work out which kind of tech you need to work with. It can help you communicate your ideas to designers or coders or administrators, it'll help you to understand your own needs better so you don't waste your time... 

Twine is very elastic; it can be used for very powerful work indeed - see Tara Copplestone's [Buried](http://taracopplestone.co.uk/buried.html) for instance. Why 'Buried' works is that Tara made the interaction reflect the theme of the work; it is art. The *rules* of interaction in digital media - not the graphics, not the pretty visuals, but the actual mechanics of how we react to the machine - are powerful forms of rhetoric that we're not in the habit of interrogating. Think of what Powerpoint has done to the lecture, this thing that encodes the rules of the business meeting. For my money, the digital media are at their best when their procedures, their rules, act _in harmony_ with the subject matter to create the argument you want your user to experience as an emergent phenomena. 
    
(oh, another interesting link - http://www.e-games.tech.purdue.edu/DesignDoc.asp)
