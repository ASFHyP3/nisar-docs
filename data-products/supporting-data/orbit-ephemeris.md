---
short_title: Orbit Ephemeris
---

# NISAR Orbit Ephemeris

{button}`Find Data <https://search.earthdata.nasa.gov/search?q=NISAR_OE>`

## Orbit Ephemeris Overview

NISAR Orbit Ephemeris (OE) products describe the position, velocity, and acceleration of the NISAR satellite through time. Accurate ephemeris measurements are essential for focusing, mapping, and geolocating SAR imagery, and are often used as input to SAR processing workflows.

## Orbit Ephemeris Datasets

Satellite position and velocity can be predicted in advance with reasonable accuracy. Position and velocity measured at the time of acquisition yield improved accuracy and precision. Accuracy and precision can be further improved after the time of acquisition by incorporating additional GNSS data.

Four types of Orbit Ephemeris products are provided for NISAR reflecting this trade-off between latency and quality:

1. Forecast Orbit Ephemeris (FOE)
2. Near real-time Orbit Ephemeris (NOE)
3. Medium precision Orbit Ephemeris (MOE)
4. Precise Orbit Ephemeris (POE)

FOE products are the earliest available and lowest data quality, while POE products are the latest available and highest data quality. The characteristics of these datasets are described in @tbl:nisar-orbit-ephemeris-characteristics.

:::{table} Orbit Ephemeris Dataset Characteristics
:label: tbl:nisar-orbit-ephemeris-characteristics

| Product Type           | Latency  | Delivery frequency | Time coverage                                                                          | Sampling     |
|------------------------|----------|--------------------|----------------------------------------------------------------------------------------|--------------|
| Forecast (FOE)         | Forecast | Daily              | One week into the future                                                               | Every 30 sec |
| Near real-time (NOE)   | Hours    | Hourly             | One product file released every hour containing up to 30 hours of reconstructed orbits | Every 10 sec |
| Medium precision (MOE) | Days     | Daily              | One product file per day, including 3 hours of orbits from previous and subsequent day | Every 10 sec |
| Precise (POE)          | Weeks    | Daily              | One product file per day, including 3 hours of orbits from previous and subsequent day | Every 10 sec |

:::

## Orbit Ephemeris File Contents

Each OE product is an XML file containing a list of position, velocity, and acceleration vectors at regular time intervals. A full description of the XML structure and data values will be made available in a future Product Specification document.

## Orbit Ephemeris Naming Convention

NISAR_ANC_J_PR_\{{term}`ProductType`}\_\{{term}`CreationTime`}\_\{{term}`ValidityStartTime`}\_\{{term}`ValidityEndTime`}.xml

:::{glossary}
ProductType
: FOE, NOE, MOE, or POE

CreationTime
: UTC time of product creation in `YYYYMMDDThhmmss` format

ValidityStartTime
: UTC time of the first orbit state vector in the product in `YYYYMMDDThhmmss` format

ValidityEndTime
: UTC time of the last orbit state vector in the product in `YYYYMMDDThhmmss` format
:::

For example, a file named `NISAR_ANC_J_PR_POE_20260107T213450_20251224T205942_20251226T025942.xml` is a Precise Orbit Ephemeris product created on Jan 7, 2026 that contains orbit state vectors from Dec 24, 2025 20:59:42 through Dec 26, 2025 02:59:42 in UTC time.

## Finding and Downloading Orbit Ephemeris Files

You can find and download NISAR OE products using the `NISAR_OE` short name in [Earthdata Search](#earthdata-search-overview) or via the [Earthaccess Python package](#earthaccess-package).

You can also find and download NISAR OE products via [Direct AWS S3 Access](#aws-s3-access-overview). OE files are organized in a separate prefix for each product type, as shown in @tbl:nisar-orbit-ephemeris-s3-locations:

:::{table} S3 Locations by Product Type
:label: tbl:nisar-orbit-ephemeris-s3-locations

| Product Type           | S3 location                                   |
|------------------------|-----------------------------------------------|
| Forecast (FOE)         | `s3://sds-n-cumulus-prod-nisar-products/FOE/` |
| Near real-time (NOE)   | `s3://sds-n-cumulus-prod-nisar-products/NOE/` |
| Medium precision (MOE) | `s3://sds-n-cumulus-prod-nisar-products/MOE/` |
| Precise (POE)          | `s3://sds-n-cumulus-prod-nisar-products/POE/` |

:::
