# Installing and Using VSFM 
## from the command line

The [VSFM package](http://ccwu.me/vsfm/) is not easy to install or work with. However, there is a (relatively) easy way to use it as a 'container' - that is, a virtual machine set up just for image processing and point cloud extraction etc from the images. Ryan Baumann from the [Duke Collaboratory for Classics Computing](https://blogs.library.duke.edu/dcthree/) has [put all of the necessary bits-and-bobs together to run VSFM this way](http://ryanfb.github.io/etc/2015/01/13/docker_for_visualsfm.html).

## Ingredients

+ [Docker](https://docs.docker.com/installation/)

## Recipe

1. Download and install docker for your machine. 

2. Then, open a terminal or command prompt and type

`$ boot2docker start`

`$ eval "$(boot2docker shellinit)"`

3. Now you're ready to go. Next thing we'll do is download and install Ryan's container which has not just VSFM, but also [youtube-dl](https://rg3.github.io/youtube-dl/) and [avconv](https://libav.org/avconv.html), a video and audio converter. At the prompt, type:

`$ docker run -i -t ryanfb/visualsfm /bin/bash`

This downloads and installs all the bits and bobs to run VSFM _in a linux virtual machine_ living inside a container on your computer. **This will take a long time to run the first time you do this.** But, what's nice is that the _next_ time you run that command, nothing needs to be downloaded - instead, it's like you've flipped the on switch on your very own point cloud extractor machine.

Now, the thing is: how do you get your images into that container? We do this by making an in-out tray (as it were) that connects the rest of your machine with the virtual machine. Once the command above has stopped running (and you'll know this is the case when the $ prompt appears again), type `exit` and hit enter. You're back at your normal command prompt.  

4. Go back and type the commands from step 2. This time, when you get to step 3, we're going to add a `-v` flag to the command that ties our two machines together. On my Mac, I created a folder called `dockerific` and I want to tie it to the `tmp` file in the virtual machine. This command spins up my virtual machine with VSFM in it, and makes that connection, that in-out tray, between the two:

`$ docker run -i -t -v /Users/shawngraham/dockerific/:/tmp/ ryanfb/visualsfm /bin/bash`

So, after the `-v` I included the full file path (on a Mac; PC you'd start with C:/ etc) and after the colon the linux file path to the tmp folder. Run that command now.

At the prompt, type `ls` (for list) and it will show you all of the bits and pieces - files and folders - that make up the VSFM part of this container. If you then typed `cd ..` (for change directory by going up a level in the folder tree) and then `ls` again, you'd see a whole list of folders, one of which will be `tmp`. Anything you put in that folder will turn up in the other folder you connected to in the `docker run` command, and vice versa! So, you can drop all of your images into (in my case) `dockerific` and have them turn up in `tmp`. Do that now.

5. Move your images out of the `tmp` folder to the VSFM by using the [CP command](http://www.computerhope.com/unix/ucp.htm). I'd suggest doing this by copying the whole `tmp` folder and giving it a new name. So, make sure you're at the home directory in the VM by using `cd ~` (check you're in the right place with the `ls` command - you should see a series of files and folders like cmvs, cmvs.tar.gz etc). Then, 

`cp -R ~/tmp/ images`  [SHAWN CHECK THAT THIS WORKS]

ALTERNATIVELY, what if you had drone footage of an archaeological site and you wanted to build the model from that? You'd follow [Ryan's workflow](http://ryanfb.github.io/etc/2014/10/22/drone_photogrammetry_workflow.html), which I'm also copying here:

5a. get the footage from youtube with '$ youtube-dl 'https://www.youtube.com/watch?v=3v-wvbNiZGY'`
