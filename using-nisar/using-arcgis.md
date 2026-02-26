---
short_title: ArcGIS
---
# Using NISAR Data in ArcGIS

Support for the NISAR file format was added to ArcGIS Pro at version 3.4 (November 2024). Those using version 3.4.0 or newer are able to use NISAR products as they would any other HDF5 file. When using older versions of ArcGIS Pro, [refer to this documentation](https://www.earthdata.nasa.gov/learn/tutorials/work-nisar-sample-data#ArcEarly) for guidance. 

The [NISAR in GIS](https://www.earthdata.nasa.gov/learn/gis/storymaps/nisar-gis) tutorial provides step-by-step guidance for adding NISAR data to an ArcGIS Pro project, visualizing the data, and using standard and SAR-specific imagery and analysis tools, focusing on the [GCOV](gcov-product-overview) and [GUNW](gunw-product-overview) products. The [Spatial Subsetting for NISAR Data](https://storymaps.arcgis.com/stories/cac03522f82f420ab992316bb935a709) tutorial demonstrates workflows for subsetting NISAR products and transforming them to other data formats.

(arcgis-adding-nisar-data)=
## Adding NISAR Data

There are multiple options available for adding NISAR data to an ArcGIS Pro project. You can either use the [Add Multidimensional Raster](#arcgis-add-multidimensional-raster-tool) tool or simply [Drag and Drop](#arcgis-drag-and-drop) the HDF5 file from the table of contents. Step-by-step guidance for each method can be found in the [NISAR Data in ArcGIS Pro section of the NISAR in GIS](https://storymaps.arcgis.com/stories/c8f85d20b73c48fd8e89f8eef49bc60b#ref-n-4Bfbbu) tutorial. 

(arcgis-add-multidimensional-raster-tool)=
### Add Multidimensional Raster Tool

Using the [Add Multidimensional Raster](https://storymaps.arcgis.com/stories/c8f85d20b73c48fd8e89f8eef49bc60b#ref-n-diybcG) tool will provide more flexibility in how the variables are displayed. Variables can each be added as individual layers or combined into [multivariate](https://storymaps.arcgis.com/stories/c8f85d20b73c48fd8e89f8eef49bc60b#ref-n-JNuqoM) or [multiband](https://storymaps.arcgis.com/stories/c8f85d20b73c48fd8e89f8eef49bc60b#ref-n-I2ow3f) rasters. If you want to work with the variable in its native HDF5 format, this is the best option to use.

```{figure} ../assets/add-multidimensional-raster-tool.png
:name: add-multidimensional-raster-tool-screenshot
:alt: Screenshot highlighting the Add Multidimensional Raster tool in ArcGIS Pro
:align: left

Click the **Add Data** menu and select **Multidimensional Data** to add NISAR data in ArcGIS Pro.
```

To add complex-valued variables, such as wrapped interferograms, to an ArcGIS Pro project, you will need to use the Add Multidimensional Raster tool, and select **Multiband Raster** as the output format in order to access both the amplitude and phase components of the dataset. 

(arcgis-drag-and-drop)=
### Drag and Drop

You can simply drag and drop the entire file from the **Catalog** pane. This approach is most useful when you want to export individual variables to other data formats before working with them in ArcGIS Pro. 

The options to adjust visualizations, use imagery tools, or perform analysis are limited when you add the entire HDF5 file to the map. By default, the first variable in the file is displayed, and any changes to symbology are applied to all variables in the file. The approach does make it easy to use the **Subset** tool in the **Data Management** menu to save the variable as a different file type with a defined spatial extent.

```{figure} ../assets/arcgis-drag-and-drop.png
:name: arcgis-drag-and-drop-screenshot
:alt: Screenshot demonstrating drag-and-drop capabilities in ArcGIS Pro
:align: left

Using drag-and-drop functionality to add NISAR data in ArcGIS Pro.
```

Note that you will not be able to work with complex-valued variables, such as wrapped interferograms, using the drag-and-drop method. You will need to use the **Add Multidimensional Raster** tool, and select **Multiband Raster** as the layer format in order to access both the amplitude and phase components of the dataset.

(arcgis-visualizing-nisar-data)=
## Visualizing NISAR Data




(arcgis-transforming-nisar-data)=
## Transforming NISAR Data

(arcgis-subsetting-nisar-data)=
### Subsetting

(arcgis-converting-nisar-format)=
### Converting Format










