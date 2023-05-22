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

Batch access (ex: gliders)
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
[Understanding of the ERDDAP server and what it provides](erddapData) is highly recommended before reading the following intructions.
```

## Import python packages

```{code-cell} ipython3
import xarray as xr
from erddapy import ERDDAP
```

- [**xarray**](https://docs.xarray.dev/en/stable/getting-started-guide/why-xarray.html) is used for data processing and netCDF file output. 
- [**erddapy**](https://ioos.github.io/erddapy/00-quick_intro-output.html) is used to access the ERDDAP server.

Both package-webpages have more detail explanation on its full range of functionalities. 
Here we will mainly focusing on getting the data to be displayer and downloaded.


## Access IOOS Glider DAC (TableDAP) data
In this demostration, we will be getting the glider data from [IOOS Glider Data Archived Center](https://gliders.ioos.us/erddap/tabledap/allDatasets.html)

Firstly, the way to use the **erddapy** is to setup the destination ERDDAP server as an object in python through `ERDDAP` ([a python class](https://docs.python.org/3/tutorial/classes.html))

```{code-cell} ipython3
#### access the ERDDAP server 
e = ERDDAP(
    server="https://gliders.ioos.us/erddap/",             # The URL that the ERDDAP server has
    protocol="tabledap",                                  # The data type (griddap or tabledap)
    response="opendap",                                   # different output data type that provided by ERDDAP server       
)
```

By executing the above code block, we have already setup the connection with the desired ERDDAP server. 
To request a the dataset list on the server, we need to set the `dataset_id = allDatasets`(e.g. https://gliders.ioos.us/erddap/tabledap/allDatasets.html).

To set the `dataset_id`, execute

```{code-cell} ipython3
# set the dataset id name 
e.dataset_id = "allDatasets"
```

## Download data list
Now, all the setting for downloading the dataset list is complete. By executing the following, we convert the list into a pandas dataframe object that contain all the dataset info on the ERDDAP server

```{code-cell} ipython3
df = e.to_pandas()
```

Let's take a peak at the first five glider deployments

```{code-cell} ipython3
df.head(5)
```

Now, let us create a list of dataset_id. This helps if user want to download all datasets on the server.

```{code-cell} ipython3
dataset_ids = []
for dataset_id in df['datasetID']:
    if dataset_id != 'allDatasets':
        dataset_ids.append(dataset_id)
```

The first five `dataset_id` is shown below.

```{code-cell} ipython3
dataset_ids[:5]
```

## Picking one dataset to investigate on the fly

```{code-cell} ipython3
# e.dataset_id = 'ce_311-20190703T1802-delayed'    # feel free to uncomment and test
# e.dataset_id = 'amelia-20201015T1436'            
e.dataset_id = 'UW685-20230125T0000'             # feel free to uncomment and test
df = e.to_pandas()
ds = df.to_xarray()
```

```{note}
Here, we try to extract the data from the server by first converting it into a Pandas dataframe then into a Xarray dataset. A direct `e.to_xarray()` would result in another data structure which is harder to visualize in this notebook.

Converting from the dataframe to the xarray helps us to convert into a gridded dataset in the later on preprocessing step. But if that is not needed, `ds = df.to_xarray()` is not a necessary step to extract the dataset from the server.
```


### Preprocessing the data
To focus on the vertical profile, we first remove row that does not contain the depth value. 
```{code-cell} ipython3
ds_transect = ds.where(ds['depth (m)'].notnull(),drop=True)   # only preserve the profile related data
```
The original dataset structure is
```{code-cell} ipython3
ds
```
After the `.where` filtering, the dataset structure becomes
```{code-cell} ipython3
ds_transect
```

This imidiately decrease the table from 90984 rows to 39661 rows.

+++

### Creating 3D plotting function
To take a quick look on the glider vertical profile, we construct a plotting function using the matplotlib package which could avoid rewriting the plotting code over and over.

```{code-cell} ipython3
import matplotlib.pyplot as plt

def plot_3d_view(ele_angle=-140,hori_angle=60):
    """
    This function is designed for creating axe object) for plotting the 
    3D scatter plot.

    Parameters
    ----------
    ele_angle : integer
        elevation angle of viewing the 3D scatter plot
    hori_angle : integer
        horizontal angle of viewing the 3D scatter plot
    Returns
    -------
    ax : matplotlib axe object
        the axe object that can apply scatter3D method 

    Raises
    ------
    """
    fig = plt.figure(figsize=(5,5))
    ax = plt.axes([0,0,1.5,1],projection = '3d')
    ax.view_init(ele_angle, hori_angle)
    ax.set_xlabel('Longitude')
    ax.set_ylabel('Latitude')
    ax.set_zlabel('Depth')
    return ax
