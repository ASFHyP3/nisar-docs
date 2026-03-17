---
short_title: QGIS
---
# Using NISAR Data in QGIS

NISAR Level 2 and Level 3 products are suitable for direct use in GIS-based analysis, such as in [QGIS](https://qgis.org/), a free and open-source GIS. For a refresher on Level 2 and Level 3 NISAR data products, see @data-products-overview. 

To explore workflows for working with specific NISAR data types in QGIS, see the [Work with NISAR Sample Data](https://www.earthdata.nasa.gov/learn/tutorials/work-nisar-sample-data) tutorials. 

## Preparing NISAR Data for QGIS

QGIS does not natively support `.h5` files. To add NISAR data in QGIS, rename the file and change the `.h5` extension to `.nc`. For example, the file 
`NISAR_L2_PR_GCOV_010_164_A_035_4005_DHDH_A_20260120T134235_20260120T134312_X05010_N_F_J_001.h5` renamed as 
`NISAR_L2_PR_GCOV_010_164_A_035_4005_DHDH_A_20260120T134235_20260120T134312_X05010_N_F_J_001.nc`
would be able to be opened in QGIS. 

Alternatively, to work directly with `.h5` data, install the [QGIS NASA Earthdata plugin](https://github.com/opengeos/qgis-nasa-earthdata-plugin). 

### GSLC Products

QGIS does not natively handle complex numbers. The `gdal_translate` function will allos extraction of the amplitude and phase components into separate real components. Since the amplitude component contains the visual information, that will be the more useful component to view in QGIS. Run the following example to extract the amplitude from a GLSC file: 

`gdal_translate -of GTiff DERIVED_SUBDATASET:AMPLITUDE:NETCDF:/path/to/nisar.nc:/science/LSAR/GSLC/grids/frequencyA/HH amplitude.tif`

Now, `amplitude.tif` will be the file to load into QGIS. 

(qgis-adding-nisar-data)=
## Adding NISAR Data
Add data to QGIS using the **Open Data Source Manger** button or shortcut. Select the **Raster** data type and add the desired file to the project. 

```{figure} ../assets/qgis-add-data.png
:name: qgis-add-data
:alt: Screenshot highlighting the **Open Data Source Manger** button and the Raster data type to select when adding NISAR data. 
:align: left

Click on **Open Data Source Manger** and select the Raster data type to add NISAR data to QGIS. 
```
After clicking the **Add** button, another window will pop up with all the groups within the NISAR data file that can be added as individual layers. All groups are selected for addition as a default, but individual groups can be selected to avoid adding too much data to your project. For more information about the HDF Files and NISAR data groups, see @hdf5.  

```{figure} ../assets/qgis-select-layers.png
:name: qgis-select-layers
:alt: Screenshot highlighting the list of layers that pop up after adding NISAR data in QGIS
:align: left

Select the data layers to add in QGIS. All layers are selected as the default. 
```

(qgis-visualizing-nisar-data)=
## Visualizing NISAR Data
After loading data into QGIS, the symbology needs to be adjusted to visualize the data in a meaningful way. 

For GCOV products, the colorbar needs to be adjusted to a smaller range of values in order to highlight the features in the scene. Right-click on the layer in the **Layers** Panel and select **Properties** to adjust the symbology, as shown in @qgis-adjust-colorbar. Note that co-polarized returns are generally higher than cross-polarized returns, so the colorbar minimum and maximums might need to be different for the two different polarizations. The minimum and maximum values for the colorbar can be stretched by expanding `Min/Max Value Settings`. The `Mean +/- standard deviation` option is good starting point to visualizing GCOV data. 

```{figure} ../assets/qgis-adjust-colorbar.png
:name: qgis-adjust-colorbar
:alt: Screenshot showing the **Symbology** for a NISAR GCOV data layer to highlight the minimum and maximum values of the colorbar
:align: left

Right-click on the data layer in the **Layers** panel and select "Properties" to open up the Layer Properties window. Select the **Symbology** tab to customize stretch values for the gradient. 
```

NISAR data products will have a black and white (aka "Singleband grey") colorbar in QGIS as a default, but can be changed to a number of other color ramp options using the **Layer Properties** window. Right-click on the desired layer, and select **Properties** in the pop-up list. A variety of color ramps are available by changing the **Render Type** to "Singleband pseudocolor", such as the "Rocket" color ramp, as seen in @qgis-color-ramp. 

```{figure} ../assets/qgis-color-ramp.png
:name: qgis-color-ramp
:alt: Screenshot showing the **Symbology** for a NISAR GCOV data layer to highlight the option to adjust the color ramp 
:align: left

Right-click on the data layer in the **Layers** panel and select "Properties" to open up the Layer Properties window. Select the **Symbology** tab to change the color ramp of the scene
```

(qgis-transforming-nisar-data)=
## Transforming NISAR Data

(qgis-subsetting-nisar-data)=
### Subsetting

Subsetting raster data in QGIS can be done using the **Clip Raster by Extent** tool in QGIS, as highlighted in @qgis-raster-extraction. Navigate to **Raster** on the menu bar, then select **Extraction** to access this tool. 

```{figure} ../assets/qgis-raster-extraction.png
:name: qgis-raster-extraction
:alt: Screenshot showing how to access the **Clip Raster by Extent** raster tool 
:align: left

Select **Raster** from the menu bar, then select **Extraction** to open the **Clip Raster by Extent** raster tool. 
```

Ensure the correct layer is selected under **Input Layer** before subsetting. Then, either enter the minimum latitude and longitudes of the desired subset or select **Draw on Map Canvas** to draw a custom rectangle directly on the map. Note that you will have to click out of the **Raster Extraction** window to click and drag a region of interest. 

```{figure} ../assets/qgis-clip-extent.png
:name: qgis-clip-extent
:alt: Screenshot showing the **Clip Raster by Extent** raster tool 
:align: left

The **Clip Raster by Extent** tool has the option to draw a rectangle directly on the map or manually add the minimum latitude and longitudes to clip the data layer. Users can either save directly to a file or produce a temporary layer, which can later be saved. 
```

(qgis-converting-nisar-format)=
### Converting Format

Once a layer is ready to be exported, right-click on the layer and select **Export** then **Save As...** from the pop-up list. 

```{figure} ../assets/qgis-export.png
:name: qgis-export
:alt: Screenshot showing the **Export** option for a layer in QGIS
:align: left

Right-click on a layer and select the **Export** option from the pop-up list. 
```

A list of output data types will be available when selecting **Format**. Saving as a GeoTiff should be appropriate for most users. 

```{figure} ../assets/qgis-export-file.png
:name: qgis-export-file
:alt: Screenshot showing the options while exporting a layer to a data file
:align: left

Select the data format, a location and name for the file, and output projection for the file and press **OK** to save. 
```