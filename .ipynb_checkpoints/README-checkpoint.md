## Efficiently construct a 3d printable topographic relief with municipal features

***Jess's Tarrytown NY model notes***


Ilana, YuAng and I noticed a large chunk of Tarrytown's municipal footprint data is inexplicably missing or incorrect from common OSM CDNs and vector tile servers.

This data is unfortunately missing from the Nextzen tile servers as well, so we'll use Microsoft's  footprints [classified using public orthoimagery here](https://github.com/Microsoft/USBuildingFootprints).

We'll rely on tile data available via the Nextzen tile servers for roads and topography, and will interact with these servers with using Karim Naaji's [vectiler CLI](https://github.com/karimnaaji/vectiler).  

While this adds a few additional steps of data munging for this particular project, jumping between GIS software, scriptable tools, various spatial utilities and CAD software is an important and will inevitably be a skill students working in the DLA Makerspace become more comfortable with over time.  In this quick example, I am working *entirely* with free and open source software complied from source for my linux distribution.  While this ensures everything discussed here is available and repeatable by anyone anywhere on just about any operating system (and is just how I roll if left to my own devices), I understand this approach to GIS can feel daunting at first.  


Taking a look at Tarrytown at the resolution of the DEM data publicly available to us (level `15` using Google's map tile coordinates), the ROI is:

##### Upper left tile {x,y}:
**Google:** `9659/12274`
##### Upper left convex point:
**WSG84:** `-73.88305400`, `41.09591200`

##### Lower right tile:
**Google:** `9661/12278`  
##### Lower right convex point:
**WSG84:** `-73.85009500`, `41.05450200`

We can take a look at these tiles [superimposed over Terrytown's OSM default map here](https://www.maptiler.com/google-maps-coordinates-tile-bounds-projection/#13/-73.85/41.07).

Vectiler query:
```
# Builds 9659.12274.15.obj:
./vectiler --tilex 9659/9661 --tiley 12274/12278 --tilez 15 --terrain 1 --roads 1 --terrainExtrusionScale 1 --pedestal 1 --pedestalHeight -20
```


#####  Discreet software packages and projects compiled individually for this environment:

|Software|Version|
|-|-|
|protobuf|3.19.1|
|PROJ version|9.0.1|
|GDAL/OGR version|3.4.3|
|QGIS version |3.26.2-Buenos Aires|
|QGIS branch| Release 3.26|
|Qt version|5.12.8|
|GEOS version|3.10.2-CAPI-1.16.0|
|QScintilla2 version|2.11.2|
|Python version|3.8.10|
|Operating System|Ubuntu 20.04.5 LTS|
|Desktop Environment|Budgie GTK+|
|Windowing system|X11|
