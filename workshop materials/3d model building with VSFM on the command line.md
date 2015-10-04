# Installing and Using VSFM via Docker
_(and then use Meshlab to make the model!)_

The [VSFM package](http://ccwu.me/vsfm/) is not easy to install or work with. However, there is a (relatively) easy way to use it as a 'container' - that is, a virtual machine set up just for image processing and point cloud extraction etc from the images. Ryan Baumann from the [Duke Collaboratory for Classics Computing](https://blogs.library.duke.edu/dcthree/) has [put all of the necessary bits-and-bobs together to run VSFM this way](http://ryanfb.github.io/etc/2015/01/13/docker_for_visualsfm.html).

## Ingredients

+ [Docker](https://docs.docker.com/installation/)
+ [Meshlab](http://meshlab.sourceforge.net/)

## Recipe

### Prep

+ Download and [install docker](https://docs.docker.com/installation/) for your machine. 

_Update August 15th_: Docker has just released a new series of tools; 'Boot2Docker' has been deprecated. With the new tools, the set up procedure goes like this:
+ in the installation dialogue, you have to install all the bits and bobs, including the the kitematic thing 
+ once everything is installed, run *kitematic* first; it will create a vm
+ leave that open. Run the docker quick start terminal (if you get the bash prompt without an error message, then everything is good and you can close kitematic).
+ connect the shell to the vm by running this command:

`$ eval "$(docker-machine env default)"`

+ You can now load Ryan's visaulsfm container by running:
`$ docker run -i -t ryanfb/visualsfm /bin/bash`

*warning: the first time you do this will take a _really_ long time.*  You can also download it using Kitematic; just search `ryanfb/visualsfm` in its search box, then hit download button. *Once you've done this* any subsequent time you want to run docker click on the shortcut to the docker'd terminal which will start up your virtual machine; you can then run the docker commands.

*If you already have boot2docker and haven't updated to the new tools* proceed as you usually do:

`$ boot2docker start`

`$ eval "$(boot2docker shellinit)"`

+ Now you're ready to go. Next thing we'll do is download and install Ryan's container which has not just VSFM, but also [youtube-dl](https://rg3.github.io/youtube-dl/) and [avconv](https://libav.org/avconv.html), a video and audio converter. At the prompt, type:

`$ docker run -i -t ryanfb/visualsfm /bin/bash` (but see the modification to this under 'accessing the innards' below)

This downloads and installs all the bits and bobs to run VSFM _in a linux virtual machine_ living inside a container on your computer. **This will take a long time to run the first time you do this.** But, what's nice is that the _next_ time you run that command, nothing needs to be downloaded - instead, it's like you've flipped the on switch on your very own point cloud extractor machine.

## Accessing the innards of that container while it is running

Now, the thing is: how do you get your images into that container? We do this by making an in-out tray (as it were) that connects the rest of your machine with the virtual machine. Once the command above has stopped running (and you'll know this is the case when the $ prompt appears again), type `exit` and hit enter. You're back at your normal command prompt.  

+ Go back and restart docker. Way fast, eh?

This time, when you get to `docker run`, we're going to add a `-v` flag to the command that ties our two machines together. On my Mac, I created a folder called `dockerific` and I want to tie it to the `tmp` file in the virtual machine. This command spins up my virtual machine with VSFM in it, and makes that connection, that in-out tray, between the two:

`$ docker run -i -t -v /Users/shawngraham/dockerific/:/tmp/ ryanfb/visualsfm /bin/bash`

So, after the `-v` I included the full file path (on a Mac; PC you'd start with C:/ etc) and after the colon the linux file path to the tmp folder. Run that command now.

### Get your images in place

At the prompt, type `ls` (for list) and it will show you all of the bits and pieces - files and folders - that make up the VSFM part of this container. If you then typed `cd ..` (for change directory by going up a level in the folder tree) and then `ls` again, you'd see a whole list of folders, one of which will be `tmp`. Anything you put in that folder will turn up in the other folder you connected to in the `docker run` command, and vice versa!

+ Drop all of your images into (in my case) `dockerific` and have them turn up in `tmp`. 

+ Move your images out of the `tmp` folder to the VSFM by using the [CP command](http://www.computerhope.com/unix/ucp.htm).

I'd suggest doing this by copying the whole `tmp` folder and giving it a new name. So, make sure you're at the home directory in the VM by using `cd ~` (check you're in the right place with the `ls` command - you should see a series of files and folders like cmvs, cmvs.tar.gz etc). Then, 

`cp -R /tmp/ images`  

> **important** do not have spaces in any file names or folder names or special characters. It just makes life easier. Here's a handy command to strip everything out:

> `for f in *; do mv "$f" "$(sed 's/[^0-9A-Za-z_.]/_/g' <<< "$f")"; done`

ALTERNATIVELY, what if you had drone footage of an archaeological site and you wanted to build the model from that? You'd follow [Ryan's workflow](http://ryanfb.github.io/etc/2014/10/22/drone_photogrammetry_workflow.html):

Make a new directory for the video you're going to download:

`$ mkdir redchurch` and then `cd redchurch`.

Get the footage from youtube with  `$ youtube-dl 'https://www.youtube.com/watch?v=3v-wvbNiZGY'` ie, slot the URL of a video you're interested in within ' after the youtube-dl command. That particular video downloads a video with a very long name. Let's rename it:

`$ mv 'The Red Church  Dating to the late 5thearly 6th century-3v-wvbNiZGY.mp4' redchurch.mp4`

Then, slice it into stills with avconv:

`$ avconv -i redchurch.mp4 -r 1/1 -qscale:v 1 redchurch_%08d.jpg`

(nb the _%08d - this is a pattern for naming the individual images).

Right, now let's go back up to our home directory with `cd ~`. (Note if you wanted to make these images out of the virtual machine and onto your host machine, you'd copy them to your `tmp` folder).

### Generate a point cloud

So, you now have a folder called `images` if you dropped them in, or `redchurch` if you extracted stills from the redchurch video. In the command below, `VisualSFM` calls the VSFM program, `sfm+pairs+pmvs` describes the commands to apply to the images in the `~/redchurch` folder and `redchurch.nvm` and `@8` specifies the output (see [Ryan's post](http://ryanfb.github.io/etc/2014/10/22/drone_photogrammetry_workflow.html) for details); the `@8` tells VSFM to match only against 8 frames either side of the current image; if you're using images you took yourself, you can drop this.


`$ VisualSFM sfm+pairs+pmvs ~/redchurch redchurch.nvm @8`

That command runs the entire process. Depending on the complexity of the images or video stills you've used, it can take hours to do all the processing. 

+ 'segmentation error'

> Boot2docker:

You might get a 'segmentation error' right at the start. What gives? It could be a memory issue. On the mac, use the 'go to' folder command in Finder to go `/users/[user]/.boot2docker` then make a new file there (with no extension) called `profile`. Put something like this in, as is appropriate for your system:

```
#disk image size in MB
DiskSize = 20000
 
# VM memory size in MB
Memory = 7168
```

> Docker-tools, Kitematic etc:

Find the `config.json` file inside the `.docker` folder on your machine (ie, `/users/[user]/.docker/machine/machines/default/config.json`

Inside that is a setting for memory. Open it in a text editor, ramp up the memory (as much as you've got) in mb, save. Then you need to [restart the virtual machine](https://docs.docker.com/machine/reference/restart/). This should do the trick. It didn't seem to do it for me, until at one point I started the Kitematic gui, and was rewarded with a 'building vm'.

[WINDOWS?]

So, make sure your images or that video are safe on your host machine somewhere. Exit your docker container and restart docker and the vsfm container. You can then drop your images back in.

### get your materials out

VSFM will create a number of .ply files; type `ls` to see them all. Also, there will be a folder like `redchurch.nvm.cmvs`. Copy the .ply files to the `tmp` folder and then on your host machine, copy them somewhere else that's safe. We'll zip up the folder too using the 'tar' command, which follows this pattern: `tar -czvf myarchive.tgz mydirectory/` eg:

`tar -czvf redchurch.nvm.cmvs.tgz redchurch.nvm.cmvs/`

Copy the `.tgz` archive file to your `tmp` folder and then move it somewhere safe on your host machine (the same place where you put the `.ply` files). Once you've got it safe on your machine, unzip it (or untar it).

![Imgur](http://i.imgur.com/M6b3xPl.png)

### Generate the model

Open Meshlab. At this point, you can follow along with [Ryan's post](http://ryanfb.github.io/etc/2014/10/22/drone_photogrammetry_workflow.html) which explains what each command does and why; for handy reference's sake I've listed them in order below. In essence, we ompute a mesh from the point cloud, clean up the mesh, then texture it with the images from the video:

1. in MeshLab use File→Open project… to open the bundle.rd.out file from one of the models reconstructed by VisualSFM. This will be in e.g. redchurch.nvm.cmvs/00/bundle.rd.out. MeshLab will then prompt you for an image list file which should be list.txt in the same directory. 
2. Next use File→Import Mesh… to open the corresponding .ply file in the top-level directory, e.g. redchurch-output.0.ply. 
3. Click the “eye” icon next to the “model” layer in the layer dialog on the right to hide it, then select the .ply layer. 
4. Run Filters→Point Set→Surface Reconstruction: Poisson, which will compute a mesh - do not worry about the crazy huge bubble this makes; we will fix this.
5. Hide your original .ply point cloud layer (click the 'eye' icon in the layer dialog), then make sure the Poisson mesh layer is selected again.
6. Use Filters→Selection→Select Faces with edges longer than… to select the extraneous huge bubble
7. Use Filters→Selection→Delete Selected Faces and Vertices to pare away the bubble.
8. You may still have some stray isolated blobs or polygons floating around in the model that you want to clean up. Use Filters→Cleaning and Repairing→Remove Isolated pieces (wrt Diameter) and/or Remove Isolated pieces (wrt Face Num.). 
9. Optional: If there are now holes left over in the model that you’d like filled before you apply the texture map from your images, you can use the interactive hole fill tool (Edit→Fill Hole) or the non-interactive filter under Filters→Remeshing, Simplification and Reconstruction→Close Holes.
10. Use Filters→Selection→Select non Manifold Edges, hit Apply, 
11. Use Filters→Selection→Delete Selected Faces and Vertices to remove any non-manifold faces.
12. Use Filters→Texture→Parameterization + texturing from registered rasters 

You now have a textured mesh. Use File→Export Mesh As…, select Alias Wavefront OBJ. You can now use this model for AR, for sharing via Sketchfab or p3d.in, for printing, etc.

If your some reason your model is too large, you can resize your texture in any image editor (use multiples of 1024 to go up, or divide down, right? 256-512-1024-2048 etc), or use Filters→Remeshing, Simplification and Reconstruction→Quadric Edge Collapse Decimation (with texture) to simplify your model and re-export, experimenting until you can fit it under the limit.
