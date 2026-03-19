# Amplitude

(sar-amplitude)=
## SAR Amplitude
The amplitude component of a SAR acquisition is the amount of the signal sent out by the sensor that returns to be measured, often referred to as radar backscatter. These values represent the conditions of the scatterers on the earth’s surface in that area, and can indicate the degree of surface roughness, structural complexity, and relative moisture content. 

Backscatter values are impacted by changes to the physical structure of the earth’s surface, including processes that alter vegetation or built structures. Because of NISAR’s regular acquisition schedule and insensitivity to cloud cover, data is available at regular intervals all over the world. This makes it very valuable for time-series analysis, which can be used to track short- or long-term changes to natural and anthropogenic features. 

The L-band sensor can penetrate through moderately complex vegetation and more deeply into the soil than C-band SAR sensors such as Sentinel-1. This provides insight into the conditions under the canopy, and at deeper levels in the soil column, and having observations using both wavelengths (and, in some areas, S-band data in addition) increases the ability to understand processes driving change on the landscape.

## Amplitude Datasets

### GCOV

For NISAR data, the [Geocoded Covariance (GCOV)](#gcov-product-overview) are the most accessible amplitude-based products. The individual covariance layers in the GCOV product have had Radiometric Terrain Correction (RTC) applied. This process uses a DEM to correct for distortions caused by the impacts of terrain on the side-looking acquisitions. 

Not only is the output product aligned with the DEM topographically, but radiometric flattening is applied to normalize the radar backscatter based on the surface area contributing to the signal returns. The pixel values represent radar backscatter in gamma-nought power, with a different layer for each polarization. 

### GSLC

The [Geocoded Single Look Complex (GSLC)](#gslc-product-overview) products are also terrain corrected, as the topographic phase is removed. They have not been radiometrically flattened, however, which differentiates them from the GCOV covariance layers. 

The pixel values are encoded as complex Digital Numbers (DN), but the amplitude values can be [extracted and converted from beta-nought radiometry](#gslc-backscatter) to either gamma-nought or sigma-nought if desired. For users who do not want or need the backscatter values to be normalized to the area contributing to the signal returns, GSLC products are also a source for amplitude values.

The pixel spacing of the GSLC products is smaller than the GCOV products. While this can allow users to see features in finer detail, it does mean that the files are also much larger. They can be more time-consuming to download, visualize, and analyze than the GCOV products. 


