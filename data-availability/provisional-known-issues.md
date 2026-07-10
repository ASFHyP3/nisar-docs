---
short_title: Known Issues
---
# Provisional Products

_Updated February 27, 2026_

(provisional-known-issues)=
## Provisional Product Known Issues

The PROVISIONAL products released in July 2026 are calibrated and have undergone validation at a limited set of sites around the world. These data are designated as PROVISIONAL pending more complete validation over larger areas around the globe. The Provisional products meet radiometric and geolocation requirements in areas where ionospheric variability is low, generally in the lower latitudes. 

These products, processed using the [NISAR Composite Release ID (CRID) P05023](https://www.earthdata.nasa.gov/data/platforms/space-based-platforms/nisar/nisar-composite-release-id-crid), are a significant improvement over the [pre-calibration BETA products](#nisar-sample-data-feb) released in February 2026, and most of the [known issues associated with the BETA products](#product-known-issues) have been resolved. There are, however, a few known issues with the PROVISIONAL products that users should be aware of. 

### Ionospheric Effects

At high latitudes, mitigation of ionospheric effects on the propagation path have proven to be challenging. The data are quite usable scientifically, but users can expect some degradation in performance, including geolocation errors, patterned decorrelation bands in interferograms, and interferometric phase residuals even after applying the ionospheric estimation layer. 

In cases where local geometric distortions are larger than a fraction of a pixel, phase residuals can be introduced by the processing algorithm themselves. In particularly active areas near the poles on specific days, a few data sets might be rendered unusable. The project and science teams continue to work on improved mitigation methods.

### Radio Frequency Interference

NISAR L-band data is affected strongly in specific geographic areas by radio-frequency interference (RFI). The PROVISIONAL products have been created with an RFI filter that performs very well, such that in most places, users will not be aware that RFI existed. However, in some places the RFI filter underperforms. This can result in the presence of bright patches that mask landscape features, or attenuation of non-RFI backscatter. 

### Ripples in SLC Data

Low-level ripples in the SLC data may occasionally be seen in areas with dark backgrounds. These are introduced in the L0B data, which continue to have low levels of residual energy from the looped-back transmit events present at their edges. The residual signal levels are low and meet requirements, but further work is needed to eliminate them. This work will be implemented in the next release.

### Frequency B Calibration

The calibration of the 5 MHz `Frequency B` channel, which is designed for split-spectrum processing, has larger systematic radiometric calibration residuals than the main band `Frequency A`. While there are no radiometric requirements for Frequency B, science team members have found these data to be useful in their own right. In future releases, the project will work to reduce these residuals further.

## BETA and PROVISIONAL Products

The PROVISIONAL products are available for acquisitions starting June 17, 2026. Until the [reprocessing campaign](validated-reprocessing) is undertaken to release fully validated data from the start of the science phase of the mission onward, only the BETA products will be available for earlier acquisition dates. 

All released data going forward from the PROVISIONAL data release will have a CRID of P05023 or higher. The BETA pre-calibration data released in February 2026 have lower CRID numbers, and users should exercise care in attempting to analyze BETA products together with PROVISIONAL products. 