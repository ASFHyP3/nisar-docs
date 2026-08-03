# GDAL

The [Geospatial Data Abstraction Library (GDAL)](https://gdal.org/en/stable) is an open-source software library used to work with raster and vector geospatial data. There are a number of GDAL command line utilities that we can leverage to transform NISAR data.

## Using GDAL to Transform NISAR Data

NISAR products are distributed in HDF5 format, and the files can be very large. Many users may want to transform the data by extracting just the datasets of interest from the HDF5 files and/or subsetting the data to a defined spatial extent. 

We can use command line utilities from the GDAL software library to transform these files. Leveraging GDAL's ability to stream data from Earthdata Cloud directly will allow us to download only the data we need in the desired format.

### Preparing GDAL to Access EDC

If you do not already have GDAL installed you can follow [GDAL's official guide](https://gdal.org/en/stable/download.html). 

:::{warning} NISAR HDF5 format not supported in GDAL HDF5 drivers prior to version 3.13.0
For GDAL releases older than `3.13.0`, the `NETCDF` driver must be used instead of the default `HDF5` driver when working with NISAR products. 

Because NISAR encodes the spatial reference system using netCDF CF conventions, older HDF5 drivers cannot find the geospatial information required to project the data to a map. 

**Users can direct GDAL to use the netCDF driver by prepending `NETCDF:` to `/vsicurl/` in all GDAL commands.**

To identify your currently installed version of GDAL, run `gdal --version`.
:::

In this guide we will be streaming products directly from NASA's [Earthdata Cloud (EDC)](https://www.earthdata.nasa.gov/about/earthdata-cloud-evolution) without downloading them first. To do so, we must allow GDAL to authenticate to EDC by placing a `.netrc` file in the home directory of our compute environment containing our [Earthdata Login](#earthdata-login) credentials.

```{code-block}
:filename: "~/.netrc"

machine urs.earthdata.nasa.gov
    login <username>
    password <password>
```

### Using a `gdalrc` File

Users can choose to generate a `gdalrc` file to simplify GDAL commands. This replaces the need to include `--config` flags for each command.

Create a file in `~/.gdal/gdalrc` with the following content:

```{code-block}
:filename "~/.gdal/gdalrc"

[configoptions]
CPL_VSIL_CURL_CHUNK_SIZE 2097152
CPL_VSIL_CURL_CACHE_SIZE 67108864
GDAL_CACHEMAX 64000000
GDAL_DISABLE_READDIR_ON_OPEN=TRUE
GDAL_HTTP_MERGE_CONSECUTIVE_RANGES=YES
GDAL_HTTP_MULTIPLEX=YES
GDAL_NUM_THREADS=ALL_CPUS
CPL_VSIL_CURL_CACHE_SIZE=1GB
GDAL_HTTP_NETRC=YES
GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt
GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```

If you have a `gdalrc` file staged, you can skip all the `--config` flags included in the sample commands on this page.

## Transform NISAR HDF5 Products

Users can transform NISAR data by using the gdal_translate or gdal_warp utilities to [extract](#gdal-extract) and/or [spatially subset](#gdal-spatial-subset) data, [reproject](#gdal-spatial-reproject) the data, and change the file format. For the examples provided here, we will output the data as a GeoTIFF.

You will need the download link for a NISAR product to run these commands. Use the [Copy URL](#copy-download-url-image) links available in the search results for Vertex, or use one of the other search methods available to find a NISAR product URL.

```{figure} ../assets/copy-download-url.png
:label: copy-download-url-image
:alt: Screenshot of the Copy URL link for a NISAR product in Vertex. 
:align: left
:width: 50%

Click the Copy URL link to get the download URL for a NISAR product in Vertex.  
```

(gdal-extract)=
### Extract Datasets

To view the available datasets present in a NISAR product, run the following command using the download URL for a NISAR product: 

```

gdalinfo "/vsicurl/https://<DOWNLOAD URL>" \
         --config GDAL_HTTP_NETRC=YES \
         --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
         --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```

Refer to the [Data Products](/data-products/products-overview.md) section for more information about the datasets included in NISAR products.

Utilize the following command to extract a specific dataset from an HDF5 product as a GeoTIFF.
```
gdal_translate -of GTiff \
                "/vsicurl/https://<DOWNLOAD URL>":<VARIABLE PATH> <OUTPUT FILE>.tif \
                --config CPL_VSIL_CURL_CHUNK_SIZE 2097152 \
                --config CPL_VSIL_CURL_CACHE_SIZE 67108864 \
                --config GDAL_CACHEMAX 64000000 \
                --config GDAL_DISABLE_READDIR_ON_OPEN=TRUE \
                --config GDAL_HTTP_MERGE_CONSECUTIVE_RANGES=YES \
                --config GDAL_HTTP_MULTIPLEX=YES \
                --config GDAL_NUM_THREADS=ALL_CPUS \
                --config CPL_VSIL_CURL_CACHE_SIZE=1GB \
                --config GDAL_HTTP_NETRC=YES \
                --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
                --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```

In the earlier 

The `gdalwarp` command is also suitable for this, and can be used as a drop-in replacement. However, using `gdal_translate` for simple dataset extraction operations may provide up to a 30% improvement in performance.

:::{hint} Example 
First we start by fetching the info of the NISAR GCOV product we will use for this example.

```
gdalinfo "/vsicurl/https://nisar.asf.earthdatacloud.nasa.gov/NISAR/NISAR_L2_GCOV_BETA_V1/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001.h5" 
```

Looking in the subdatasets section of the output of this command we are given information on the first dataset:
```

SUBDATASET_1_NAME=HDF5:"/vsicurl/https://nisar.asf.earthdatacloud.nasa.gov/NISAR/NISAR_L2_GCOV_BETA_V1/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001.h5"://science/LSAR/GCOV/grids/frequencyA/HHHH
SUBDATASET_1_DESC=[35928x36288] //science/LSAR/GCOV/grids/frequencyA/HHHH (32-bit floating-point)
```

The path of this dataset is `/science/LSAR/GCOV/grids/frequencyA/HHHH`. This means it is the frequency A, HHHH polarization dataset of the GCOV. The second line tells us that the dataset is 35928 by 36288 pixels with the type of 32-bit floating point. The `SUBDATASET_1_NAME` provides the full string which we can utilize in a `gdal_translate` command the dataset as a GeoTIFF named `output.tif` as follows.

```
gdal_translate -of GTiff \
                "/vsicurl/https://nisar.asf.earthdatacloud.nasa.gov/NISAR/NISAR_L2_GCOV_BETA_V1/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001.h5"://science/LSAR/GCOV/grids/frequencyA/HHHH output.tif \
                --config CPL_VSIL_CURL_CHUNK_SIZE 2097152 \
                --config CPL_VSIL_CURL_CACHE_SIZE 67108864 \
                --config GDAL_CACHEMAX 64000000 \
                --config GDAL_DISABLE_READDIR_ON_OPEN=TRUE \
                --config GDAL_HTTP_MERGE_CONSECUTIVE_RANGES=YES \
                --config GDAL_HTTP_MULTIPLEX=YES \
                --config GDAL_NUM_THREADS=ALL_CPUS \
                --config CPL_VSIL_CURL_CACHE_SIZE=1GB \
                --config GDAL_HTTP_NETRC=YES \
                --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
                --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt\
```

:::

(gdal-spatial-subset)=
### Spatial Subsetting

Spatial subsetting is possible in `gdal_translate` however the use of `gdalwarp` for spatial subsetting allows spatial extents to be described with WKT geometry strings, such as the strings used for Vertex's AOI (Area of Interest) feature. This allows the use of Vertex or other geospatial user interfaces to select a spatial extent for subsetting. 

To reproject in `gdalwarp` utilize the `-cutline <WKT>` flag alongside the `-cutline srs WGS84`, `-crop_to_cutline` and `-dstalpha` flags such as in the example below.

```
gdalwarp -of GTiff \
         "/vsicurl/https://<DOWNLOAD URL>":<VARIABLE PATH> <OUTPUT FILE>.tif \
         -cutline <WKT> \
         -cutline_srs WGS84 \
         -crop_to_cutline \
         -dstalpha \
         --config CPL_VSIL_CURL_CHUNK_SIZE 2097152 \
         --config CPL_VSIL_CURL_CACHE_SIZE 67108864 \
         --config GDAL_CACHEMAX 64000000 \
         --config GDAL_DISABLE_READDIR_ON_OPEN=TRUE \
         --config GDAL_HTTP_MERGE_CONSECUTIVE_RANGES=YES \
         --config GDAL_HTTP_MULTIPLEX=YES \
         --config GDAL_NUM_THREADS=ALL_CPUS \
         --config CPL_VSIL_CURL_CACHE_SIZE=1GB \
         --config GDAL_HTTP_NETRC=YES \
         --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
         --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```

:::{hint} Example
In this example we will perform spatial subsetting on the subdataset which we identified utilizing the `gdalinfo` utility in the previous example.

We will begin by utilizing Vertex to pick an area within our product. Once we have picked an area within our product, we can copy the AOI string from the header bar of Vertex which is convieniently in WKT format. An example WKT string is given below.

```
POLYGON((-115.7994 43.887,-113.7599 43.887,-113.7599 44.9751,-115.7994 44.9751,-115.7994 43.887))
```

We will then input this string, and the full dataset string which we identified in the previous example into the spatial subsetting snippet which is provided above. This gives us the final command which we can utilize to perform our spatial subsetting operation.

```
gdalwarp -of GTiff \
         "/vsicurl/https://nisar.asf.earthdatacloud.nasa.gov/NISAR/NISAR_L2_GCOV_BETA_V1/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001.h5"://science/LSAR/GCOV/grids/frequencyA/HHHH output.tif \
         -cutline "POLYGON((-115.7994 43.887,-113.7599 43.887,-113.7599 44.9751,-115.7994 44.9751,-115.7994 43.887))" \
         -cutline_srs WGS84 \
         -crop_to_cutline \
         -dstalpha \
         --config CPL_VSIL_CURL_CHUNK_SIZE 2097152 \
         --config CPL_VSIL_CURL_CACHE_SIZE 67108864 \
         --config GDAL_CACHEMAX 64000000 \
         --config GDAL_DISABLE_READDIR_ON_OPEN=TRUE \
         --config GDAL_HTTP_MERGE_CONSECUTIVE_RANGES=YES \
         --config GDAL_HTTP_MULTIPLEX=YES \
         --config GDAL_NUM_THREADS=ALL_CPUS \
         --config CPL_VSIL_CURL_CACHE_SIZE=1GB \
         --config GDAL_HTTP_NETRC=YES \
         --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
         --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```
:::

(gdal-spatial-reproject)=
### Reprojection

Reprojection operations can also be performed in `gdalwarp` utilizing the `-t_srs <SRS>`, where `<SRS>` is a EPSG code (such as `EPSG:3857` for Web Mercator).

```
gdalwarp -of GTiff \
         "/vsicurl/https://<DOWNLOAD URL>":<VARIABLE PATH> <OUTPUT FILE>.tif \
         -t_srs <SRS> \
         -dstalpha \
         --config CPL_VSIL_CURL_CHUNK_SIZE 2097152 \
         --config CPL_VSIL_CURL_CACHE_SIZE 67108864 \
         --config GDAL_CACHEMAX 64000000 \
         --config GDAL_DISABLE_READDIR_ON_OPEN=TRUE \
         --config GDAL_HTTP_MERGE_CONSECUTIVE_RANGES=YES \
         --config GDAL_HTTP_MULTIPLEX=YES \
         --config GDAL_NUM_THREADS=ALL_CPUS \
         --config CPL_VSIL_CURL_CACHE_SIZE=1GB \
         --config GDAL_HTTP_NETRC=YES \
         --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
         --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```

:::{hint} Example
We can utilize this snippet to project the product which we have previously dealt with in our examples into Web Mercator as follows.

```
gdalwarp -of GTiff \
         "/vsicurl/https://nisar.asf.earthdatacloud.nasa.gov/NISAR/NISAR_L2_GCOV_BETA_V1/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001.h5"://science/LSAR/GCOV/grids/frequencyA/HHHH output.tif \
         -t_srs EPSG:3857 \
         -dstalpha \
         --config CPL_VSIL_CURL_CHUNK_SIZE 2097152 \
         --config CPL_VSIL_CURL_CACHE_SIZE 67108864 \
         --config GDAL_CACHEMAX 64000000 \
         --config GDAL_DISABLE_READDIR_ON_OPEN=TRUE \
         --config GDAL_HTTP_MERGE_CONSECUTIVE_RANGES=YES \
         --config GDAL_HTTP_MULTIPLEX=YES \
         --config GDAL_NUM_THREADS=ALL_CPUS \
         --config CPL_VSIL_CURL_CACHE_SIZE=1GB \
         --config GDAL_HTTP_NETRC=YES \
         --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
         --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```
:::
