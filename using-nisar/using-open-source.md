# Open Source Software 

(open-source-software)=
## Programmatic Approaches

Users who want to develop programmatic workflows to access, analyze, and visualize NISAR data can use a range of existing open-source software packages, including those listed here. 

### Data Search and Discovery
- [asf-search](https://github.com/asfadmin/Discovery-asf_search): SAR-specific data discovery tools (see @asf-search-package)
- [earthaccess](https://github.com/earthaccess-dev/earthaccess): General data discovery tools for all NASA EO data (see @earthaccess-package)

### NISAR Mission Data Processing Code
- [ISCE3](https://github.com/isce-framework/isce3): Processing code for generating NISAR L1 and L2 products (see @isce-processing-software)
- [PLAnT-ISCE3](https://github.com/isce-framework/plant-isce3): Provides convenience scripts to simplify running ISCE3

### Data Transformation
- [gdal-driver-nisar](https://anaconda.org/channels/nisar-forge/packages/gdal-driver-nisar/overview): GDAL plugin providing streaming capabilities and block-optimized reading for NISAR HDF5 products (see @gdal-nisar)
- [openSEPPO](https://github.com/EarthBigData/openSEPPO): Tools for processing and managing SAR remote sensing data, focused on NISAR products
- [nisarHDF](https://github.com/fastice/nisarhdf): Provides NISAR data transformation utilities and support for Greenland Ice Mapping Project (GrIMP) workflows
- [nisar_pytools](https://github.com/ZachHoppinen/nisar_pytools): Includes tools to search, access, and transform data, as well as an RSLC to GUNW InSAR pipeline

### InSAR
- [GMTSAR](https://github.com/gmtsar/gmtsar): A GMT-based InSAR processor with NISAR support
- [dolphin](https://github.com/isce-framework/dolphin): Persistent-scatterer and distributed-scatterer InSAR wrapped phase estimation
- [sweets](https://github.com/isce-framework/sweets): End-to-end InSAR workflow automation leverging dolphin 
- [MintPy](https://github.com/insarlab/MintPy): Small baseline subset (SBAS) InSAR time series processing

### Polarimetry
- [PolSAR tools](https://github.com/polsartools/polsartools): Polarimetric SAR processing tools

Refer to the [Tutorials](#tutorials-overview) section for workflows that leverage some of these packages. 
