---
short_title: Available Data
---

# Available NISAR Data

NISAR launched July 30, 2025, and has been successfully collecting data through its Commissioning phase and into the Science phase. The calibration-validation process is underway, and fully calibrated NISAR PROVISIONAL products for the full observation plan are now available to the public.

In addition, a limited set of [NISAR S-band sample data products](https://bhoonidhi.nrsc.gov.in/NISAR/NisarProducts.html) can now be accessed through ISRO's [Bhoonidhi data hub](https://bhoonidhi.nrsc.gov.in/bhoonidhi/home.html). This S-band product release includes RSLC, GSLC, and GCOV products generated from NISAR acquisitions in January and February 2026. Refer to the [Bhoonidhi NISAR Mission site](https://bhoonidhi.nrsc.gov.in/NISAR/) for more information.

(nisar-provisional-data-july)=
## NISAR PROVISIONAL Data: July 2026

<!-- #TODO: add summary of PROVISIONAL data -->

(nisar-sample-data-feb)=
## NISAR BETA Pre-Calibration Data: February 2026

{button}`Find NISAR L-Band Data <https://search.asf.alaska.edu/#/?dataset=NISAR&prodConfig=PR&resultsLoaded=true>`

Prior to the release of the PROVISIONAL products, a selection of pre-calibration BETA NISAR L-band Level-1 to Level-3 products were made available through the ASF DAAC. This large volume of global data was released to allow users to develop workflows to access the data and metadata for each product type, to become familiar with the characteristics of the L-band products, and to begin working with the data in a substantive way.

The February 2026 release of NISAR L-band pre-calibration data includes all Level-1 to Level-3 products for a subset of the data acquired between October 17, 2025 and January 20, 2026. This includes up to 8 acquisitions per track (both ascending and descending), and is a representative distribution of the production observation plan. @feb-26-data-release displays the spatial extent of the data included in this release. For a more detailed acquisition map, see the interactive [NISAR February 2026 Released Data](https://experience.arcgis.com/experience/0042193b06104889971cd77f505190e0) map.

```{figure} ../assets/feb-26-data-release.png
:label: feb-26-data-release
:alt: Map of the spatial extent of archived pre-calibration products included in the February 2026 data release.
:align: center

Spatial distribution of the archived pre-calibration NISAR data products, highlighted in green, included in the February 2026 data release.  
<span style="font-size: 12px;">_Basemap credits: Esri, TomTom, Garmin, FAO, NOAA, USGS, (c) OpenStreetMap contributors, and the GIS User Community._</span>
```

(known-issues)=
(sample-product-limitations)=
The BETA products are not fully calibrated, and there are a number of [known issues](#product-known-issues) users should be aware of when working with these datasets. The PROVISIONAL products released in July 2026 are fully calibrated and partially validated, and are a significant improvement over the BETA products. Users should exercise care if attempting to analyze BETA products together with PROVISIONAL products.

(data-release-timeline)=
## L-Band Data Release Timeline

NISAR has continually collected L-band data over nearly all global landmasses since August 2025. @data-acquisition-extent shows the spatial extent of the collected data. The [NISAR Reference Observation Plan](https://experience.arcgis.com/experience/6052a864cd01459393884a7f751558e3) provides a more detailed, interactive map of NISAR data acquisitions.

```{figure} ../assets/data-acquisition-extent.png
:label: data-acquisition-extent
:alt: Map of the spatial extent of NISAR data collection.
:align: center

Spatial extent of NISAR L-band data collection, highlighted in green.
<span style="font-size: 12px;">_Basemap credits: Esri, TomTom, Garmin, FAO, NOAA, USGS, (c) OpenStreetMap contributors, and the GIS User Community._</span>
```

All L-band data products processed by the mission will be available to the public through the Alaska Satellite Facility.

The nominal data release timeline as of June 2026 is described below.

### Jan 2026: Sample products
An [initial release](https://www.earthdata.nasa.gov/news/nisar-sample-data-products-available) of 25 pre-calibration sample data products were made available on January 23, 2026. This release included one or more products of each of the nine Level 1-3 product types.

### Feb 2026: Pre-calibration products
A [larger volume](https://www.earthdata.nasa.gov/news/nisar-release-over-100000-new-data-product-files) of pre-calibration global data products were made available on February 27, 2026. This release included over 100,000 Level 1-3 products totaling over 500 TB of science data. These datasets are marked as BETA, as they are not yet fully calibrated.

(timeline-calibrated-forward-processing)=
### Jul 2026: Provisional forward processing
After the calibration phase concludes and planned software improvements are completed, the NISAR project will begin forward processing of newly-acquired data. These datasets will be marked as PROVISIONAL, indicating that they are calibrated and partially validated, but processing improvements are still underway. Provisional datasets will be released in the second half of July 2026, including all acquisitions starting from June 17, 2026.

This release will be the first to include [L0B RRSD](#rrsd-product-overview) products, which will have a nominal latency of 2-10 hours from data acquisition to availability. Level 1-3 products will have a nominal latency of 36-72 hours. Products will be continuously generated and made publicly available for all areas shown in @data-acquisition-extent and in the [NISAR Reference Observation Plan](#nisar-reference-observation-plan). 

(validated-reprocessing)=
### Q4 2026: Validated reprocessing

After the start of forward processing, additional validation will take place using the provisional data, resulting in algorithm improvements. Once the products are fully validated, the NISAR project will transition to generating validated products with a new version of the processor and begin a reprocessing campaign. These validated products will supersede any earlier versions of the data in the archive.

This reprocessing campaign will generate new versions of Level 0-3 products from the global backlog of all L-band data collected during the science phase of the mission. Data products will be continually published to ASF and made publicly available as they are generated during the reprocessing effort, which is expected to be complete by the end of 2026.
