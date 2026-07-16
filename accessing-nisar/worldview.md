---
short_title: Worldview 
---

# Exploring NISAR Data in Worldview

(worldview-overview)=
## Worldview

[NASA Worldview](https://worldview.earthdata.nasa.gov/) is a user-friendly visualization tool that enables interactive browsing and animation of over 1,200 satellite data products. Imagery in Worldviews is powered by NASA's Global Imagery Browse Services (GIBS) service and delivers  global, full-resolution visualizations of satellite imagery.
 
## NISAR Data in Worldview

NISAR [Level-2 Geocoded Covariance (GCOV)](#gcov-product-overview) products are available in Worldview. GCOV imagery is displayed using a false-color red, green, and blue (RGB) decomposition to facilitate more intuitive visual interpretation of the SAR backscatter data. Visualization is applied to acquisitions with multiple polarmetric channels (dual-pol or quad-pol) combines co-polarized backscatter(HH or VV) values in the red and blue channels with cross-polarized cross-polarized values (HV or VH) in the green channel. In this false-color scale, vegetated areas appear green; urban and/or sparsely vegetated areas appear orange or yellow; calm water, dry sand, and frozen ground appears blue; and rough water may appear red.

Single-polarization acquisitions, collected mostly in polar regions or over open ocean, are also colorized. Because they only have one available polarization, the false-color approach provides less information. The color bar passes from blue to green to orange to yellow, indicating co-polarized backscatter values from low to high. Water or dry soil is still generally blue, and urban areas are still generally yellow, but vegetated areas may exhibit a different color of green/orange than in the dual-pol RGB decomposition for the same area. Wet snow may appear very yellow, while drier snow is more green or blue.

Note that different landcover types may appear similar to each other in this visualization. Consider referencing other imagery when interpreting this visualization.

### Adding NISAR Data 

To add NISAR GCOV data, click **Add Layers**, which will open up a window with all available datasets. Using the search bar, type in NISAR. Add your desired data layer(s). 

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