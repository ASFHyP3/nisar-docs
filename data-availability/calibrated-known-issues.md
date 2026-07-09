---
short_title: Known Issues
---
# Provisional Products

_Updated February 27, 2026_

(provisional-known-issues)=
## Provisional Product Known Issues

The NISAR Products being released have a CRID 5023.  These are calibrated and have undergone validation at a limited set of sites around the world. These data are designated as Provisional pending more complete validation over larger areas around the global. The Provisional products meet radiometric and geolocation requirements in areas where ionospheric variability is low, generally in the lower latitudes.   
At high latitudes, mitigation of ionospheric effects on the propagation path have proven to be challenging.  The data are quite usable scientifically, but users can expect some degradation in performance, including geolocation errors, patterned decorrelation bands in interferograms, and interferometric phase residuals even after applying the ionospheric estimation layer. In cases where local geometric distortions are larger than a fraction of a pixel, phase residuals can be introduced by the processing algorithm themselves. In particularly active areas near the poles on specific days, a few data sets might be rendered unusable. The project and science teams continue to work on improved mitigation methods.
There are few other issues that users should be aware of:
1.	NISAR L-band data is affected strongly in specific geographic areas by radio-frequency interference (RFI).  The Provisional products have been created with an RFI filter that performs very well, such that in most places, users will not be aware that RFI existed.  However, in some places the RFI filter underperforms by leaving residual RFI, or overperforms by removing features in high contrast areas.  
2.	Low-level ripples in the SLC data may occasionally be seen in areas with dark backgrounds.  These are introduced in the L0B data, which continue to have low levels of residual energy from the looped-back transmit events present at their edges.  The residual signal levels are low and meet requirements, but further work is needed to eliminate them. This will occur in the next release.
3.	The calibration of the 5 MHz “Frequency B” channel, which is designed for split-spectrum processing, has larger systematic radiometric calibration residuals than the main band “Frequency A”.  While there are no radiometric requirements for Frequency B, science team members have found these data to be useful in their own right.  In future releases, the project will work to reduce these residuals further.
All released data going forward will have a CRID of 5023 or higher.  The pre-calibrated data released in February 2026 have lower CRID numbers, and users should exercise care in attempting to analyze them together with CRID 5023+ products. The February 2026 data will be reprocessed along with all data acquired from beginning of mission until June 16, when the CRID 5023 forward processing began.
