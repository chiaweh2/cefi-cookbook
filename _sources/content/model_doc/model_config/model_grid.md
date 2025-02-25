---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.5
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

Regional MOM6 Grid
===

(rmom6Grid)=
## Horizontal Grids
```{warning}
When user use the raw model output, a `ocean_static.nc` file is also needed for getting the geospatial location of the grided values.
```
To understand all the grid points that is provided in `ocean_static.nc`, we need to first introduce the Arakawa C grid that is used by regional MOM6.

````{dropdown} What is Arakawa C Grid? (optional read)
The Arakawa grid system, including the C-grid, was introduced by Arakawa and Lamb in 1971.
The “staggered” Arakawa C-grid is named so because it further separates the evaluation of vector quantities compared to the Arakawa B-grid. For instance, instead of evaluating both east-west (u) and north-south (v) velocity components at the grid center, the C-grid evaluates the u components at the centers of the left and right grid faces, and the v components at the centers of the upper and lower grid faces1.
This staggering of variables is employed to retain non-divergence of the flow at all times2. The Weather Research and Forecasting Model (WRF), for example, uses the Arakawa Staggered C-Grid in its atmospheric calculations. This staggering allows for more accurate representation and computation of physical quantities in numerical models.
````

### What the `ocean_static.nc` file provides
Here, we use a python package called `Xarray` to demostrate what the `ocean_static.nc` provides. 
```{tip}
If you have netcdf4 package installed in you local system, `ncdump -hs ocean_static.nc` also shows the same information directly in the Command Line Interface.
```
```{code-cell} ipython3
import xarray as xr
opendap_url = "http://psl.noaa.gov/thredds/dodsC/Projects/CEFI/regional_mom6/northwest_atlantic/hist_run/ocean_static.nc"
xr.open_dataset(opendap_url)
```
From the output, we can find there are many two dimensional matrices (arrays) that provides different quantity related to the grid structure of the model. In the following section, we will get into each of the variables that is listed in this "grid file".


### "Staggered" Grid
The figure below illustrates the grid design that is called the Arakawa C grid
```{image} ../../../images/arakawaCGrid.png
:alt: Arakawa C "staggered" grid illustration
:class: bg-primary mb-1
:width: 90%
:align: center
```
- **Scalars** are quantities that are fully described by a magnitude (or numerical value) alone. In this context, they are located at the **T/h-points**.
- **Velocities** are vector quantities that are described by both a direction and a magnitude. Here, they are staggered such that **u-points** (representing velocity in the x-direction) and **v-points** (representing velocity in the y-direction) are not at the same location.
- **Vorticities**, which measure the spinning motion of fluid particles, are located at **q-points**.

The indexing for points (i,j) in the logically-rectangular domain is such that i increases in the x direction (eastward for spherical polar coordinates), and j increases in the y direction (northward for spherical polar coordinates).
A q-point with indices (i,j) lies to the upper right (northeast) of the h-point with the same indices. This means that if you have a scalar at a certain point (h-point), the vorticity (q-point) associated with that scalar is located to its upper right.

### Grid Distance
Besides the location of the grid, the `ocean_static.nc` file also provide the grid distant in the file to calculate the derivative or area.
The figure illustrates the grid cell distances for all different aspect of the grid points in the staggered grid structure
```{image} ../../../images/arakawaCGrid_dist.png
:alt: Arakawa C grid distant illustration
:class: bg-primary mb-1
:width: 90%
:align: center
```
These quantitys are also provided in the `ocean_static.nc` file.

## Vertical Grids
The index for the vertical dimension k increases with depth, although the vertical coordinate z, measured from the mean surface level z=0, decreases with depth. This means that as you go deeper into the fluid, the k index increases, but the z coordinate (measured from the surface) decreases.
```{image} ../../../images/arakawaCGrid_vertical.png
:alt: Arakawa C grid vertical structure illustration
:class: bg-primary mb-1
:width: 90%
:align: center
```
```{warning}
In the `ocean_static.nc` file, there isn't a vertical coordinate or index. The vertical coordinate that the CEFI data portal provides has been adjusted to a regular z coordinate, which increases with depth. This adjusted coordinate is only present in data with three-dimensional values. The coordinate variables include `z_l`, which represents the depth at the center of a cell, and `z_i`, which represents the depth at the cell interface. In other words, `z_l` and `z_i` are used to denote the depth at different points within the cell structure in the data.
```