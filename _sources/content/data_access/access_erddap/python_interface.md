---
jupytext:
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.14.4
kernelspec:
  display_name: Python 3 (ipykernel)
  language: python
  name: python3
---

Accessing ERDDAP using Python
===

## Packages 
To use python to access the ERDDAP server directly from your python script or jupyter-notebook, you will need
- ERDDAPY
- Xarray
- netcdf4 

+++

## Extract the data from a ERDDAP server
In this page, we demonstrate how to use the extract/download data directly from a ERDDAP server and perform data processing, visualization, and export data. 

```{tip}
[Understanding of the ERDDAP server and what it provides](errdapData) is highly recommended before reading the following intructions.
```



### Import needed python package
```{code-cell} ipython3
import warnings
import cftime
import numpy as np
import xarray as xr
from dask.diagnostics import ProgressBar
```

```{code-cell} ipython3
warnings.simplefilter("ignore")
```
```{tip}
This line of code is not affecting the execution but just removing some warning outputs that might clutter your notebook. 
However, do pay attention to some of the warnings since they will indicate some deprecation of function and arg/kwarg in future software updates.
```

## Lazy loading the NMME model data from IRI/LDEO Climate Data Library
Like in the previous notebook, we request the metadata from the OPeNDAP server to quickly check the data structure.
Four models provide forecasts till the current and hindcast at the time of generating this notebook.
Here, we only request one model `GFDL-SPEAR` for demonstration. 
However, for a better prediction, it is always better to have an ensemble of models with each model having its multiple runs. 

```{code-cell} ipython3
#### The opendap access
model_list = ['GFDL-SPEAR']
forecast_list = ['http://iridl.ldeo.columbia.edu/SOURCES/.Models/.NMME/.%s/.FORECAST/.MONTHLY/.sst/dods'%model for model in model_list] 

hindcast_list = ['http://iridl.ldeo.columbia.edu/SOURCES/.Models/.NMME/.%s/.HINDCAST/.MONTHLY/.sst/dods'%model for model in model_list] 
```
