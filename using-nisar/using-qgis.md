---
short_title: QGIS
---
# Using NISAR Data in QGIS
call out nisar products that are suitable for GIS analysis (L2-L3)

The [Work with NISAR Sample Data] tutorials demonstrate how to use NISAR data in QGIS 

## Preparing NISAR Data for QGIS

Support for the NISAR file format was added to ArcGIS Pro at version 3.4 (November 2024). Those using version 3.4.0 or newer are able to use NISAR products as they would any other HDF5 file. When using older versions of ArcGIS Pro, refer to this documentation for guidance.
QGIS does not support .h5 files 
rename the file by replacing the `.h5` extension with `.nc`. To work with `h5` data in QGIS, there is a [QGIS NASA Earthdata plugin](https://github.com/opengeos/qgis-nasa-earthdata-plugin)

(qgis-adding-nisar-data)=
## Adding NISAR Data
how to load these into QGIS, including selecting data layers

```{figure} ../assets/qgis-add-data.png
:name: qgis-add-data
:alt: Screenshot highlighting the **Open Data Source Manger** button and the Raster data type to select when adding NISAR data. 
:align: left

Click on **Open Data Source Manger** and select the Raster data type to add NISAR data to QGIS. 
```

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



