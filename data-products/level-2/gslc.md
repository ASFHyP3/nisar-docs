---
short_title: GSLC
---
# Geocoded Single Look Complex (GSLC)

{button}`Product Specification <https://nisar.asf.earthdatacloud.nasa.gov/NISAR-SAMPLE-DATA/DOCS/NISAR_D-102269_RevE_NASA_SDS_Product_Specification_L2_GSLC_Nov8_2024_w-sigs.pdf>`
{button}`Find Data <https://search.asf.alaska.edu/#/?dataset=NISAR&sciProducts=GSLC>`

(gslc-product-overview)=
## Product Overview

The GSLC product is a Level 2 product derived from the Level-1 [RSLC](#rslc-product-overview) product by geocoding the input RSLC into a map coordinate system such as a UTM Zone or Polar stereographic projection system.

The geocoding is performed by inverse mapping of the map coordinates with their topographic heights into the radar coordinate system and interpolating the radar signal at the radar location corresponding to the map coordinate. Phase-preserving complex interpolation projects the data onto a uniformly spaced, north-south/east-west aligned geographic grid. 

### Interferometry

The phase of the GSLC product is flattened for the orbit used in the RSLC processing. The phase flattening removes the topographic phase contribution in the GSLC. Consequently, cross-multiplying two GSLC products will result in an interferometric phase flattened interferogram.

### Backscatter

Amplitude values in the GSLC product are presented as Digital Numbers (DN). To help users transform these DN values to beta-nought, sigma-nought, or gamma-nought backscatter, look-up tables (LUTs) are provided in the GSLC product. Refer to [this Earthdata Forum post](https://forum.earthdata.nasa.gov/viewtopic.php?f=7&p=25489#p25489) to learn how to use these LUTs to convert the DN values to your desired radar backscatter coefficient.
