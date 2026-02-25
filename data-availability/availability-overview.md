---
short_title: Available Data
---

# Available NISAR Data

NISAR launched July 30, 2025, and has been successfully collecting data through its Commissioning phase and into the Science phase. The calibration-validation process is underway, and a selection of uncalibrated data generated from NISAR acquisitions is now available to the public.

(nisar-sample-data-feb)=
## NISAR Uncalibrated Data: February 2026 

{button}`Find NISAR Data <https://search.asf.alaska.edu/#/?dataset=NISAR&prodConfig=PR&resultsLoaded=true>`

NISAR mission data were processed to generate products from Level-1 to Level-3. These datasets are available for a range of geographic locations, and give users a first look at products generated from NISAR acquisitions. These uncalibrated products are a preview for a full calibrated data release scheduled for June 2026.  

The NISAR project is still in the early phases of calibration, so these products are not yet fully calibrated, and contain artifacts, as described in @sample-product-limitations. The products will be improved in [future releases](#data-release-timeline), but allow users to become familiar with NISAR data products and develop methods for working with the data and metadata.

## Product Availability

The February 2026 release of NISAR uncalibrated data includes a global dataset, representative of the final product distribution of all NISAR products. All Level-1 to Level-3 product types are available. 

This release includes data acquired between October 17, 2025 and January 20, 2026. This includes up to 8 acquisitions per track (both ascending and descending). @feb-26-data-release displays the spatial extent of the data included in this release. For a more detailed acquisition map, see the [NISAR Spring 2026 Released Data Plan map](https://experience.arcgis.com/experience/0042193b06104889971cd77f505190e0). 


```{figure} ../assets/feb-26-data-release.png
:label: feb-26-data-release
:alt: Map of uncalibrated products included in the February 2026 data release.  
:align: center

Spatial distribution of the uncalibrated NISAR data products, highlighted in green, included in the February 2026 data release. 
```

(sample-product-limitations)=
## Sample Product Limitations 

There are known limitations in the sample products. Keep these in mind when working with the data.

1. Radiometric banding across the swath. This is due to incomplete calibration, specifically:
   * Inter-beam channel calibration: The on-board digital beamforming is controlled by amplitude and phase weights for each of the receive channels. These weights have not yet been updated based on diagnostic mode analysis. These adjustments are expected to be very small, with a minor improvement to SNR and phase variability. As can be seen in this release, the beamforming is working very well even without adjustments. 
   * Antenna pattern calibration, which is still being refined.

1. Very low amplitude radiometric ripple aligned with the azimuth direction, only noticeable in some radar dark areas, and at a spatial scale of about 600 m and shorter. We are working to improve radiometric uniformity at this low level, but SNR may still exhibit some banding at this scale.

1. Bright narrow bands in azimuth direction may appear at very dark regions, primarily visible at the backscatter of frequency B data. This is a known issue mostly caused by incomplete masking of the transmit gaps of the receive window where the transmit events occur. 

1. Polarimetric channel imbalance. Polarimetric calibration and estimation of channel imbalances in the presence of a highly active ionosphere have not yet been performed. These steps will follow the radiometric corrections described above.

1. Quad-polarimetric (QP) product noise layers: In the QP products, the noiseEquivalentBackscatter layer for the HH polarimetric channel is incorrectly populated with zeros. The noiseEquivalentBackscatter layers for the HV and VV polarimetric channels are populated with correct (uncalibrated) values.

1. The Geocoded Unwrapped (GUNW) interferogram product has three known limitations:
   * The boundary of the ionospheric phase layer has edge-effect artifacts. These artifacts originate from inaccurate valid sample sub swath masks in the input RSLC products and will be resolved in a future release. Additionally, ionospheric phase layers may show localized artifacts caused by localized phase noise due to Radio Frequency Interference, water bodies, vegetation, snow coverage or other factors. The algorithm refinement to better maks such localized decorrelating regions and minimizing artifacts in the ionospheric phase is under development. 
   * Interferogram generation over solid earth regions does not yet use the full "rubbersheeting" algorithm to estimate local image distortions due to large deformations. The algorithm used here for alignment of radar imagery (coregistration) is based on geometrical offsets (derived from imaging geometry of the NISAR acquisitions, orbit and a digital elevation model) refined with a polynomial fit to the data-driven dense offsets computed from amplitude cross correlation of the radar data. 
   * Interferogram generation over crysophere regions uses a full rubbersheeting algorithm in which the coregistration is based on geometrical offsets refined with dense offsets computed from amplitude cross correlation. 

1. The noise floor for 77 MHz data appears higher than expected. The issue is still being investigated, but is probably related to the calibration tone settings and how they impact quantization. 

(data-release-timeline)=
## Data Release Timeline

As of end of February 2026, the timeline for NISAR product releases is as follows: 

- **January 23**: [Initial release](https://www.earthdata.nasa.gov/news/nisar-sample-data-products-available) of 25 sample data products
- **February 27**: Released a larger volume of uncalibrated global data products
- **June 2026**: Release of fully calibrated and algorithmically improved global products