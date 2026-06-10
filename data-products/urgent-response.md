# NISAR Urgent Response Products

Describe strategy (couple paragraphs), including what it means to "task" and what events trigger rapid response processing.
How to find UR data (naming conventions, search filters, etc.)
Latency vs. quality tradeoffs
Life cycle of the products
Link to Earthdata (LANCE) page

NISR starts hazards and response capability to help. Respond to national disasters. 
Depending on product type, 1 to 3 days from data acquisition
Capability to have data available to the public with 6 hours of acquisition 
see the [Land, Atmosphere Near real-time Capability for Earth observation (LANCE)](https://www.earthdata.nasa.gov/data/projects/lance)
Automated generation for volcanoes and earthquakes based on certain criteria 
Smart Tasking requested limited to certain gov’t agencies, USGS and NOAA
"task" requesting that can redirect the satellite to capture image over a region of interest
"Smart tasking" software that can automatically trigger tasking
Tasking via a smart tasking website can be requested by a set of authorized users at US government agencies, such as USGS and NOAA. 
Such users can also request expedited processing of NISAR data that with prior scheduling
The NISAR operations team determines whether the requested acquisition can be acquired without disrupting the Reference Operation Plan (ROP)
Within 6 hours after acquisition, data should be downlinked and processed to Level 2 productions. 

| Product          | Current Best Estimate (Nominal) | Current Best Estimate (Urgent Response) |
|------------------|---------------------------------|-----------------------------------------|
| L0               | 12 Hours                        | 2 Hours                                 |
| L1               | 2 Days                          | 4 Hours                                 |
| L2               | 3 Days                          | 6 Hours                                 |
| L3 Soil Moisture | 4 Days                          | N/A                                     |

Is there a process for outside people to request UR products
Tradeoffs include Using a lower precision orbit file (other ancillary data layers that we don’t get?) 


| Data Layer                                                      | Nominal Products                                                     | Urgent Response Products       |
|-----------------------------------------------------------------|----------------------------------------------------------------------|--------------------------------|
| Orbit Ephemeris                                                 | Near-Realtime Orbit Ephemeris (NOE) and Medium Orbit Ephemeris (MOE) | Forecast Orbit Ephemeris (FOE) |
| Radar Pointing                                                  | Near-Realtime Radar Pointing (NRP) and Precise Radar Pointing (PRP)  | Forecast Radar Pointing (FRP)  |
| Geolocation Correction using Ionospheric Total Electron Content | Yes                                                                  | No                             |
| Tropospheric Correction                                         | Yes                                                                  | No                             |

Naming convention Level-2 naming convention with UR for the "processing type" 
In Vertex, selecting the `Urgent Response` under `Product configuration`
image vertex-urgent-response-filter

```{figure} ../assets/vertex-urgent-response-filter.png
:label: vertex-urgent-response-rilter
:alt: Screenshot of the Urgent Response filter in Vertex selected in the Product Configuration menu. 
:align: center

Search for Urgent Response products in Vertex by selecting Urgent Response in the Product Configuration dropdown menu in the Product Filters section.  
```

Can find using vertex
You can subscribe to CMR email subscription 
Once a regular acquisition replaces the UR product, probably something like 30 days 

UR Preocessing can occur at the request of approved federal agencies

LANCE earth data application group/project earth data low latency capabilities, if it has a low latency requirement it gets sent to lance

Urgent response products showing up in worldview. When production product comes along, it will replace the UR product
