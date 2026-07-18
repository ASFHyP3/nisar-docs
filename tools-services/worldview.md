---
short_title: Worldview 
---

# Exploring NISAR Data in Worldview

(worldview-overview)=
## Worldview
[NASA Worldview](https://worldview.earthdata.nasa.gov/) is a user-friendly visualization tool that enables interactive browsing and animation of over 1,200 satellite data products. Imagery in Worldviews is powered by NASA's Global Imagery Browse Services (GIBS) service and delivers  global, full-resolution visualizations of satellite imagery.

:::{important}NISAR GCOV Layer Available in Worldview
NISAR [Level-2 Geocoded Covariance (GCOV)](#gcov-product-overview) data can now be [visualized in Worldview](#worldview-nisar-gcov)! 
 :::

(worldview-nisar-gcov)=
## NISAR GCOV Layer

NISAR PROVISIONAL GCOV products are displayed as a daily mosaic, and users can click through each day to view the available data. GCOV imagery is displayed using a false-color [RGB decomposition](#worldview-rgb-decomp) to facilitate more intuitive visual interpretation of SAR backscatter data, and the daily mosaics are posted to a [pixel spacing](#worldview-pixel-spacing) of 15.5 meters.

(worldview-pixel-spacing)=
### Pixel Spacing

Where multiple frequencies are available, the higher-resolution frequency is included in the visualization (generally [Frequency A](#nisar-frequencies)). Regardless of the pixel spacing of the source GCOV dataset, however, all products are resampled to 15.5-m pixel spacing in the visualization layer.

% TODO zooming/showing the fine resolution of the available imagery, show difference between 10, 20, 80 m resolution areas

(worldview-rgb-decomp)=
### RGB Decomposition

For GCOV products containing multiple polarimetric channels (dual-pol or quad-pol), the visualization combines co-polarized backscatter (HH or VV) values in the red and blue channels with cross-polarized values (HV or VH) in the green channel. In this false-color scale, vegetated areas appear green; urban and/or sparsely vegetated areas appear orange or yellow; calm water, dry sand, and frozen ground all appear blue; and rough water may appear red. 

Single-polarization acquisitions, collected mostly in polar regions or over open ocean, are also colorized. Because they only have one available polarization, there is less information to integrate into the false-color visualization. The color bar passes from blue to green to orange to yellow, indicating co-polarized backscatter values from low to high. Calm water or dry soil is still generally blue, and urban areas are still generally yellow, but vegetated areas may exhibit a different color of green/orange than in the dual-pol RGB decomposition for the same area. Wet snow may appear very yellow, while drier snow is more green or blue.

Note that different land cover types may appear similar to each other in this visualization. Comparing this visualization with other imagery in Worldview may help when interpreting NISAR GCOV data.  

Refer to @worldview-colorbars for a comparison of the color bars for the dual-pol and single-pol RGB decomposition approaches. 

```{figure} ../assets/worldview-colorbars.png
:label: worldview-colorbars
:alt: Comparison of multipolarimetric and single-polarization color bars used in Worldview.  
:align: center

Color bars used in multipolarmetric and single-polarization imagery visualization for NISAR GCOV products in Worldview. 
```

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
:alt: Screenshot displaying the Add Layer button and checkbox.
:align: center

Add layers to the map using either the **Add Layer** button or by clicking the checkbox next to the desired data layer. 
```

Click the **X** on the top right of the pop-up to see the data listed on in the **Layers** panel. You can click the checkbox next to **Group Similar Layers** to help organize data layers, which can be helpful if comparing multiple data types.

Above the newly added data in the layer panel, you can toggle on/off **Place Labels**, **Coastlines/Borders/Roads** and **Coastlines** layers to help locate and orient yourself while exploring data. 

```{figure} ../assets/worldview-layers-panel.png
:label: worldview-layers-panel
:alt: Screenshot describing the layer panel options. 
:align: center

The layers panel allows for toggling on and off of each layer. This can be done by clicking on the eye icon. In this screenshot, all the reference layers are on, displaying place labels, borders, and coastlines. On the bottom of the panel, the **Group Similar Layers** checkbox is checked, which helps organize data layers. This can be helpful when comparing across multiple data types. 
```

You can select a desired base layer in the Base Layers menu, which include default options with [Moderate Resolution Imaging Spectroradiometer (MODIS)](https://www.earthdata.nasa.gov/data/instruments/modis), [Visible Infrared Imaging Radiometer Suite (VIIRS)](https://www.earthdata.nasa.gov/data/instruments/viirs), and [Ocean Color Instrument (OCI)](https://www.earthdata.nasa.gov/data/instruments/oci) data. Learn more about the base layer options in this [Earthdata Forum post](https://forum.earthdata.nasa.gov/viewtopic.php?t=5228). For the purposes of this documentation, we will use MODIS v6.1.STD as our base layer.

### Exploring NISAR Data

#### Time Slider Tool

Once NISAR data are loaded into Worldview, search for available data temporally by using the time slider tool. As a default, an arrow click steps through time one day at a time. This can be useful when determining when there are data acquisitions over an area of interest. 

Once a single day of data acquisition has been established, you can customize the time slider tool to step through time in a custom increment. Click the **1 Day** text above the time slider arrows, and select **Custom** from the pop-up menu.  By adjusting the Custom Interval Selector to 12 days, you can explore data acquired each cycle. This allows for quick access to multiple available acquisitions over an area of interest. 

```{figure} ../assets/worldview-customize-timestep.png
:label: worldview-customize-timestep
:alt: Screenshot illustrating adjusting the Custom Interval Selector to 12 Days. 
:align: center

Click on the the **1 Day** text above the time step arrows, then select **Custom** from the pop-up menu. Enter 12 days into the Custom Interval Selector to step through time 12 days/one NISAR cycle at a time. 
```

To create an animation from available imagery, click the video recorder icon to the right of the arrows. Like the time slider tool, the animation tool allows for a custom increment of 12 days for stepping through each NISAR cycle. Select a start date, end date, and how many frames pers second will be shown in the final animation. 

```{figure} ../assets/worldview-animate-timeseries.png
:label: worldview-animate-timeseries
:alt: Screenshot showing the placement and parameters in the animation tool.
:align: center

Click on the video recorder icon next to the time step arrows to animate a timeseries. A pop-up box will allow for further refinement of the time step, start and end date, and frames per second in the animation. Click on the video recorder icon circled in red to create the animated GIF. 
```

Click on the video recorder icon, which will open a pop-up to further refine the area of interest to be shown in the final animation. Here, you can select the resolution of the output GIF. Click the **Create GIF** button to create the GIF and save locally. 

```{figure} ../assets/worldview-save-animation-gif
:label: worldview-save-animation-gif
:alt: Screenshot describing how to put finishing touches on animation and save. 
:align: center

Adjust the rectangle over an area of interest to be animated. Select the output resolution for the final GIF and check the box next to **Include Date Stamps** to include date stamps on the final product. Finally, click **Create GIF** to create and save the animation. 
```

#### Comparison Tool

Data can be compared across dates and datasets by using the clicking the **Start Comparison** button. A swipe bar will appear on the screen, allowing users to swipe between two different tabs of data. The mode of comparison can also be changed to opacity or with a "spy" tool. 

```{figure} ../assets/worldview-start-comparison
:label: worldview-start-comparison
:alt: Screenshot highlighting the Start Comparison button. 
:align: center

Select the **Start Comparison** button to enter comparison mode. 
```

The date of the comparison layer can be changed either by moving the **A** and **B** arrows on the time slider or by clicking into the **A** and **B** tabs in the **Layers** panel. Within each comparison tab, you can toggle layers on and off, which can be particularly useful when comparing across datasets.
 
```{figure} ../assets/worldview-adjust-comparison
:label: worldview-start-comparison
:alt: Screenshot highlighting the tabs and time slider arrows to adjust dates in comparison mode. 
:align: center

Adjust the date of the comparison sides by moving the time slider arrows of **A** or **B**, circled in red, or by clicking into the **A** or **B** tabs highlighted on the Layers panel. 
```

Note that you cannot animate nor download data in comparison mode. Exit comparison mode by clicking the **Exit Comparison** button on the bottom of the **Layers** panel. 

```{figure} ../assets/worldview-exit-comparison
:label: worldview-start-comparison
:alt: Screenshot emphasizing the **Exit Comparison** button.  
:align: center

Exit Comparison mode by clicking the **Exit Comparison** button on the bottom of the **Layers** panel. 
```

### Downloading Data

#### Open in Earthdata Search
Once a day and area have been selected, and you ready to download data, click on the **Data** tab. Select the layer to download from. Note that only one data layer can be downloaded at a time. It can be helpful to click the **Set Area of Interest** checkbox, which will allow a rectangular AOI to be drawn on and passed to Earthdata Search. Click on **Download Via Earthdata Search** to open a new window with all the parameters from Worldview set. For more information on downloading data using Earthdata Search, refer to @download-nisar-data-earthdata-search.

```{figure} ../assets/worldview-download-data
:label: worldview-start-comparison
:alt: Screenshot dispalying the Data download parameters.  
:align: center

Download data by clicking the **Data** tab on the **Layers** panel. Select the data layer you want download, click the checkmark to set an area of interst, and click **Download Via Earthdata Search**. This will open Earthdata Search with all the parameters selected. 
```

#### Load into a GIS
NISAR data can also be loaded into a GIS as a WMS or WMTS service, with WMS being the default. In your GIS, select **Add Layer**, then set the data type to WMS/WMTS.

```{figure} ../assets/worldview-add-new-wms
:label: worldview-add-new-wms
:alt: Screenshot of a QGIS window ready to load the GIBS WMS service.   
:align: center

Add a new data layer to your GIS with the data type WMS/WMTS. 
```

For data in EPSG:4326 projection, use the URL 'https://uat.gibs.earthdata.nasa.gov/wms/epsg4326/best/wms.cgi' and add to your project. This will provide access to all imagery available, so either search for the desired layer or select the desired layer in the browser under RTC SAR Backscatter. Since this data collection is temporally dependent, you will need to use the Temporal Controller tool in QGIS or the Time Slider tool in ArcGIS Pro to explore the data through time.

For more information, see the [GIBS Wiki Page]( https://wiki.earthdata.nasa.gov/display/GIBS/).

```{figure} ../assets/worldview-add-wms-connection
:label: worldview-add-new-wms
:alt: Screenshot of a QGIS window ready to load the GIBS WMS service.   
:align: center

Use the URL 'https://uat.gibs.earthdata.nasa.gov/wms/epsg4326/best/wms.cgi' in the WMS/WMTS connection and press OK to add to your GIS. 
```