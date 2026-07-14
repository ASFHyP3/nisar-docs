---
short_title: Worldview 
---

# Exploring NISAR Data in Worldview

(worldview-overview)=
## Worldview

Worldview application for browsing, comparing, and animating visualizations

as a part of NASA's Global Imagery Browse Services (GIBS) service to provide visualizations of NASA Earth Science observations. 
GIBS strives to provide global, full-resolution visualizations of satellite data
Worldview is highly responsive, enables visual discovery of data 
Worldview application for browsing, comparing, and animating visualizations

### Adding NISAR Data

Click **Add Layers**, which will open up a window with all available datasets. Using the search bar, type in NISAR. Add your desired data layer(s). 

```{figure} ../assets/worldview-add-layers.png
:label: worldview-add-layers
:alt: Screenshot highlighting the **Add Layers** button and the search bar. 
:align: center

Search for NISAR products in Worldview by adding layers. 
```



```{figure} ../assets/worldview-add-nisar-layer.png
:label: worldview-add-nisar-layer
:alt: Screenshot displaying the add layers 
:align: center

Search for NISAR products in Worldview by adding layers. 
```

### Exploring NISAR Data
zooming/showing the fine resolution of the available imagery, show difference between 10, 20, 80 m resolution areas

Toggle between Geographic (EPSG 4326), Sea Ice Polar Stereographic North (EPSG:3413), and Antarctic Polar Stereographic (EPSG:3031).

* Timeslider 
    - stepping through a day at a time
    - above the increment date arrows, click on the *1 Day* text, which will allow for different increment. 
    - Custom option stepping through a cycle (12 days) at a time
    - The video icon creates an animation. Click the *1 Day* text to create the custom increment steps.



* comparison tool 
    - Between sar layer and an optical layer with clouds
    - nisar data between two dates
    - show how to update the comparison option

### Downloading Data

#### Open in Earthdata Search
* transitioning to Earthdata Search to download source data
Once a day and area of interested are selected, click the download data tab 
* Select the data layer to download (only one can be selected at a time)
* It can be helpful to click the *Set Area of Interest* checkbox, which will allow a rectangular AOI to be drawn on
* 

#### Load into a GIS
* loading into a GIS