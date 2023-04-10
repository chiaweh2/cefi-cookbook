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

Accessing table (spreadsheet) data
===

## Packages used
To use python to access the ERDDAP server directly from your python script or jupyter-notebook, you will need
- ERDDAPY
- Xarray
- netcdf4 
- matplotlib
- folium

```{note}
The package [**netcdf4**](http://unidata.github.io/netcdf4-python/) develop by UNIDATA is not needed in the import part of the python script. However, it is the essential package that [support netCDF format output from Xarray](https://docs.xarray.dev/en/stable/user-guide/io.html). The package [**matplotlib**](https://matplotlib.org/stable/) is also not needed in the import part of the python script. It is the essential package that [support quick visualization from Xarray](https://docs.xarray.dev/en/stable/user-guide/plotting.html). 
```

+++

In this page, we demonstrate how to extract/download data directly from a ERDDAP server and perform data processing, visualization, and export data in python environment. 

```{tip}
[Understanding of the ERDDAP server and what it provides](errdapData) is highly recommended before reading the following intructions.
```

## Import python packages

```{code-cell} ipython3
# execute the two line when using colab
# !pip install erddapy
# !pip install netcdf4
```

```{code-cell} ipython3
import xarray as xr
from erddapy import ERDDAP
```

- [**xarray**](https://docs.xarray.dev/en/stable/getting-started-guide/why-xarray.html) is used for data processing and netCDF file output. 
- [**erddapy**](https://ioos.github.io/erddapy/00-quick_intro-output.html) is used to access the ERDDAP server.

Both package-webpages have more detail explanation on its full range of functionalities. 
Here we will mainly focusing on getting the data to be displayer and downloaded.


## Access TableDAP type data
In this demostration, we will be getting the table data of CPS Trawl Life History Haul Catch Data from [NOAA NMFS ERDDAP server](https://coastwatch.pfeg.noaa.gov/erddap/tabledap/FRDCPSTrawlLHHaulCatch.html)

Firstly, the way to use the **erddapy** is to setup the destination ERDDAP server as an object in python through `ERDDAP` ([a python class](https://docs.python.org/3/tutorial/classes.html))

```{code-cell} ipython3
#### access the ERDDAP server
e = ERDDAP(
    server="https://coastwatch.pfeg.noaa.gov/erddap/",    # The URL that the ERDDAP server has
    protocol="tabledap",                                   # The data type (griddap or tabledap)
    response="opendap",                                   # different output data type that provided by ERDDAP server       
)
```

```{note}
Like the comment in the code above, three most important keyword arguments ([kwarg](https://docs.python.org/3/glossary.html#term-argument)) to set for the `ERDDAP` class are `server` (The URL that the ERDDAP server is located which has the form of `"https://.../erddap/"`), `protocol` (The [data type](erddapData) one want to get. It is either `"tabledap"` or `"griddap"`), and `response` (For most general use, set the kwarg as `"opendap"` to request the data through OPeNDAP Data Access Protocol (DAP) and its projection constraints).
```
By executing the above code block, we have already setup the connection with the desired ERDDAP server. 
To request a specific dataset on the server, we need to know the `dataset_id`.
The fastest way to get the dataset ID is to go into the data page (e.g. https://coastwatch.pfeg.noaa.gov/erddap/tabledap/FRDCPSTrawlLHHaulCatch.html).
The dataset ID is shown on the second line right after institution. 
```{tip}
One can also get the dataset ID directly from the URL shown above (e.g. https://.../**FRDCPSTrawlLHHaulCatch**.html).
```
To set the `dataset_id`, execute

```{code-cell} ipython3
# set the dataset id name 
#  ex:  https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplAquariusSSS3MonthV5.html
#  dataset_id = jplAquariusSSS3MonthV5
e.dataset_id = "FRDCPSTrawlLHHaulCatch"
```

## Download data 
Now, all the setting for downloading the data is complete for this simple example.
All we need to do is to fetch the data from the server to local machine memory.
`erddapy` has a widely used Xarray backend to support export to xarray object. 
Simply execute

```{code-cell} ipython3
ds = e.to_xarray()
```

The `ds` object constructed by Xarray is a great way to see the gridded data structure and perform quick visualization, preprocessing, and exporting to netCDF format.

```{code-cell} ipython3
ds
```

jupyter output cell above shows the coordinates, variables, and related attributes of the datasets and variables. 


## Visualize data 
To quickly visualize the different variables (with the help of the installed matplotlib package not imported but supporting the plot method in Xarray),

```{code-cell} ipython3
import numpy as np
cruises = np.unique(ds.cruise.data)
```

```{code-cell} ipython3
cruises
```

```{code-cell} ipython3
import matplotlib.pyplot as plt

for cruise in cruises:
    yy = ds.where(ds.cruise == cruise,drop=True).stop_latitude.data
    xx = ds.where(ds.cruise == cruise,drop=True).stop_longitude.data
    plt.plot(xx,yy,'o',markersize=1)
    
```

```{code-cell} ipython3
import folium
from folium import plugins

ds.stop_latitude.min().data

lon = (ds.stop_longitude.min().data + ds.stop_longitude.max().data) / 2
lat = (ds.stop_latitude.min().data + ds.stop_latitude.max().data) / 2

fmap = folium.Map(location=[lat, lon], tiles="OpenStreetMap", zoom_start=4)
marker_cluster = plugins.MarkerCluster().add_to(fmap)

for cruise in cruises:
    yy = ds.where(ds.cruise == cruise,drop=True).stop_latitude.data
    xx = ds.where(ds.cruise == cruise,drop=True).stop_longitude.data
    for point in range(0, len(yy)):
        folium.Marker([yy[point],xx[point]], popup=f'Cruise #: {cruise:0.0f}').add_to(marker_cluster)
fmap
```

## Preprocess data
With the help of the Xarray, we can also performed a quick masking on a specific species to see the distribution of the species during the trawling

```{code-cell} ipython3
ds_octo = ds.where(ds.scientific_name=='Octopoda',drop=True)
```

```{code-cell} ipython3
import folium
from folium import plugins

lon = (ds_octo.stop_longitude.min().data + ds_octo.stop_longitude.max().data) / 2
lat = (ds_octo.stop_latitude.min().data + ds_octo.stop_latitude.max().data) / 2

fmap = folium.Map(location=[lat, lon], tiles="OpenStreetMap", zoom_start=5)
marker_cluster = plugins.MarkerCluster().add_to(fmap)

for cruise in cruises:
    yy = ds_octo.where(ds_octo.cruise == cruise,drop=True).stop_latitude.data
    xx = ds_octo.where(ds_octo.cruise == cruise,drop=True).stop_longitude.data
    for point in range(0, len(yy)):
        folium.Marker([yy[point],xx[point]], popup=f'Cruise #: {cruise:0.0f}').add_to(marker_cluster)
fmap
```

## Export to netCDF
To output the dataset, we use the `.to_netcdf()` method
```
ds.to_netcdf('./FRDCPSTrawlLHHaulCatch.nc')
```
