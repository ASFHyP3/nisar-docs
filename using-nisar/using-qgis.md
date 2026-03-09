---
short_title: QGIS
---
# Using NISAR Data in QGIS

NISAR Level 2-3 products are suitable for GIS analysis. Working with NISAR in [QGIS](https://qgis.org/), a free and open-source GIS. For a refresher on Level 2 and Level 3 data products, see @data-products-overview. 

The [Work with NISAR Sample Data](https://www.earthdata.nasa.gov/learn/tutorials/work-nisar-sample-data) tutorials provide a quick overview to work with NISAR data in QGIS. 

## Preparing NISAR Data for QGIS

QGIS does not natively support `.h5` files. To add NISAR data in QGIS, rename the file and change the `.h5` extension to `.nc`. For example, the file 
`NISAR_L2_PR_GCOV_010_164_A_035_4005_DHDH_A_20260120T134235_20260120T134312_X05010_N_F_J_001.h5` renamed as 
`NISAR_L2_PR_GCOV_010_164_A_035_4005_DHDH_A_20260120T134235_20260120T134312_X05010_N_F_J_001.nc`
would be able to be opened in QGIS. 

Alternatively, to work directly with `.h5` data, install the [QGIS NASA Earthdata plugin](https://github.com/opengeos/qgis-nasa-earthdata-plugin). 

(qgis-adding-nisar-data)=
## Adding NISAR Data
Add data to QGIS using the **Open Data Source Manger** button or shortcut. Select the **Raster** data type and add the desired file to the project. 

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
After loading data into QGIS, the symbology needs to be adjusted to visualize the data in a meaningful way. 

For GCOV products, the colorbar needs to be adjusted to a smaller range of values in order to highlight the features in the scene. Right-click on the layer in the **Layers** Panel and select **Properties** to adjust the symbology, as shown in @qgis-adjust-colorbar. Note that co-polarized returns are generally higher than cross-polarized returns, so the colorbar minimum and maximums might need to be different for the two different polarizations. Adjusting minimum and maximum values might take a bit of trial and error to highlight interesting features for each scene. 

```{figure} ../assets/qgis-adjust-colorbar.png
:name: qgis-adjust-colorbar
:alt: Screenshot showing the **Symbology** for a NISAR GCOV data layer 
:align: left

Right-click on the data layer in the **Layers** panel and select "Properties" to open up the Layer Properties window. Select the **Symbology** tab to adjust the Color Gradient minimum and maximum to appropriate values for the data layer. 
```

(qgis-transforming-nisar-data)=
## Transforming NISAR Data

(qgis-subsetting-nisar-data)=
### Subsetting

(qgis-converting-nisar-format)=
### Converting Format
how to export imagery to different file formats



