# NISAR Urgent Response Products

NISAR Urgent Response (UR) products offer expedited processing in response to major events or natural disasters, such as earthquakes, volcanic activity, flooding, or wildfires. Data delivery of UR products will be flagged for rapid downlink and processing to provide low latency data to support urgent response.

Within 6 hours after acquisition, data should be processed to Level-2 productions. A comparison of UR processing time estimates compared to nominal products is available in @tbl:ur-processing-estimates.

:::{table} Processing time estimate comparisons for Production and Urgent Response products 
:label: tbl:ur-processing-estimates
:align: center

| Product          | Production Best Estimate | Urgent Response Best Estimate |
|------------------|--------------------------|-------------------------------|
| L0               | 12 Hours                 | 2 Hours                       |
| L1               | 2 Days                   | 4 Hours                       |
| L2               | 3 Days                   | 6 Hours                       |
| L3 Soil Moisture | 4 Days                   | N/A                           |

:::

UR Processing can occur at the request of approved federal agencies
Tasking via a smart tasking website can be requested by a set of authorized users at US government agencies, such as USGS and NOAA. 
Such users can also request expedited processing of NISAR data that with prior scheduling
The NISAR operations team determines whether the requested acquisition can be acquired without disrupting the Reference Operation Plan (ROP)
Is there a process for outside people to request UR products

### Naming Convention
UR products use the same naming convention as standard @naming-conventions, but the `Product Identifier` parameter will be `UR` and the `Location` will be `J`, since these products are processed at the Jet Propulsion Laboratory.  For example, a RSLC UR product would have the name: 

`NISAR_L1_`**UR**`_RSLC_001_005_A_219_4020_SVNA_A_20220104T182346_20220104T183426_P01101_M_F_`**J**`_001.h5`

### Ancillary Data 
Expedited processing will include lower quality precision orbit files and have fewer ancillary data layers than standard Production products. UR products are processed using Forcast Orbit Ephemera (FOE), which are preliminary predicted and lowest data quality of the @orbit-ephemeris-datasets. A comparison of ancillary data layers in Production and UR products is described in @tbl:ur-ancillary-data-layers. 

# Add in explanation for corrections? 

:::{table} Ancillary data layers available for Urgent Response and Production products 
:label: tbl:ur-ancillary-data-layers
:align: center

| Data Layer                                                      | Production Products                                                  | Urgent Response Products       |
|-----------------------------------------------------------------|----------------------------------------------------------------------|--------------------------------|
| Orbit Ephemeris                                                 | Near-Realtime Orbit Ephemeris (NOE) and Medium Orbit Ephemeris (MOE) | Forecast Orbit Ephemeris (FOE) |
| Radar Pointing                                                  | Near-Realtime Radar Pointing (NRP) and Precise Radar Pointing (PRP)  | Forecast Radar Pointing (FRP)  |
| Geolocation Correction using Ionospheric Total Electron Content | Yes                                                                  | No                             |
| Tropospheric Correction                                         | Yes                                                                  | No                             |

:::

### Finding UR Products in Vertex
Once processed, UR products will be available through @vertex. To filter for UR products, select the `Urgent Response` filter option under `Product Configuration`, as shown in @vertex-urgent-response-filter. 

```{figure} ../assets/vertex-urgent-response-filter.png
:label: vertex-urgent-response-filter
:alt: Screenshot of the Urgent Response filter in Vertex selected in the Product Configuration menu. 
:align: center

Search for Urgent Response products in Vertex by selecting Urgent Response in the Product Configuration dropdown menu in the Product Filters section.  
```

### Alerts
You can subscribe to CMR email subscription 
Once a regular acquisition replaces the UR product, probably something like 30 days 


Urgent response products showing up in worldview. When production product comes along, it will replace the UR product
