## Simple Geolocation with Mixare

In the first dawn of smart-phone enabled AR, when every SDK was free, one of the go-to applications was geolocation with a radar heads-up display. Remember Gowalla?

It's still a handy tool to have however. In this tutorial, we'll add our own data to [Mixare](http://www.mixare.org/). You can install Mixare on your ios or android phone from that link. If you want to see how to build it for yourself, [this tutorial will see you through](https://sashageekette.wordpress.com/2012/12/02/getting-started-with-mixare-on-eclipse/)(it's a bit out of date in that Google wants everyone to build using their own programme rather than eclipse, but you can still do the build yourself following that tutorial; I found that some of the later steps (12 onwards) were not necessary).

Go ahead and install Mixare on your device. Then, fire it up. Its default grabs points of interest from Wikipedia within 20 km of you- you can see them if you hold your device up level with your head. Click on the options button - your options include 'data source', 'list view', 'map view', zoom level', 'search'. 

Click on data source. By default, it's grabbing Wikipedia from [Geonames.org](http://www.geonames.org/export/wikipedia-webservice.html), an old version of Twitter's search (which, if you were building from scratch, you'd want to update), OSM, and a page from Mixare.org itself.

Frankly, it's amazing after three years that all of these aren't borked - the Wikipedia search is the only one still working. But that's ok, because what we want is hidden under the options button on this page of resources: "Add data source".

On this page, you have:
```
Name

Url

Data source

Display as
```

Before we add anything here, let's quickly build a new page somewhere on the internet that our Mixare can find. I keep a kind of 'scratch pad' repository on github, with a gh-pages branch. I create a new page there, and enter the following:

```
{
    "status": "OK",
    "num_results": 3,
    "results": [
        {
            "id": "2827",
            "lat": "46.43893",
            "lng": "11.21706",
            "elevation": "1737",
            "title": "Penegal",
            "distance": "9.756",
            "has_detail_page": "1",
            "webpage": "http%3A%2F%2Fwww.suedtirolerland.it%2Fapi%2Fmap%2FgetMarkerTplM%2F%3Fmarker_id%3D2827%26project_id%3D15%26lang_id%3D9"
        },
        {
            "id": "2821",
            "lat": "46.49396",
            "lng": "11.2088",
            "elevation": "1865",
            "title": "Gantkofel",
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
