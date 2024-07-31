Regional MOM6 introduction
===

##  What is regional MOM6
The [Modular Ocean Model (MOM)](https://www.gfdl.noaa.gov/mom-ocean-model/) was originally developed at the NOAA Geophysical Fluid Dynamics Lab several decades ago as a global physical ocean model, which simulates ocean currents, temperatures and salinity. The model also includes the physics for the formation and melting of sea ice. The current version of the global model is version 6 (MOM6, [described here](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2019MS001726)). 
To understand more about the different versions of MOM, here is a [great documentation](https://mom-ocean.github.io)
The regional version of MOM6, was recently developed with the primary goal of supporting CEFI to focus on high-resolution simulations of various distinct regions. While it has much of the same physics as the global model, a key difference is that boundary conditions along the edge of the regional model must be provided. This is a complex task and took a while to develop.  A description of how the boundary conditions are implemented can be found [here](https://gmd.copernicus.org/articles/16/6943/2023/) for the northwest Atlantic region.

There are numerous online resources available for both MOM6 and its regional variant. These resources provide valuable information, tutorials, and documentation to assist users in effectively utilizing these models for their research needs.
- [MOM6 readthedoc for model design](https://mom6.readthedocs.io/en/main/)
- [Regional MOM6 readthedoc for running simulation](https://cefi-regional-mom6.readthedocs.io/en/latest/Introduction.html)
- [Python package for generating regional configuration for MOM6 - ](https://regional-mom6.readthedocs.io/en/latest/)

---

##  Table of Content of Regional MOM6
```{tableofcontents}
```
