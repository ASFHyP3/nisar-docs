---
short_title: Worldview 
---

# Exploring NISAR Data in Worldview

(worldview-overview)=
## Worldview

[NASA Worldview](https://worldview.earthdata.nasa.gov/) is a user-friendly visualization tool that enables interactive browsing and animation of over 1,200 satellite data products. Imagery in Worldviews is powered by NASA's Global Imagery Browse Services (GIBS) service and delivers  global, full-resolution visualizations of satellite imagery.
 
(nisar-in-worldview)=
## NISAR Data in Worldview
Where multiple frequencies are available, the higher-resolution frequency is displayed. Regardless of the original source resolution, all products are resampled to 15.5-m pixel spacing in this visualization.
zooming/showing the fine resolution of the available imagery, show difference between 10, 20, 80 m resolution areas

### NISAR GCOV 
Currently, only NISAR [Level-2 Geocoded Covariance (GCOV)](#gcov-product-overview) products are available in Worldview. GCOV imagery is displayed using a false-color RGB decomposition to facilitate more intuitive visual interpretation of SAR backscatter data.

For acquisitions containing multiple polarimetric channels (dual-pol or quad-pol), visualization combines co-polarized backscatter (HH or VV) in the red and blue channels with cross-polarized backscatter (HV or VH) in the green channel. In this false-color scale, calm water, dry sand, and frozen ground appear blue, vegetated areas appear green, and urban and/or sparsely vegetated areas appear orange or yellow.

Single-polarization acquisitions, primarily collected in polar regions or over open ocean, are also colorized. With only one polarization channel available, however, the visualization provides less information than dual-pol or quad-pol composites. The color bar progresses from blue to green to orange to yellow, representing co-polarized backscatter values from low to high. In this presentation, water or dry soil still generally appears blue, and urban areas still typically appear yellow. However, vegetated areas may exhibit a different green/orange color than in the dual-pol RGB decomposition for the same area. Wet snow may appear very yellow, while drier snow is generally greener or bluer.


A comparison of the multipolametric and single-polarization color bars can be seen in (@worldview-colorbars). 

```{figure} ../assets/worldview-colorbars.png
:label: worldview-colorbars
:alt: Comparison of multipolarimetric and single-polarization color bars used in Worldview.  
:align: center

Color bars used in multipolarmetric and single-polarization imagery visualization for NISAR GCOV products in Worldview. 
```

Note that different land cover types may appear similar to each other in this visualization. Comparing this visualization with other imagery in Worldview may help when interpreting NISAR GOV data.  


## Using NISAR Data in Worldview

### Adding NISAR Data 

To add NISAR GCOV data, click on the **Add Layers** in the Layers tab, which will open up a window with all available datasets. Using the search bar, type **NISAR**, which will return a list of available layers associated with the NISAR mission.

 Note that SAR data layers are currently only searchable and visible in Geographic (EPSG 4326) projection. 

```{figure} ../assets/worldview-add-layers.png
:label: worldview-add-layers
:alt: Screenshot highlighting the **Add Layers** button and the search bar. 
:align: center

Search for NISAR products in Worldview by adding layers. 
```

Click on the data type you want to add. You can either select the checkbox next to the data layer in the results panel or the **Add Layer** button in the layer explanation panel.  

```{figure} ../assets/worldview-add-nisar-layer.png
:label: worldview-add-nisar-layer
:alt: Screenshot displaying the add layers 
:align: center

Search for NISAR products in Worldview by adding layers. 
```

Click the **X** on the top right of the pop-up to see the data listed on in the **Layers** panel. You can click the checkbox next to **Group Similar Layers** to help organize data layers, which can be helpful if comparing multiple data types.

Above the newly added data in the layer panel, you can toggle on/off **Place Labels**, **Coastlines/Borders/Roads** and **Coastlines** layers to help locate and orient yourself while exploring data. 

You can select your desired base layer in the base layer panel, which include default options with [Moderate Resolution Imaging Spectroradiometer (MODIS)](https://www.earthdata.nasa.gov/data/instruments/modis), [Visible Infrared Imaging Radiometer Suite (VIIRS)](https://www.earthdata.nasa.gov/data/instruments/viirs), and [Ocean Color Instrument (OCI)](https://www.earthdata.nasa.gov/data/instruments/oci) data. Learn more about the base layer options in this [Earthdata Forum post](https://forum.earthdata.nasa.gov/viewtopic.php?t=5228). For the purposes of this documentation, we will use MODIS v6.1.STD as our base layer.

### Exploring NISAR Data
#### Time Slider Tool
Once NISAR data are loaded into Worldview, you can search for available data temporally by using the time slider tool. As a default, the arrows step through time one day at a time. This can be helpful when determining when an area of interest has data acquisitions. 

Once a single day of data acquisition has been established, you can customize the time slider tool to step through time in a custom increment. Click the **1 Day** text above the time slider arrows, and select **Custom** from the pop-up menu.  By adjusting the Custom Interval Selector to 12 days, you can explore data acquired each cycle. This allows for quick access to multiple available acquisitions over an area of interest. 

To create an animation from available imagery, click the video recorder icon to the right of the arrows. Like the time slider tool, the animation tool allows for a custom increment of 12 days for stepping through time. Select a start date, end date, and how many frames pers second will be shown in the final animation. Then, click on the video recorder icon, which will open a pop-up to further refine the area of interest to be shown in the final animation. Here, you can select the resolution of the output GIF. Click the **Create GIF** button to create the GIF and save locally. 

#### Comparison Tool

Data can be compared across dates and datasets by using the clicking the **Start Comparison** button. A swipe bar will appear on the screen, allowing users to swipe between two different tabs of data. The mode of comparison can also be changed to opacity or with a "spy" tool. 

The date of the comparison layer can be changed either by moving the **A** and **B** arrows on the time slider or by clicking into the tab of each date and adjusting with the time slider arrows.

### Downloading Data

#### Open in Earthdata Search
* transitioning to Earthdata Search to download source data
Once a day and area of interested are selected, click the download data tab 
* Select the data layer to download (only one can be selected at a time)
* It can be helpful to click the *Set Area of Interest* checkbox, which will allow a rectangular AOI to be drawn on
* 

#### Load into a GIS
* loading into a GIS