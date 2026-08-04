# GDAL

The [Geospatial Data Abstraction Library (GDAL)](https://gdal.org/en/stable) is an open-source software library used to work with raster and vector geospatial data. There are a number of GDAL command line utilities that we can leverage to transform NISAR data.

## Using GDAL to Transform NISAR Data

NISAR products are distributed in HDF5 format, and the files can be very large. Many users may want to transform the data by extracting just the datasets of interest from the HDF5 files and/or subsetting the data to a defined spatial extent. 

We can use command line utilities from the GDAL software library to transform these files. Leveraging GDAL's ability to stream data from Earthdata Cloud directly will allow us to download only the data we need in the desired format.

### Preparing GDAL to Access EDC

If you do not already have GDAL installed you can follow [GDAL's official guide](https://gdal.org/en/stable/download.html). 

:::{warning} NISAR HDF5 format not supported in GDAL HDF5 drivers prior to version 3.13.0
For GDAL releases older than `3.13.0`, the `NETCDF` driver must be used instead of the default `HDF5` driver when working with NISAR products. Because NISAR encodes the spatial reference system using netCDF CF conventions, older HDF5 drivers cannot find the geospatial information required to project the data onto a map. 

**Users can direct older versions of GDAL to use the netCDF driver by prepending `NETCDF:` to `/vsicurl/` in all GDAL commands.**

To identify your currently installed version of GDAL, run `gdal --version`.
:::

In this guide we will be streaming products directly from NASA's [Earthdata Cloud (EDC)](https://www.earthdata.nasa.gov/about/earthdata-cloud-evolution) without downloading them first. To do so, we must allow GDAL to authenticate to EDC by placing a `.netrc` file in the home directory of our compute environment containing our [Earthdata Login](#earthdata-login) credentials.

```{code-block}
:filename: ~/.netrc

machine urs.earthdata.nasa.gov
    login <username>
    password <password>
```

### Using a `gdalrc` File

Users can choose to generate a `gdalrc` file to simplify GDAL commands. This replaces the need to include `--config` flags for each command.

Create a file in `~/.gdal/gdalrc` with the following content:

```{code-block}
:filename: ~/.gdal/gdalrc

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

Users can transform NISAR data by using the `gdal_translate` or `gdalwarp` utilities to [extract](#gdal-extract) and/or [spatially subset](#gdal-spatial-subset) data, [reproject](#gdal-spatial-reproject) the data, and change the file format. For the examples provided here, we will output the data as a GeoTIFF.

You will need the download link for a NISAR product to run these commands. Use the [Copy URL](#copy-download-url-image) links available in the search results for [Vertex](#vertex-overview), or use one of the other [available search methods](#nisar-access-overview) to find a NISAR product URL.

```{figure} ../assets/copy-download-url.png
:label: copy-download-url-image
:alt: Screenshot of the Copy URL link for a NISAR product in Vertex. 
:align: left
:width: 50%

Click the Copy URL link to get the download URL for a NISAR product in Vertex.  
```

(gdal-extract)=
### Extract Datasets

Run the following command using the download URL for a NISAR product to view the available datasets present in a NISAR product: 

```
gdalinfo "/vsicurl/https://<DOWNLOAD URL>" \
         --config GDAL_HTTP_NETRC=YES \
         --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
         --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```

Refer to the [Data Products](#data-products-overview) section for more information about the datasets included in NISAR products.

Utilize the following command to extract a specific dataset from an HDF5 product as a GeoTIFF:

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

The `gdalwarp` command is also suitable for this, and can be used as a drop-in replacement. However, using `gdal_translate` for simple dataset extraction operations may provide up to a 30% improvement in performance.

:::{hint} Example 
First we start by fetching the info of the NISAR GCOV product we will use for this example.

```
gdalinfo "/vsicurl/https://nisar.asf.earthdatacloud.nasa.gov/NISAR/NISAR_L2_GCOV_BETA_V1/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001.h5" 
```

By looking in the subdatasets section of the output of this command we are given the following information regarding the first dataset:

```
SUBDATASET_1_NAME=HDF5:"/vsicurl/https://nisar.asf.earthdatacloud.nasa.gov/NISAR/NISAR_L2_GCOV_BETA_V1/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001/NISAR_L2_PR_GCOV_005_149_A_024_4005_DHDH_A_20251120T123755_20251120T123830_X05009_N_F_J_001.h5"://science/LSAR/GCOV/grids/frequencyA/HHHH
SUBDATASET_1_DESC=[35928x36288] //science/LSAR/GCOV/grids/frequencyA/HHHH (32-bit floating-point)
```

We can garner a number of important details from this information.
 - The path of this dataset is `/science/LSAR/GCOV/grids/frequencyA/HHHH` as specified by the second field of the `SUBDATASET_1_DESC` variable on the second line. 
   - This means this dataset is the frequency A, HHHH polarization dataset of the GCOV product which we are using for our example. 
 - The first and third field of the `SUBDATASET_1_DESC` variable specifies that the resolution of the dataset is 35928 by 36288 pixels with the type of 32-bit floating point. 
 - The `SUBDATASET_1_NAME` variable provides the full string which we can utilize in a `gdal_translate` command.

The following command utilizes the `SUBDATASET_1_NAME` string to form a command which outputs our chosen dataset as a GeoTIFF named `output.tif`:

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

We can utilize later `SUBDATASET` fields to use this process to extract other datasets in a given NISAR product to GeoTIFF. To do so replace the `1` in `SUBDATASET_1_NAME` with the ID of whatever dataset you wish to extract.
:::

See the [official GDAL documentation on `gdal_translate`](https://gdal.org/en/stable/programs/gdal_translate.html) for more information on the `gdal_translate` command, its use, and capabilities. Similarly, the official documentation on `gdalinfo` is available [here](https://gdal.org/en/stable/programs/gdalinfo.html).

(gdal-spatial-subset)=
### Spatial Subsetting

GDAL has many utilities which allow for spatial subsetting. In this section we will demonstrate spatial subsetting through the use of the `gdalwarp` utility with WKT spatial extent strings.

The `gdalwarp` utility allows describing spatial extents using a type of string known as a Well Known Text (WKT) Polygon or MultiPolygon string. WKT Polygon or MultiPolygon strings are a subset of strings defined by the [OGC Standard, Section 7](https://www.ogc.org/standards/sfa/). Instructive examples for WKT strings are available on [Wikipedia](https://en.wikipedia.org/wiki/Well-known_text_representation_of_geometry). For future convenience we will refer to WKT Polygon or MultiPolygon strings as WKT spatial extent strings. WKT spatial extent strings are utilized widely across geospatial applications, such as in Vertex, QGIS, and more. An easy method for sampling WKT spatial extent strings is to pick an Area of Interest (AOI) in Vertex, and then copy the string associated with that AOI in the filter bar.

:::{tip}
In previous sections we have utilized the `gdal_translate` utility. This utility does support spatial subsetting, however in this section we will instead utilize the `gdalwarp` utility to perform such an operation. The `gdalwarp` utility allows for more flexible spatial subsetting by inputting WKT spatial extent strings. The `gdal_translate` utility does not support the use of such strings. The ease of use of WKT spatial extent strings and their flexibility outweighs the potential performance improvements provided by `gdal_translate` for most users. Utilize the `-projwin` and `projwin_srs` flags as described in the [`gdal_translate` docs](https://gdal.org/en/stable/programs/gdal_translate.html#cmdoption-gdal_translate-projwin) if you are interested in the highest performance spatial subsetting possible.
:::

To perform spatial subsetting with `gdalwarp` utilize the `-cutline <WKT>` flag alongside the `-cutline srs WGS84`, `-crop_to_cutline` and `-dstalpha` flags. The command below demonstrates the use of these flags:

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

We will begin by utilizing Vertex to pick an area within our product. Once we have picked an area within our product, we can copy the AOI string from the header bar of Vertex which is conveniently in WKT format. An example WKT spatial extent string obtained in this manner is given below.

```
POLYGON((-115.7994 43.887,-113.7599 43.887,-113.7599 44.9751,-115.7994 44.9751,-115.7994 43.887))
```

We will then input this string, and the full dataset string which we identified in the previous example into the spatial subsetting snippet which is provided above. This gives us the final command, which we can utilize to perform our spatial subsetting operation:

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

See the [official GDAL documentation on `gdalwarp`](https://gdal.org/en/stable/programs/gdalwarp.html) for more information on the `gdalwarp` command, its use, and capabilities.

(gdal-spatial-reproject)=
### Reprojection

The `gdalwarp` utility can also be used to reproject datasets from the [projection used for the source NISAR HDF5 product](#nisar-l2-projections) to a different spatial reference system.

In your `gdalwarp` command, set the `-t_srs <SRS>` flag, where `<SRS>` is the [EPSG code](https://epsg.io/) for the desired output spatial reference system (such as `EPSG:3857` for Web Mercator):

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
We can utilize this snippet to project the product which we have dealt with in our previous examples into Web Mercator as follows:

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
