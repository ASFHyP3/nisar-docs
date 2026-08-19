# Harmony

(harmony-overview)=
## Harmony Services for NISAR

[Harmony](https://www.earthdata.nasa.gov/data/tools/nasa-harmony) is Earthdata's data transformation service for customizing NASA datasets. It is seamlessly integrated into the [Earthdata Search](#earthdata-search-overview) platform, but users can also leverage the [Harmony APIs](https://harmony.earthdata.nasa.gov/docs) or the [Harmony-py](https://github.com/nasa/harmony-py) Python library to interact with the data programmatically. 

ASF is working with the Harmony team to develop subsetting functionality, starting with a service that [extracts individual datasets](#harmony-extract-datasets) from NISAR HDF5 products and exports them as GeoTIFFs. 

Refer to the @tools-services-roadmap to see the development plan for additional Harmony services supporting NISAR.

### Dataset Extraction Service

(harmony-supported-products-extract)=
Users can use Harmony to extract individual datasets as GeoTIFFs from NISAR HDF5 files for the following products: 

- Geocoded Polarimetric Covariance ([GCOV](#gcov-product-overview))
- Geocoded Unwrapped Interferogram ([GUNW](#gunw-product-overview))
- Geocoded Pixel Offsets ([GOFF](#goff-product-overview))
- Soil Moisture ([SME2](#sme2-product-overview))

Users can extract two-dimensional datasets under the `/science/LSAR/$product-type/grids/` group as stand-alone GeoTIFFs for these products. This can be particularly useful for those users only interested in one or two layers in a product. However, users interested in multiple layers will be better served by [downloading the full HD5 file](#download-nisar-data-earthdata-search). 

(harmony-extract-datasets)=
## Extract Datasets in Earthdata Search

Harmony services are available directly in [Earthdata Search](#earthdata-search-overview), which is a map-based web browser interface for data search and access. This makes it easy to find NISAR products for your area and time period of interest and extract just the datasets of interest from the HDF5 file. Each selected dataset is output as a GeoTIFF file.

1. Search for one of the [supported product types](#harmony-supported-products-extract) in [Earthdata Search](#earthdata-search-overview) and [select the desired collection](#find-nisar-collections).

    ```{figure} ../assets/harmony-search-gcov.png
    :label: harmony-search-gcov-image
    :alt: Screenshot of searching for a GCOV product in Earthdata Search
    :align: center
    :class: framed
    
    Search for [supported product type](#harmony-supported-products-extract) collections in [Earthdata Search](#earthdata-search-overview) and select the desired collection.
    ```

2. Add one or more granules to a project by clicking the green ＋ icon for each item of interest.

    ```{figure} ../assets/harmony-add-to-project.png
    :label: harmony-add-to-project-image
    :alt: Screenshot of adding an item to a project in Earthdata Search
    :align: center
    :class: framed
    
    Click the green ＋ icon for a granule of interest to add it to your project.
    ```

3. Click the **My Project** button to view the list of granules you've added. 

   - You will need to log in with your [Earthdata Login](#earthdata-login) credentials if you have not already done so. 

    ```{figure} ../assets/harmony-open-project.png
    :label: harmony-open-project-image
    :alt: Screenshot of opening the My Project pane in Earthdata Search
    :align: center
    :class: framed
    
    Click the **My Project** button to view the list of granules you've added.
    ```

4. Select the **Customize Download** option, then click the **Edit Variables** button.
   
    ```{figure} ../assets/harmony-customize-download.png
    :label: harmony-customize-download-image
    :alt: Screenshot of selecting the option to customize download and clicking the Edit Variables button
    :align: center
    :class: framed
    
    Select the **Customize Download** option, then click the **Edit Variables** button.
    ```

   - If you add datasets for multiple collections to the same project, each collection will be listed in the left panel. You can switch collections by clicking the **Edit Options** link for the desired collection.

      ```{figure} ../assets/harmony-multiple-collections.png
      :label: harmony-multiple-collections-image
      :alt: Screenshot of accessing the download options for each collection when multiple collections are added to the same project
      :align: center
      :class: framed
      
      When multiple collections are included in the project, click the **Edit Options** link for each collection to set the variables to extract.
      ```

5. Click on the directory icons to see their contents. Select the individual datasets to extract, then click the **Download Data** button.

    ```{figure} ../assets/harmony-select-variables.png
    :label: harmony-select-variables-image
    :alt: Screenshot of selecting the datasets to extract from a NISAR HDF5 file
    :align: center
    :class: framed
    
    Expand the directory structure and select the datasets to be extracted to GeoTIFF format, then click the **Download Data** button.
    ```

   - Not all products will contain all the listed variables. This list includes all possible variables that _may_ be present in a product of that type. If you select any variables that are not present in your selected granule, the job will still run. 
     - GeoTIFFs will be generated for any selected variables that are present in the granule, and any datasets that are not present will be ignored.
     - If you do not see a download link for a variable you selected, refer to the [naming convention](#naming-convention-overview) of the file to determine which polarizations and frequencies would be expected for that product. 
   - If multiple collections are included in the Project, you will need to define the download options for each one. You can either: 
     - Click the **Edit Options** link for each collection, as illustrated in @harmony-multiple-collections-image.
     - Click the **Back to Edit Options** link at the top of the panel once you have made your variable selections and click the **Next** button to progress through each collection. 

        ```{figure} ../assets/harmony-multiple-edit.png
        :label: harmony-multiple-edit-image
        :alt: Screenshot of using the Next button to access the download options for each collection when multiple collections are added to the same project
        :align: center
        :class: framed
      
        To set download options when multiple collections are included in the project, click the **Next** button at the bottom of the Edit Options panel to move to the next collection.
        ```

   - The **Download Data** button will launch the Harmony jobs for all collections in the project that have extraction options defined. 
   
6. Harmony will process your extraction request, and indicate its progress on the status page.

    ```{figure} ../assets/harmony-status-page.png
    :label: harmony-status-page-image
    :alt: Screenshot of the Harmony Status page in Earthdata Search
    :align: center
    :class: framed
    
    Once you click the **Download Data** button, the Harmony Status page will open and indicate progress.
    ```

7. Once the extraction process is complete, the download links for the individual GeoTIFFs will be displayed. Click each link to download the products through the web browser, or click the **Download Files** button to leverage the Earthdata bulk download app.

    ```{figure} ../assets/harmony-status-complete.png
    :label: harmony-status-complete-image
    :alt: Screenshot of the Harmony Status page in Earthdata Search showing a completed job
    :align: center
    :class: framed
    
    Once the extraction process is complete, the Harmony Status page will display the download links for the extracted GeoTIFFs. 
    ```