# Harmony

(harmony-overview)=
## Harmony Services for NISAR

Harmony is Earthdata's data transformation service. It is seamlessly integrated into the [Earthdata Search](#earthdata-search-overview) platform, but users can also leverage the [Harmony APIs](https://harmony.earthdata.nasa.gov/docs) or the [Harmony-py](https://github.com/nasa/harmony-py) Python library to interact with the data programmatically. 

ASF is working with the Harmony team to develop subsetting functionality, starting with a service that [extracts individual datasets](#harmony-extract-datasets) from NISAR HDF5 products and exports them as GeoTIFFs. 

Refer to the @tools-services-roadmap to see the development plan for additional Harmony services supporting NISAR.

### Dataset Extraction Service

(harmony-supported-products-extract)=
Users can use Harmony to extract individual datasets as GeoTIFFs from NISAR HDF5 files for the following products: 

- Geocoded Polarimetric Covariance ([GCOV](#gcov-product-overview))
- Geocoded Unwrapped Interferogram ([GUNW](#gunw-product-overview))
- Geocoded Pixel Offsets ([GOFF](#goff-product-overview))
- Soil Moisture ([SME2](#sme2-product-overview))

(harmony-extract-datasets)=
## Extract Datasets in Earthdata Search

Harmony services are available directly in [Earthdata Search](#earthdata-search-overview), which is a map-based web browser interface for data search and access. 

1. Search for one of the [supported product types](#harmony-supported-products-extract) in [Earthdata Search](#earthdata-search-overview) and select the desired collection.

```{figure} ../assets/harmony-search-gcov.png
:label: harmony-search-gcov-image
:alt: Screenshot of searching for a GCOV product in Earthdata Search
:align: center

Search for [supported product type](#harmony-supported-products-extract) collections in [Earthdata Search](#earthdata-search-overview) and select the desired collection.
```

2. Add one or more granules to a project by clicking the green ＋ icon for each item of interest.

```{figure} ../assets/harmony-add-to-project.png
:label: harmony-add-to-project-image
:alt: Screenshot of adding an item to a project in Earthdata Search
:align: center

Click the green ＋ icon for a granule of interest to add it to your project.
```

3. Click the **My Project** button to view the list of granules you've added. 

   - You will need to log in with your [Earthdata Login](#earthdata-login) credentials if you have not already done so. 

```{figure} ../assets/harmony-open-project.png
:label: harmony-open-project-image
:alt: Screenshot of opening the My Project pane in Earthdata Search
:align: center

Click the **My Project** button to view the list of granules you've added.
```

4. Select the **Customize Download** option, then click the **Edit Variables** button.

```{figure} ../assets/harmony-customize-download.png
:label: harmony-customize-download-image
:alt: Screenshot of selecting the option to customize download and clicking the Edit Variables button
:align: center

Select the **Customize Download** option, then click the **Edit Variables** button.
```

5. Click on the directory icons to see their contents, select the individual datasets to extract, then click the **Download Data** button.

   - Not all products will contain all of the listed variables. This list includes all possible variables that _may_ be present in a product of that type.

```{figure} ../assets/harmony-select-variables.png
:label: harmony-select-variables-image
:alt: Screenshot of selecting the datasets to extract from a NISAR HDF5 file
:align: center

Expand the directory structure and select the datasets to be extracted to GeoTIFF format, then click the **Download Data** button.
```

6. Harmony will process your extraction request, and indicate its progress on the status page.

```{figure} ../assets/harmony-status-page.png
:label: harmony-status-page-image
:alt: Screenshot of the Harmony Status page in Earthdata Search
:align: center

Once you click the Download Data button, the Harmony Status page will open and indicate progress.
```

7. Once the extraction process is complete, the download links for the individual GeoTIFFs will be displayed. Click each link to download the products through the web browser, or click the **Download Files** button to leverage the Earthdata bulk download app.

```{figure} ../assets/harmony-status-complete.png
:label: harmony-status-complete-image
:alt: Screenshot of the Harmony Status page in Earthdata Search showing a completed job
:align: center

Once the extraction process is complete, the Harmony Status page will display the download links for the extracted GeoTIFFs. 
```