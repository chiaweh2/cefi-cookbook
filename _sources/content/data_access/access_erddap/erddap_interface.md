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

ERDDAP Server Interface
===

## Landing Page
Usually, the ERDDAP page would look a lot alike.
If the institutes/agencies do not specified the related data that is hosted at the front page, it is sometime a bit confusing that which ERDDAP server you have landed on.
To give an example, here are three ERDDAP servers that look similar but are hosting very different datasets.
- [NOAA IOOS Sensors (Integrated Ocean Observing System)](http://erddap.secoora.org/erddap/index.html)
- [Southern California Coastal Ocean Observing System](http://erddap.axiomdatascience.com/erddap/index.html)
- [BCO-DMO - Biological and Chemical Oceanography Data Management Office at Woods Hole Oceanographic Institution (WHOI).](https://erddap.bco-dmo.org/erddap/index.html)

```{important}
The first two ERDDAP servers look almost identical if you do not pay attension to the small differences on the landing page. 
Sometime the only way to seperate one from another is to go to the "View a List of All Datasets" link that is shown on the top right of every landing page.
The third ERDDAP server is not hosted by NOAA but WHOI which is more obvious in terms of landing page differences due to the top logo indicating the institution that is maintaining the server.

```
## Data Listing Page
When clicking on the "View a List of All Datasets", the ERDDAP server will show the user a tabulated list of data that is hosted on the server. 
A example page hosted by [NOAA NMFS SWFSC ERD](https://coastwatch.pfeg.noaa.gov/erddap/info/index.html?page=1&itemsPerPage=1000) shows the tabulated list.
All dataset that is hosted will be showing in the list. 

Usually the data can be seperated to two types
- **TableDAP Data**
- **GridDAP Data**

**TableDAP** means the data is in the tabulated format (think of it as excel/google spread sheet with each row containing a data point).
**GridDAP** means the data is in the gridded format (think of it as netCDF with longitude, latitude, and time axises for each data point).
The `data` link shown on each row under either `TableDap Data` or `GridDap Data` column represents the type of the data of that row.

## Downloading individual dataset
By click on the `data` link under the ["GridDAP Data/TableDAP Data"](https://coastwatch.pfeg.noaa.gov/erddap/griddap/index.html?page=1&itemsPerPage=1000) column, one will be able to see the detail of each dataset.
The page would look like [this](https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplAmsreSstMon.html) (Using AMSRE Model Output, obs4MIPs NASA-JPL, Global, 1 Degree, 2002-2010, Monthly dataset as a example).
The data page provide a easy way to subset the dataset.
The scroll bar shows the available dimension(GridDap)/row(TableDap) for user to set the desired range to subset the data.
After the subsetting, user can choose the desired file type and click submit.
This will download the file to your local machine throught the browser. 
````{tip}
For more advance usage of downloading dataset in batch using the command line or other computer language, ERDDAP server also provide a way to request a data subset via a specially formed URL.
To get the URL, one can press the `Just generate the URL` button on the page to get the specially formed URL.
With the command below, user can contruct the command in any language to perform the batch download using `curl`. A more detail description of using curl on ERDDAP URL is [here](https://apdrc.soest.hawaii.edu/erddap/files/documentation.html)
```{code-cell} ipython3
curl -g "erddapUrl" -o /path/file.nc
```
````


## Visualizing individual dataset
By clicking on the the `graph` link under the ["Make A Graph"]((https://coastwatch.pfeg.noaa.gov/erddap/griddap/index.html?page=1&itemsPerPage=1000)) column, one will be able to visualize the dataset. 
The server provide the same subsetting method for the visualization.  

## Quick view of metadata
When entering the `data` or `graph` link, the metadata of the specific dataset is always shown in the bottom of the two pages. 
However, there is another way to request the metadata from a URL directly. 
(Using the [Aquarius Sea Surface Salinity, L3 SMI, Version 5, 1.0°, Global, 2011-2015, 3-
Month](https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplAquariusSSS3MonthV5.html) data as example)
By changing the data page URL from
```{code-cell} ipython3
https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplAquariusSSS3MonthV5.html 
```
to
```{code-cell} ipython3
https://coastwatch.pfeg.noaa.gov/erddap/griddap/jplAquariusSSS3MonthV5.das
```
The metadata will show on the browser directly.
This is very similar to the OPeNDAP server approach of getting the Data Attribute Structure (DAS) for a hosted dataset.


---

## Available ERDDAP servers
Since there are many available ERDDAP servers, a list of deployed servers is provided by [NOAA](https://coastwatch.pfeg.noaa.gov/erddap/download/setup.html#organizations).   

