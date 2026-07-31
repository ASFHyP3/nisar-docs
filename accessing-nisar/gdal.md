# Subsetting NISAR Data with GDAL

NISAR products are distributed in HDF5 format, and can be subsetted into the GeoTIFF format utilizing NASA's Harmony service in the cloud. However, for those with the local compute to do so, it is also possible to subset these files locally using the GDAL command line utility. We will utilize GDAL's ability to stream data from Earthdata Cloud directly, allowing us to only download the necessary data for our specific subsetting operation.

## Preparing GDAL to access Earthdata Cloud
If you do not already have GDAL installed you can follow [GDAL's official guide](https://gdal.org/en/stable/download.html). 

In this guide we will be streaming products directly from Earthdata Cloud without downloading them first. To do so, we must allow GDAL to authenticate to Earthdata Cloud by placing a `.netrc` file in the home directory of our compute environment containing our Earthdata login.

```
# ~/.netrc
machine urs.earthdata.nasa.gov
    login <username>
    password <password>
```

## Utilizing GDAL to subset NISAR HDF5 Products

### Variable Subsetting
To view the available data elements and variables present in a product utilize the following command. These are also listed in detail in the [Data Products](/data-products/products-overview.md) section.

```

gdalinfo "/vsicurl/https://<DOWNLOAD URL>" \
         --config GDAL_HTTP_NETRC=YES \
         --config GDAL_HTTP_COOKIEFILE=/tmp/gdal_cookies.txt \
         --config GDAL_HTTP_COOKIEJAR=/tmp/gdal_cookies.txt
```

Utilize the following command to extract a specific data element from an HDF5 product as a GeoTIFF. The download URL can be found via the copy download url button in Vertex.
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

The `gdalwarp` command is also suitable for this, and can be used as a drop in replacement. However we have found an up to 30% performance improvement when utilizing the `gdal_translate` command for simple variable subsetting operations.

### Spatial Subsetting

Spatial subsetting is possible in `gdal_translate` however the use of `gdalwarp` for spatial subsetting allows spatial extents to be described with WKT geometry strings, such as the strings used for Vertex's AOI (Area of Interest) feature. This allows the use of Vertex or other geospatial user interfaces to select a spatial extent for subsetting. To reproject in `gdalwarp` utilize the `-cutline <WKT>` flag alongside the `-cutline srs WGS84`, `-crop_to_cutline` and `-dstalpha` flags such as in the example below.

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

### Reprojection

Reprojection operations can also be performed in `gdalwarp` utilizing the `-t_srs <SRS>`, where `<SRS>` is a EPGS code (such as `EPSG:3857` for Web Mercator).

```
gdalwarp -of GTiff \
         "/vsicurl/https://<DOWNLOAD URL>":<VARIABLE PATH> <OUTPUT FILE>.tif \
         -t_srs <SRS>
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


## Utilizing a gdalrc file to simplify commands

By placing a file in `~/.gdal/gdalrc` with the following content we can avoid needing all of the `--config` flags placed at the end of our commands.

```

#~/.gdal/gdalrc
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
