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