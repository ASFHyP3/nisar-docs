---
short_title: Vertex
---

# Finding NISAR Data with Vertex

{button}`Search for all NISAR Data Products<https://search.asf.alaska.edu/#/?dataset=NISAR&prodConfig=PR>`

(vertex-overview)=

## Vertex

[Vertex](https://search.asf.alaska.edu/#/?dataset=NISAR&prodConfig=PR) is ASF's web-based data search interface. It is optimized for searching NASA's SAR holdings, including NISAR. Because search parameters for SAR differ from other types of Earth observation data, it can be helpful to use a search platform tailored specifically for SAR datasets.

## 1. Search for NISAR data

Navigate to [Vertex](https://search.asf.alaska.edu/#/?dataset=NISAR&prodConfig=PR) and set the **Search Type** to `Geographic Search` and select `NISAR` from the **Dataset** menu. Press **Search** to explore search results.

```{figure} ../assets/vertex-dataset-selection.png
:label: vertex-dataset-selection
:alt: Image depicting the option to select NISAR from the Dataset options.
:align: center

Click on the **Dataset** field and select `NISAR` from the drop-down menu to search for NISAR products.
```

(vertex-antarctica)=

### Antarctica

NISAR has great coverage over Antarctica. Users interested in this area may find it helpful to use the **Antarctic map projection** in Vertex, which renders acquisition footprints at high latitudes much better than the default global view.

```{figure} ../assets/vertex-antarctic-map.png
:label: vertex-antarctic-map-view
:alt: Image illustrating how to use the Antarctic Map View in Vertex.
:align: center

Click the **Antarctic map projection** button in the **Map View** section of the Vertex map toolbar to set the map to a south polar stereographic projection.
```

Note that the [**Layers**](https://docs.asf.alaska.edu/vertex/manual/#other-vertex-options) button in the toolbar is not available when using a polar map view, as only one basemap layer is available for each polar view.

## 2. Filter for desired products

(vertex-geographic-extent)=

### Geographic Extent

To search for a specific geographic region, click on the left-most **Area of Interest** button to choose to draw a point, line, polygon, box, circle, or to upload a geospatial file.

Select a drawing mode to draw a region of interest on the map, then press **Search** to update the search results for the new region of interest.

```{figure} ../assets/vertex-geographic-search.png
:label: vertex-geographic-search
:alt: Screenshot of Vertex highlighting the Geographic Search option to draw a region of interest to search for products.
:align: center

Choose a shape and draw an area of interest for a geographic search.
```

_Take care when drawing an AOI while in the [Antarctic Map View](#vertex-antarctica). Rectangular AOIs drawn over the South Pole can sometimes be translated into an unexpected polygon, resulting in either no results or many more (orders of magnitude) results than expected. If this occurs, try drawing an AOI to one side or the other of the pole._

### Date Range

To search for products in a specific date range, click the **Filters** button to open the **Search Filters** panel and specify a start and end date in the **Date Filters** section. On larger screens, the date range filter will be displayed directly in the top search bar.

```{figure} ../assets/vertex-date-filters.png
:label: vertex-date-filters
:alt: Screenshot displaying the date filters option.
:align: center

Click the **Filters** button to open the **Search Filters** panel and enter a date range.
```

### NISAR Filters

NISAR-specific filters are available to more precisely search for NISAR data products. Refer to the [Vertex Getting Started User Guide](https://docs.asf.alaska.edu/vertex/manual/#product-filters) for a comprehensive list of filters and search options.

```{figure} ../assets/vertex-nisar-filters.png
:label: vertex-nisar-filters
:alt: Screenshot displaying the NISAR-specific filters in Vertex.
:align: center

NISAR-specific filters in Vertex.
```

**Product Filters** are listed in @tbl:vertex-product-filters. Science Products are organized by product level, and multiple selections are allowed. For a complete list of NISAR products, including detailed descriptions and specifications, refer to @data-products-overview.

:::{table} Product Filters for NISAR Products
:label: tbl:vertex-product-filters

| Product Filters       | Description                                                                                                                                |
| --------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Science Product       | Specific product type, grouped by product level. Multiple selections allowed.                                                              |
| Product Configuration | Specific processing pipelines, including Production and [Urgent Response](#urgent-response-product-overview). Multiple selections allowed. |
| Data Maturity         | Specific product validation/calibration status between beta and provisional data. Multiple selections allowed.                             |

:::

**Observational Filters** allow users to refine search results by polarization, direction, instrument, frame coverage, and/or range bandwidth, as described in @tbl:vertex-observational-filters. For information about NISAR bands, frequencies, and polarization, see @nisar-instrumentation. Note that only L-band data are available through Vertex. S-band data are provided through [ISRO's Bhoonidhi](https://bhoonidhi.nrsc.gov.in/bhoonidhi/home.html).

:::{table} Observational Filters for NISAR Products
:label: tbl:vertex-observational-filters

| Observational Filters  | Description                                                                                   |
| ---------------------- | --------------------------------------------------------------------------------------------- |
| Main Band Polarization | Frequency A polarizations. Multiple selections allowed.                                       |
| Side Band Polarization | Frequency B polarizations. Multiple selections allowed.                                       |
| Direction              | Orbit direction (ascending, descending).                                                      |
| Instrument             | Only L-Band SAR is currently available.                                                       |
| Frame Coverage         | Full or Partial frame coverage.                                                               |
| Range Bandwidth        | Range bandwidth in MHz. Multiple selections allowed.                                          |
| Joint Observation Only | Toggle on to restrict search to acquisitions with simultaneous L- and S-Band data collection. |

:::

Users can also search by **Track and Frame**. Note that "Track" is also known as "Path" or "Relative Orbit" for other satellite missions, such as Sentinel-1. Searching for a specific track and frame will return scenes that align consistently over a specific area. The NISAR track-frame map for available NISAR data is available on the [NISAR Mission website](https://science.nasa.gov/mission/nisar/data/).

## 3. Download data

Data are free and available to download through Vertex. Once the desired scene is selected, a list of files will appear on the right-hand side of the screen (or below the scene details on a narrow browser window). The HDF5 file, listed first, contains the science data and imagery. To learn more about HDF5 files, see @hdf5.

Under the Science Data dropdown menu, click the download icon circled in the figure to save to your computer. You will be prompted to sign in with your [Earthdata Login (EDL)](https://www.earthdata.nasa.gov/data/earthdata-login) account if you have not already.

```{figure} ../assets/vertex-download-files.png
:label: vertex-download-files
:alt: Screenshot of the list of files for a single GCOV product.
:align: center

All product files associated with a GCOV product. The HDF5 file, listed first, contains the science data and imagery, and can be downloaded directly by clicking the download icon, circled in red.
```

<!-- TODO: add section on download queue and bulk download options -->

[//]: # "(vertex-download-queue)="
[//]: # "### Download Queue"

(vertex-gdal-snippet-exporter)=

### GDAL Snippet Exporter

[GDAL](https://gdal.org/en/stable/) is a command line utility and library which enables transformation of geographic data. The GDAL snippet exporter allows generating GDAL commands to extract datasets, spatially subset, or reproject all geocoded (Level 1 and Level 2) NISAR HDF5 products without downloading the entire HDF5 file. This section focuses on the use of the Vertex GDAL Snippet Exporter, to learn more about the use of GDAL with NISAR data in general visit the [Nisar Data User Guide page on GDAL](#gdal-nisar).

#### Installing GDAL

To use commands generated by the snippet exporter you must install GDAL to be able to utilize the commands.

##### Windows

The recommended method of installing GDAL on windows is by installing [QGIS](https://qgis.org/) and utilizing the [OSGeo4W Shell](https://www.osgeo.org/projects/osgeo4w/).

##### Linux

Install GDAL using your distributions package manager. On Debian or Ubuntu systems this can be achieved by running the following command:

```{code} bash
sudo apt install gdal-bin
```

#### Configuring GDAL for use with Vertex

The Vertex GDAL snippet export generates CLI snippets which stream products directly from NASA's [Earthdata Cloud (EDC)](https://www.earthdata.nasa.gov/about/earthdata-cloud-evolution) without downloading them first. To do so, we must allow GDAL to authenticate to EDC by placing a `.netrc` file in the home directory of our compute environment containing our [Earthdata Login](#earthdata-login) credentials.

```{code-block} plaintext
:filename: ~/.netrc (Unix Systems) or C:\Users\<YOUR WINDOWS USERNAME> (Windows)

machine urs.earthdata.nasa.gov
    login <username>
    password <password>
```

#### Generating GDAL CLI snippets in Vertex

##### Simpled Dataset Extraction

Simple dataset extraction can be performed using the GDAL snippet dropdown. To open the GDAL snippet dropdown click the arrow button on any supported HDF5 file (GCOV, GOFF, GSLC, GUNW or SME2) in the scene file list.

```{figure} ../assets/vertex-gdal-dropdown
:label: vertex-gdal-dropdown
:alt: Screenshot displaying the icon to click to open the GDAL snippet dropdown.
:align: center
```

Then click on the terminal icon next to your desired dataset to copy the GDAL CLI snippet corresponding with that dataset.

```{figure} ../assets/vertex-gdal-dropdown-expanded
:label: vertex-gdal-dropdown
:alt: Screenshot displaying the GDAL snippet dropdown.
:align: center
```

##### Detailed GDAL Snippet Generation

Spatial subsetting, reprojection, and more can be achieved through the GDAL snippet exporter dialog. To open the GDAL snippet dialog click the tranformation icon on any supported HDF5 file in the scene file list.

```{figure} ../assets/vertex-gdal-dialog-button
:label: vertex-gdal-dropdown
:alt: Screenshot displaying the icon to click to open the GDAL snippet dialog.
:align: center
```

Then, select a dataset in the GDAL snippet dialog.

```{figure} ../assets/vertex-gdal-dialog-dataset
:label: vertex-gdal-dropdown
:alt: Screenshot displaying the datasets in the GDAL snippet dialog.
:align: center
```

To perform a spatial subsetting operation ensure you have an area of interest selected on the map view, then check the "Crop to current AOI" box. To perform reprojection enter a EPSG code (ie EPSG:3857) or WGS84 into the "Output Projection" box.

```{figure} ../assets/vertex-gdal-dialog options
:label: vertex-gdal-dropdown
:alt: Screenshot displaying the GDAL snippet dialog options.
:align: center
```

Once you have configured the output options copy the final outputted snippet by clicking the copy icon above the "GDAL shell command" code block.

```{figure} ../assets/vertex-gdal-dialog-copy
:label: vertex-gdal-dropdown
:alt: Screenshot displaying the icon to click to copy the GDAL command output in the GDAL snipet dialog.
:align: center
```

### Running GDAL Snippets

To run GDAL snippets on Windows open the OSGeo4W shell and paste the command into the shell. You may be asked if you are sure you want to paste your clipboard into the shell, click yes. Then hit enter to run the command.

To run GDAL snippets on Unix open your system shell or terminal, paste the command into the shell, and hit enter.

## Urgent Response Products

[Urgent Response](#urgent-response-product-overview) (UR) products can be found by setting the [Product Configuration](#tbl:vertex-product-filters) filter to `Urgent Response`. Refer to [Urgent Response: Vertex](#ur-vertex) for more guidance.
