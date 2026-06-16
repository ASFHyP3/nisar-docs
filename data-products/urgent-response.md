# NISAR Urgent Response Products

##  Urgent Response Product Overview

NISAR is a powerful tool for monitoring surface dynamics, but most NISAR products are not made available until 36-72 hours after data acquisition.

NISAR Urgent Response (UR) products provide expedited processing in response to major events or natural disasters, such as earthquakes, volcanic activity, flooding, or wildfires. Acquisitions designated for UR data delivery will be flagged for rapid downlink and processing to provide [low-latency](#latency) data in support of response efforts.

UR products use lower-quality orbit ephemeris files for product processing than are used to process standard Production (PR) products, and do not have all atmospheric corrections applied. This may impact data quality, but allows the UR products to be made available much more quickly than PR products. Users should consider whether these tradeoffs are acceptable for their use case. 

(ur-latency)=
### Latency

Urgent response [Level 0](#level-0-unfocused-raw-products) (raw) products should be available within 2 hours of acquisition, while [Level 2](#level-2-geocoded-products) (geocoded) products should be available within 6 hours of acquisition. Refer to @tbl:ur-processing-estimates for a comparison of data processing latency between PR and UR products.

:::{table} Processing time estimate comparisons for Production (PR) and Urgent Response (UR) products 
:label: tbl:ur-processing-estimates
:align: center

| Product          | PR Best Estimate | UR Best Estimate |
|------------------|------------------|------------------|
| L0               | 12 Hours         | 2 Hours          |
| L1               | 2 Days           | 4 Hours          |
| L2               | 3 Days           | 6 Hours          |
| L3 Soil Moisture | 4 Days           | N/A              |

:::

### Tasking

NISAR's Smart Tasking Tool triggers UR requests automatically in response to earthquakes greater than 7.0 magnitude and less than 50 km deep, and volcanic events that trigger volcano observatory notices. UR products can also be manually requested by authorized users at government agencies such as USGS and NOAA. 

Note that the UR designation only prioritizes expedited downlinking and processing for acquisitions already in the [NISAR acquisition plan](#nisar-reference-observation-plan). It is not designed to support requests for acquisitions that deviate from the existing plan.

### Product Availability

UR products will be available for 30 days. After 30 days, the UR products will be removed from the archive, and only the standard PR products for that acquisition will be available. 

### Naming Convention

UR products use the same [naming conventions](#naming-convention-overview) as standard NISAR products. They can be identified by the **Product Identifier** component, which is `UR` for Urgent Response, instead of `PR` for Production.

For example, an RSLC UR product would have a filename like: 

`NISAR_L1_`**UR**`_RSLC_001_005_A_219_4020_SVNA_A_20220104T182346_20220104T183426_P01101_M_F_J_001.h5`

### Ancillary Data 

UR products include lower precision orbit files and have fewer ancillary data layers than PR products. UR products are processed using Forecast Orbit Ephemera (FOE), which are preliminary predicted and lowest data quality of the @orbit-ephemeris-datasets. A comparison of ancillary data layers in Production and UR products is described in @tbl:ur-ancillary-data-layers. 

:::{table} Ancillary data layers available for Production (PR) and Urgent Response (UR) products 
:label: tbl:ur-ancillary-data-layers
:align: center

| Data Layer                                                      | PR Products                                                          | UR Products                    |
|-----------------------------------------------------------------|----------------------------------------------------------------------|--------------------------------|
| Orbit Ephemeris                                                 | Near-Realtime Orbit Ephemeris (NOE) and Medium Orbit Ephemeris (MOE) | Forecast Orbit Ephemeris (FOE) |
| Radar Pointing                                                  | Near-Realtime Radar Pointing (NRP) and Precise Radar Pointing (PRP)  | Forecast Radar Pointing (FRP)  |
| Geolocation Correction using Ionospheric Total Electron Content | Yes                                                                  | No                             |
| Tropospheric Correction                                         | Yes                                                                  | No                             |

:::

### Finding UR Products in Vertex

Once processed, UR products will be available through @vertex. To filter for UR products, select the **Urgent Response** filter option under **Product Configuration** in **Product Filters**, as shown in @vertex-urgent-response-filter. 

```{figure} ../assets/vertex-urgent-response-filter.png
:label: vertex-urgent-response-filter
:alt: Screenshot of the Urgent Response filter in Vertex selected in the Product Configuration menu. 
:align: center

Search for Urgent Response products in Vertex by selecting Urgent Response in the Product Configuration dropdown menu in the Product Filters section.  
```

