---
short_title: QGIS
---
# Using NISAR Data in QGIS

NISAR products Level 2-3 are suitable for GIS analysis. Working with NISAR in [QGIS](https://qgis.org/), a free and open-source GIS. 

The [Work with NISAR Sample Data](https://www.earthdata.nasa.gov/learn/tutorials/work-nisar-sample-data) tutorials provide a quick overview to work with NISAR data in QGIS. 

## Preparing NISAR Data for QGIS

QGIS does not natively support `.h5` files. To add NISAR data in QGIS, rename the file by changing the `.h5` extension to `.nc`. Alternatively, to work directly with `.h5` data, install the [QGIS NASA Earthdata plugin](https://github.com/opengeos/qgis-nasa-earthdata-plugin). 

(qgis-adding-nisar-data)=
## Adding NISAR Data
Add in data to QGIS using the **Open Data Source Manger** button or shortcut. Select the **Raster** data type and add the desired file to the project. 

```{figure} ../assets/qgis-add-data.png
:name: qgis-add-data
:alt: Screenshot highlighting the **Open Data Source Manger** button and the Raster data type to select when adding NISAR data. 
:align: left

Click on **Open Data Source Manger** and select the Raster data type to add NISAR data to QGIS. 
```
After clicking the **Add** button, another window will pop up with all the groups within the NISAR data file that can be be added as individual layers. All groups are selected for addition as a default, but individual groups can be selected to avoid adding too much data to your project. For more information about the HDF Files and NISAR data groups, see @hdf5.  
```{figure} ../assets/qgis-select-layers.png
:name: qgis-select-layers
:alt: Screenshot highlighting the list of layers that pop up after adding NISAR data in QGIS
:align: left

Select the data layers to add in QGIS. All layers are selected as the default. 
```

(qgis-visualizing-nisar-data)=
## Visualizing NISAR Data
how to render them pleasingly

```{figure} ../assets/qgis-adjust-colorbar.png
:name: qgis-adjust-colorbar
:alt: Screenshot showing the **Symbology** for a NISAR GCOV data layer 
:align: left

Right click on the data layer in the **Layers** panel and select "Properties" to open up the Layer Properties window. Select the **Symbology** tab to adjust the Color Gradient minimum and maximum to appropriate values for the data layer. 
```

(qgis-transforming-nisar-data)=
## Transforming NISAR Data

(qgis-subsetting-nisar-data)=
### Subsetting

(qgis-converting-nisar-format)=
### Converting Format
how to export imagery to different file formats