```

### Plotting a subset of the dataset and focusing on single variables
- temperature profile along the glider path

```{code-cell} ipython3
ds_part = ds_transect
varname = 'temperature (Celsius)'
zname = 'depth (m)'
yname = 'latitude (degrees_north)'
xname = 'longitude (degrees_east)'
```

```{code-cell} ipython3
ax2 = plot_3d_view(ele_angle=-140,hori_angle=60)
p = ax2.scatter3D(ds_part[xname],
                  ds_part[yname],
                  ds_part[zname],
                  c=ds_part[varname],      # color value of individual points is taken from their heights
                  cmap="viridis"                           # the color mapping to be used. Other example options: winter, autumn, ...
                )
# ax2.invert_zaxis()
ax2.invert_xaxis()
cbar = plt.colorbar(p)
cbar.set_label(varname)
```

- salinity profile along the glider path

```{code-cell} ipython3
varname = 'salinity (0.001)'
zname = 'depth (m)'
yname = 'latitude (degrees_north)'
xname = 'longitude (degrees_east)'
```

```{code-cell} ipython3
ax2 = plot_3d_view(ele_angle=-160,hori_angle=110)
p = ax2.scatter3D(ds_part[xname],
                  ds_part[yname],
                  ds_part[zname],
                  c=ds_part[varname],      # color value of individual points is taken from their heights
                  cmap="viridis"                           # the color mapping to be used. Other example options: winter, autumn, ...
                )
# ax2.invert_zaxis()
ax2.invert_xaxis()
cbar = plt.colorbar(p)
cbar.set_label(varname)
```

### Showing the geopgraphic location of the glider path

Using the FOLIUM package, we can plot a interactive map in the notebook environment to investigate the path of the glider.

```{code-cell} ipython3
import folium
import numpy as np

lon = ds_part[xname].data
lat = ds_part[yname].data


fmap = folium.Map(location=[(np.min(lat)+np.max(lat))/2, (np.min(lon)+np.max(lon))/2], tiles="OpenStreetMap", zoom_start=8)
points = [[lat[i],lon[i]] for i in range(len(lon)) ]
folium.PolyLine(points, color='red', weight=2.5, opacity=0.4,popup=f'{dataset_id}').add_to(fmap)
folium.Marker([lat[0],lon[0]], popup=f'start').add_to(fmap)
folium.Marker([lat[-1],lon[-1]], popup=f'end').add_to(fmap)
    
fmap
```

## Converting the table data to gridded data

In the following steps, we demostrate how to convert a point observation from glider to a gridded data.
The gridded dataset will have two dimensions - time as first dimension and depth as the second dimension.


By using the `numpy.unique` method, we first establish the two dimensions and the assoicated arrays.
```{code-cell} ipython3
import numpy as np
import pandas as pd

# idealy/theoretically the three array should have same len (first dimension)
# lat = np.unique(ds_transect['latitude (degrees_north)'].data)
# lon = np.unique(ds_transect['longitude (degrees_east)'].data)
time = np.unique(ds_transect['time (UTC)'].data)
dtime = pd.to_datetime(time)
```

```{code-cell} ipython3
# vertical profile (second dimension)
depth = np.unique(ds_transect['depth (m)'].data)
```

Then, we create an empty `xr.DataArray` to later put the interpolated values into the corresponding dimensions.
```{code-cell} ipython3
# create 2D gridded array for vertical profile along the glider trajectory
da_transect = xr.DataArray(
    coords={
        "depth": depth,
        "time": dtime.values,
        # "lon": ("time", lon),  # place holder not real lon at the associated time
        # "lat": ("time", lat),  # place holder not real lat at the associated time
    },
    dims=["depth", "time"],
)
da_transect = da_transect.rename('var')
```

To convert the table data into gridded data, we perform the following processes
1. for each single time profiling, we take all the vertical measurement
2. for each single time profiling, we average the measurement on the same vertical level
3. if multiple location is registered during the vertical profiling, we use the first recorded location as the profiling location
4. the veritical profile is linearly interpolated to make every vertical profiling to have the same number of grid

```{code-cell} ipython3
# we minimized the number of time profiling (first 10 time stamp) that needed to be processed to gridded data in this notebook (efficiency)
print(f'processing {varname}')
for i in range(len(time[:10])):
    print(time[i])
    loc_time = time[i]
    
    # only preserve single time (mid point time during the profiling)
    ds_temp = ds_transect.where((ds['time (UTC)'] == loc_time),drop=True)
    ds_temp = ds_temp.assign_coords({'depth':ds_temp['depth (m)']})
    
    # group mean the value for up and down profiling (single depth single value)
    ds_temp = ds_temp.groupby('depth (m)').mean()
    
    # create profile data array to store profiling at one location
    da_var = xr.DataArray(
        ds_temp[varname].data,
        coords={"depth": ds_temp['depth (m)'].data},
        dims=["depth"]
    )
    da_var = da_var.rename('var')

    # put the single profiling to the 2D gridded dataarray
    da_var = da_var.interp(
        depth=depth,
        method="linear",
        kwargs={"fill_value": np.nan},
    )
    da_transect[:,i] = da_var 
```

The gridded dataset that has the interpolated values put in is
```{code-cell} ipython3
da_transect
```

## Plotting the gridded data

```{code-cell} ipython3
da_transect.where(da_transect.notnull(),drop=True).plot(yincrease=False, x='time', y='depth')
```
