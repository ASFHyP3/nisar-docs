---
short_title: Known Issues
---
# Provisional Products

(provisional-known-issues)=
## Provisional Product Known Issues

The PROVISIONAL products [released in July 2026](#nisar-provisional-data-july) are calibrated and have undergone validation at a limited set of sites around the world. These data are designated as PROVISIONAL pending more complete validation over larger areas around the globe. The Provisional products generally meet radiometric and geolocation requirements in lower-latitude areas where ionospheric variability is low. 

These products, processed using the [NISAR Composite Release ID (CRID) P05023](https://www.earthdata.nasa.gov/data/platforms/space-based-platforms/nisar/nisar-composite-release-id-crid), are a significant improvement over the [pre-calibration BETA products](#nisar-sample-data-feb) released in February 2026, and most of the [known issues associated with the BETA products](./product-known-issues.md) have been resolved. There are, however, a few known issues with the PROVISIONAL products that users should be aware of. 

### Ionospheric Effects

At high latitudes, mitigation of ionospheric effects on the propagation path have proven to be challenging. The data are quite usable scientifically, but users can expect some degradation in performance, including geolocation errors, patterned decorrelation bands in interferograms, and interferometric phase residuals even after applying the ionospheric estimation layer. 

In cases where local geometric distortions are larger than a fraction of a pixel, phase residuals can be introduced by the processing algorithm themselves. In particularly active areas near the poles on specific days, a few data sets might be rendered unusable. The project and science teams continue to work on improved mitigation methods.

### Radio Frequency Interference

NISAR L-band data is affected strongly in specific geographic areas by radio-frequency interference (RFI). The PROVISIONAL products have been created with an RFI filter that performs very well, such that in most places, users will not be aware that RFI existed. However, in some places the RFI filter underperforms by leaving residual RFI, or overperforms by removing features in high contrast areas.  

### Ripples in SLC Data

Low-level ripples in the SLC data may occasionally be seen in areas with dark backgrounds. These are introduced in the L0B data, which continue to have low levels of residual energy from the looped-back transmit events present at their edges. The residual signal levels are low and meet requirements, but further work is needed to eliminate them. This work will be implemented in the next release.

### Frequency B Calibration

The calibration of the 5 MHz `Frequency B` channel, which is designed for split-spectrum processing, has larger systematic radiometric calibration residuals than the main band `Frequency A`. While there are no radiometric requirements for Frequency B, science team members have found these data to be useful in their own right. In future releases, the project will work to reduce these residuals further.

### Incomplete L0B Products

Users will find some products were generated from incomplete L0B datasets, due to missing data in the downlink caused by weather and other capture issues.  The quality flags in the L0B data quality products identify where these data issues occur. The higher-level products generated from these incomplete L0B are included in the archive, since some users may still find them useful. Because the issues are ephemeral, they are difficult to track in advance.

### Diagnostic Mode Frames

Users will find that the L-SAR products using calibration modes in Track 161/174, 161/175, 169/090, 169/091 are not usable. This will be rectified in August 2026.

### 40 MHz Banding

40 MHz products in joint mode appear to have residuals radiometric bands that are larger than typical.  They are still within requirements, but are visually noticeable.  The team is working on understanding this issue.

(provisional-known-issues-sme2)=
### Soil Moisture Products

[Soil Moisture (SME2)](#sme2-product-overview) products require time series of Level 2 [GCOV](#gcov-product-overview) products as input for the processing workflow. Because fully calibrated GCOV products have only recently become available, and the calibration/validation process requires longer time series before some cal/val metrics (e.g., un-biased root mean squared error (UBRMSE)) can be computed, the SME2 products in the PROVISIONAL collection are not yet fully calibrated. 

In areas of quad-pol acquisitions, there are three to six gaps across the swath due to the nature of NISAR’s SweepSAR acquisition and the number of time steps used in the soil moisture algorithm. In these gap areas, there will be occasions where one or more of the three soil moisture algorithms included in the SME2 products may not deliver an estimate.

## BETA and PROVISIONAL Products

The PROVISIONAL products are available for acquisitions starting June 17, 2026. Until the [reprocessing campaign](#validated-reprocessing) is undertaken to release fully validated data from the start of the science phase of the mission onward, only the BETA products will be available for earlier acquisition dates. 

All released data going forward from the PROVISIONAL data release will have a CRID of P05023 or higher. The BETA pre-calibration data released in February 2026 have lower CRID numbers, and users should exercise care in attempting to analyze BETA products together with PROVISIONAL products. 