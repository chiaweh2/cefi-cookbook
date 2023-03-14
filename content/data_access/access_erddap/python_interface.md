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

# Accessing ERDDAP using Python




## Predicting marine heatwaves
Using the NMME (North American Multi-Model Ensemble), [Jacox et al., 2022](http://doi.org/10.1038/s41586-022-04573-9) demonstrate the possibility of predicting the marine heatwaves under a monthly time scale with the lead time up to a year. 
The [marine heatwaves portal](https://psl.noaa.gov/marine-heatwaves/) forecast hosted at NOAA/PSL website is based on the calculation show in this notebook.

### Goals in the notes 
- the NMME model data from [IRI/LDEO Climate Data Library](http://iridl.ldeo.columbia.edu/SOURCES/.Models/.NMME/)
- Calculate the ensemble mean climatology for each model based on hindcast
- Calculate the SST anomaly in the forecast
- Calculate the threshold based on the SST anomaly
- Calculate the marine heatwave in the forecast
- Show result

+++

```{note}
The following example is based on the paper [Jacox et al., 2022](http://doi.org/10.1038/s41586-022-04573-9). 
```

## Extract the data from the IRI/LDEO Climate Data Library OPeNDAP server
In this notebook, we demonstrate how to use the [NMME model](https://www.cpc.ncep.noaa.gov/products/NMME/) to generate the marine heatwaves prediction.
The dataset is currently hosted on [IRI/LDEO Climate Data Library](http://iridl.ldeo.columbia.edu/SOURCES/.Models/.NMME/).

```{tip}
The OPeNDAP server on the [IRI/LDEO Climate Data Library](http://iridl.ldeo.columbia.edu/SOURCES/.Models/.NMME/) also has a data extraction limit. 
For solving some of the limit issues, there are some great discussions on this [GitHub issue](https://github.com/pangeo-data/pangeo/issues/767).
To summarize, user sometime will need to play a bit on the chunk size to find the optimal download scheme.
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
