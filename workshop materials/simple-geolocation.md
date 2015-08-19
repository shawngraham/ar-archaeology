## Simple Geolocation with Mixare

In the first dawn of smart-phone enabled AR, when every SDK was free, one of the go-to applications was geolocation with a radar heads-up display. I think that's still a handy tool to have, with useful archaeological dimensions (load up POIs from your GIS, get that heads-up bearing rather than studying a map; public archaeology where one is guided to look at the landscape through archaeological eyes, etc). 

In this tutorial, we'll add our own data to [Mixare](http://www.mixare.org/). Follow that link to install Mixare on your ios or android phone. Mixare is open source. If you want to build it for yourself, [this tutorial will see you through](https://sashageekette.wordpress.com/2012/12/02/getting-started-with-mixare-on-eclipse/). The tutorial is a bit out of date in that Google wants everyone to build using their own android development programme rather than the eclipse environment, but you can still do the build yourself following that tutorial; I found that some of the later steps (12 onwards) were not necessary. [Here are my notes on building Mixare from source](mixare-from-source.md). As an introduction into Android app-building, it's quite useful too. If Mixare ever gets pulled from the app store, being able to build it ourselves (or use its pieces in other applications) will be useful.

Go ahead and install Mixare on your device. Then, fire it up. Its default settings grab points of interest from Wikipedia within 20 km of you- you can see them if you hold your device up level with your head. Click on the options button - your options include 'data source', 'list view', 'map view', zoom level', 'search'. 

Click on data source. By default, it's grabbing Wikipedia from [Geonames.org](http://www.geonames.org/export/wikipedia-webservice.html), an old version of Twitter's search (which, if you were building from scratch, you'd want to update since the old api is no longer used), OSM, and a (broken) page from Mixare.org itself.

Frankly, it's amazing after three years that all of these aren't borked - the Wikipedia search is the only one still working. But that's ok, because what we want is hidden under the options button on this page of resources: "Add data source".

On this page, you have:
```
Name

Url

Data source

Display as
```

Before we add anything here, let's quickly build a new page somewhere on the internet that our Mixare can find. As it happens, github pages don't work for this nor does dropox. [My own domain does though](http://graeworks.net/mixdata.json) I keep a kind of 'scratch pad directory' on my own domain. I create a new page in my text editor of choice, with the following:

```
{
    "status": "OK",
    "num_results": 3,
    "results": [
        {
            "id": "2827",
            "lat": "45.3875812",
            "lng": "-75.6960202",
            "elevation": "120",
            "title": "Carleton University",
            "distance": "9.756",
            "has_detail_page": "1",
            "webpage": "http://carleton.ca"
        },
        {
            "id": "2821",
            "lat": "45.2853629",
            "lng": "-75.7218656",
            "elevation": "1865",
            "title": "Tim Horton's",
            "distance": "9.771",
            "has_detail_page": "0",
            "webpage": ""
        },
        {
            "id": "2829",
            "lat": "46.3591",
            "lng": "11.1921",
            "elevation": "2116",
            "title": "Roen",
            "distance": "17.545",
            "has_detail_page": "1",
            "webpage": "http%3A%2F%2Fwww.suedtirolerland.it%2Fapi%2Fmap%2FgetMarkerTplM%2F%3Fmarker_id%3D2829%26project_id%3D15%26lang_id%3D9"
        }
    ]
}
```
...which I then ftp to my domain.

So - you need to have a unique ID for each of your points. `Lat` and `lng` in decimal degrees. `Elevation` - this doesn't seem to be used, nor does `distance` - you can ignore them. *IF* you want your POI to link to a webpage, then `has_detail_page` has to be set to 1, and the URL gets put in the `webpage` bit. Make sure to validate your JSON with [JSONLint](http://jsonlint.com/). It is possible to modify the source code so that you can have different kinds of icons for different kinds of POIs, etc- [see this disscussion](https://github.com/abduegal/mixare/wiki/Data-handler).

## Add to your Mixare

So back in your app - at the add data page, simply fill in the fields. Select 'mixare' as the data source. Hit the back button until you're back at your camera with radar. Ta da! 

## Going further

I'm a fan of bricolage - sometimes it's not necessary to build a *complete* do-everything app, but rather, use a series of small tools within a larger narrative framework.  Imagine that you took my ['diary in the attic'](https://www.dropbox.com/s/y1cu6ee6j77of87/nilediary.pdf?dl=0) pages, and hid them around the grounds of a stately old house. Then, you could use Mixare to provide POIs relatively close to where the pages are hiding. The player could use Mixare to find the locations, and then the [Android SpectralScope](https://www.dropbox.com/s/prgpqdoia3ugbdk/nilediary3.apk?dl=0) to find the ghosts in the pages...  "Imagine, for instance, that you are a ghost hunter, equipped with the latest range-finding and dimensional-inspecting apps... find the diary. Peer into the dimensional rift. Uncover the truth..."

You could also tie your POIs not to webpages, but to audio sources, or video files, or Twine files. You could make the link [open an app on the user's phone](http://stackoverflow.com/questions/16153863/html-link-to-launch-an-app-if-installed-or-go-to-a-website-if-not) (although that may or may not be a good idea).

You could probably also merge aspects of the Mixare SDK with the Vuforia SDK to put both kinds of functionality (image/object based tracking with geolocation) into a single app - although this is where I think the philosophy of one small tool that does what you need it to do comes to the fore.
