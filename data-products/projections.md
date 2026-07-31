# Projections

(nisar-l2-projections)=
## NISAR Level 2 Projections

NISAR [Level 2](#level-2-geocoded-products) products are georeferenced and provided in map coordinates. The projected coordinate system used for each product will depend on its location, as described in @tbl:nisar-projections. 

- Products between 60°N and 60°S are projected to the UTM Zone (WGS 84) appropriate for the product location
- Products north of 60°N are projected to the NSIDC Sea Ice Polar Stereographic North (EPSG 3413) projection
- Products south of 60°S are projected to the Antarctic Polar Stereographic (EPSG 3031) projection

:::{table} Projections used for Level 2 NISAR products
:label: tbl:nisar-projections
| EPSG Code(s) | Common Name | Geographical Extent |
| --- | --- | --- |
| 3413 | NSIDC Sea Ice Polar Stereographic North | Acquisitions north of 60°N |
| 3031 | Antarctic Polar Stereographic | Acquisitions south of 60°S |
| 32601-32660 | UTM Zone North | Acquisitions between 0°N and 60°N |
| 32701-32760 | UTM Zone South | Acquisitions between 0°S and 60°S |
:::

The following figures illustrate the extent of the different projections used for ascending frames (@projections-ascending-image) and descending frames (@projections-descending-image).

```{figure} ../assets/projections-ascending.png
:label: projections-ascending-image
:alt: Figure illustrating the extent of different projections used for ascending NISAR frames
:align: center

Different projectsions used for ascending NISAR frames.
```

```{figure} ../assets/projections-descending.png
:label: projections-descending-image
:alt: Figure illustrating the extent of different projections used for descending NISAR frames
:align: center

Different projectsions used for descending NISAR frames.
```

(nisar-l3-projections)=
## NISAR Level 3 Projections

NISAR [Level-3](#level-3-geophysical-products) products ([SME2](#sme2-product-overview)) are posted to the global [EASE Grid 2.0 (EPSG 6933)](https://nsidc.org/data/user-resources/help-center/guide-ease-grids) with a pixel spacing of 200 m. 
