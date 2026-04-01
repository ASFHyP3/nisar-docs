---
short_title: ASF Search Python Package
---
# Finding NISAR Data with ASF Search

(asf-search-package)=
## ASF Search Python Package

ASF's [`asf_search`](https://pypi.org/project/asf-search/) Python package enables quick and customizable programmatic access to NISAR data. 

## ASF Search Version
The `asf_search` package is always under development to add functionality in support of new platforms and products, to manage dependencies, and to comply with security best practices. In particular, NISAR support in `asf_search` will be evolving as more data products are added to the archive and preferred search patterns emerge. 

As such, we recommend using the latest release of the package whenever possible. You can update your installation of `asf_search` via `pip` with:
```
python -m pip install --upgrade asf_search
```
or via `conda` with:
```
conda update asf_search
```
<!-- TODO: Add in minimum asf_search version that allows for NISAR searches -->

## Search for NISAR Data

To quickly begin exploring NISAR data, search by setting the `dataset` parameter to `'NISAR'` and the `processingLevel` parameter to the four-letter acronym corresponding to your desired product. For example, to search for NISAR GCOV products, use the following Python code:
```python
import asf_search as asf

results = asf.search(dataset='NISAR', processingLevel='GCOV')
``` 
A list of accepted `processingLevel` constants for data from all missions hosted by ASF, including NISAR, is available [here](https://github.com/asfadmin/Discovery-asf_search/blob/master/asf_search/constants/PRODUCT_TYPE.py). 

Refer to the [Searching page of the ASF Data Search Manual](https://docs.asf.alaska.edu/asf_search/searching/)
 for more details on available search filters and their possible values.

## Download data

Downloading NISAR data requires authentication through [Earthdata Login (EDL)](https://urs.earthdata.nasa.gov/). For more information, see @earthdata-login. 

EDL credentials can be provided to `asf_search` using the `ASFSession` class. After creating an authenticated `ASFSession`, pass the session object to the download function along with the target directory path where the data will be saved:
```python 
session = asf.ASFSession().auth_with_creds('username', 'password')
results.download(path='path/to/data/', session=session) 
```
Alternatively, users may [configure a local `.netrc` file](https://nsidc.org/data/user-resources/help-center/creating-netrc-file-earthdata-login) to store their EDL credentials. Once the `.netrc` file is properly set up, downloads can be performed without explicitly passing credentials:
```python
results.download(path='path/to/data/')
```

## Stream data

NISAR data can also be streamed into memory using `asf_search` when accessed on a resource in the `us-west-2` region.  AWS `us-west-2` NISAR data is typically served to users through HTTPS CloudFront URLs. 

Data streaming can be done using `https` or S3 protocols, both of which are described in the examples below. 

### Example: Stream via HTTPS

Similar to downloading data, streaming requires user obtain an [EDL account](https://urs.earthdata.nasa.gov/). However, rather than passing a `username` and `password`, a EDL login token is required. For step-by-step guidance on generating an EDL token, see the [User Token Management](https://urs.earthdata.nasa.gov/documentation/for_users/user_token) document. After generating the token, it is valid for 60 days. 

This example streams data for a single RSLC product. First, the code snippet uses `asf_search` to retrieve an HTTPS access url, then sets a [`fsspec`](https://filesystem-spec.readthedocs.io/en/latest/) configuration, and then opens the data with [`xarray`](https://docs.xarray.dev/en/stable/) using the `h5netcdf` engine. 

The code below will also require the python packages [`h5netcdf`](https://h5netcdf.org/index.html) and [`aiohttp`](https://docs.aiohttp.org/en/stable/) be installed before running. 

```python
import asf_search as asf
import fsspec
import xarray as xr

results = asf.search(dataset='NISAR', processingLevel='RSLC', maxResults=1)

token = ... # Requires Earthdata Login Token :https://urs.earthdata.nasa.gov/documentation/for_users/user_token
fs = fsspec.filesystem('https', client_kwargs={'headers': {'Authorization': f'Bearer {token}'}, 'trust_env': False})

fsspec_config = {
    'cache_type': 'background',
    'block_size': 16*1024*1024,  # 16 MB
}

ds = xr.open_datatree(
    fs.open(results[0].get_urls()[0], **fsspec_config),
    engine='h5netcdf',
    decode_timedelta=False,
    phony_dims='access',
)

print(ds.science.LSAR.identification.isDithered.values) 
```

### Example: Stream via S3

Prior to running, obtain [credentials from the NISAR s3 credentials endpoint](nisar-s3-credentials-endpoint) and [configure your environment to use temporary AWS credentials](export-s3-credentials). These credentials are valid for 60 minutes after generation. 

This example streams data for a single RSLC product. First, we use `asf_search` to retrieve a URL for `h5` file. Then, we use `s3fs` to pass the AWS credentials in our environment to stream the data. 

Ensure that the [`h5netcdf`](https://h5netcdf.org/index.html) python package is installed before running. 

```python 
import asf_search as asf
import s3fs
import xarray as xr

results = asf.search(dataset='NISAR', processingLevel='RSLC', maxResults=1)

s3_links = results[0].properties["s3Urls"]
s3_h5_link = [link for link in s3_links if link.endswith(f'{results[0].properties["sceneName"]}.h5')]

fsspec_config = {
    'cache_type': 'background',
    'block_size': 16*1024*1024,  # 16 MB
} 

s3 = s3fs.S3FileSystem()
ds = xr.open_datatree(
   s3.open(s3_h5_link[0], **fsspec_config),
   engine='h5netcdf',
   decode_timedelta=False,
   phony_dims="access"
)
```