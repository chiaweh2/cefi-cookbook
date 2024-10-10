Frequently Ask Questions
===

## Why regional MOM6? How is it different from other operational models?
```{dropdown} Answer
Regional models have some benefits over global models, including being able to represent finer scale features more rapidly. They can also be “tuned” (have their many parameter values adjusted) to better represent conditions in the region of interest. While regional ocean models including the Regional Ocean Modeling System ([ROMS](https://www.myroms.org)) and Finite Volume Coastal Ocean Model  ([FVCOM](https://csdms.colorado.edu/wiki/Model:FVCOM)) have been developed and used for many years, NOAA did not have regional ocean model capability. Building off the expertise in developing global models, the regional version of MOM6 has been developed particularly with fishery and ocean habitat applications in mind.
```

## Are regional models the same as climate models?
```{dropdown} Answer
The climate system is often simulated by coupling models representing different parts of the earth system together.  Common components include the atmosphere, ocean, sea ice, land, land vegetation, and ocean biogeochemistry.  Terminology varies depending on which components are included:
- Earth system model (ESM): Earth system models couple all of the components listed in the previous section. They are global and their dynamics are almost entirely emergent from their internal dynamics; in general, the only inputs provided to these models are solar forcing, volcanic aerosols, and human-produced greenhouse gas emissions.
- General circulation model (GCM, also sometimes called global climate models): These are similar to ESMs, but without ocean biogeochemistry and a simplified version of vegetation on land.  (In the past, the term “general circulation model” was used to describe just the atmosphere or ocean component models)
- Atmospheric model : can be both global or regional where the sea surface temperatures are specified as boundary conditions with an interactive land component.
- Ocean model: Ocean models remove the atmospheric and land components and focus only on the ocean; they often include sea ice and ocean biogeochemistry as well.  These are less computationally intensive than fully coupled ESMs, and also provide extra  flexibility in experimental design since the atmospheric components are provided as user inputs.  They can be very useful to address research questions where the feedback of ocean dynamics on the atmosphere can be ignored or approximated via input setup.
- Regional ocean model: A regional ocean simulates only a specific section of the globe.  This adds extra lateral boundaries to the setup relative to a global model, which introduces additional computational complexities.  However, the limited spatial extent allows simulation at higher resolution than a global model given the same computing resources.  Regional models also allow for tailoring of input model components and input parameters to capture dynamics specific to a region that may not be applicable globally.
```

## Is regional MOM6 the same as global MOM6?
```{dropdown} Answer
[The Modular Ocean Model, version 6 (MOM6)](https://www.gfdl.noaa.gov/mom-ocean-model/) is the ocean component of the NOAA Geophysical Fluid Dynamics Laboratory (GFDL)’s earth system model (ESM4). This model has been developed over several decades and is one of the world’s premier ESMs. The MOM6 ocean model simulates physical ocean dynamics like ocean currents, temperature, and salinity, and can be coupled to a sea ice model (SIS2) that simulates formation and melting of sea ice and an ocean biogeochemical model (COBALT) that simulates nutrient cycling and lower trophic level dynamics.

While the global version of MOM6 has existed for many decades, the regional version has been  developed much more recently and is still being improved. Simulating open lateral boundaries is a complex task, and it took time to add these capabilities in a manner compatible with the global MOM6 configuration.  A description of how these boundary conditions are implemented can be found in the [documentation paper](https://gmd.copernicus.org/articles/16/6943/2023/) for the northwest Atlantic implementation. Both the global and regional implementations use the same underlying code base. 
```

## Are the boundary conditions part of a regional model?
```{dropdown} Answer
A regional ocean model always requires external input to prescribe what is happening at the surface and lateral boundaries; that input usually comes from the output of a larger- and coarser-scale global model or a [reanalysis](reanalyses), which combines a model with observations.  These boundary conditions play a strong driving role in any simulation, and a regional model will inherit some of both the skill and biases of its parent model/[reanalysis](reanalyses).  A regional model is more than just a high-resolution filter for the parent model; it can resolve dynamics not possible at a coarser scale, and also can add new processes not present in the parent (for example, extra biological complexity).  This can alleviate biases from the parent model.  But at the same time, some biases can be amplified in the regional model output.  The resulting features in a regional model will always be a combination of the parent model’s dynamics and its own internal dynamics.
```

## What are differences between historical run, forecast, and projection?
```{dropdown} Answer
Different types of regional simulations can be run by pairing a regional MOM6 domain with different types of parent models/datasets for its atmospheric and boundary condition forcing.  The terminology for these different simulation types -- historical, forecast, projection, etc. -- is not standardized across the field and can be confusing.  Here's a brief summary of the CEFI simulations and our chosen terminology:

- Historical simulations: CEFI's historical simulations attempt to simulate real-world conditions in the recent past. They derive their input forcing from a global [reanalysis](reanalyses).  Reanalyses combine model dynamics and observations using a process known as data assimilation. Regional historical runs can be used to measure the skill of the model compared to observations.  They also play many roles in research and ecosystem management: to fill in spatiotemporal gaps in observations, provide a physical basis to drive fisheries and other ecosystem models, initialize forecasts, and many more.  Note that our historical simulations do not themselves assimilate observations; they are simply forced by a data-assimilative parent model.  Sometimes historical simulations are referred to as “hindcasts”.<br><br>
Note on terminology - In some contexts, "historical" ESM or climate model simulations can refer the historical experiment output of an earth system model intercomparison project (e.g., [CMIP6](https://doi.org/10.5194/gmd-9-1937-2016)). Unlike a reanalysis model, these ESMs are not directly tied to observations on initialization. They usually start from a simulation designed to bring the internal dynamics into equilibrium under pre-industrial conditions (i.e. letting the model approach its long-term average climate). They do not assimilate data and are tied to specific time periods only by prescribed greenhouse gas emissions and atmospheric aerosols. A skillful ESM/GCM will capture real-world statistical variability across interannual and decadal scales, but will not have a year-to-year match to the real world.  For example, they will produce warm or cold events like ENSO, but not specific heat waves when they occur in the real world.  The CEFI suite does not currently include this type of CMIP historical experiment simulation.<br><br>
    
- Short-term forecasts: Regional forecast simulations derive their atmospheric and boundary forcing from a global seasonal forecast model.  CEFI uses the seasonal simulations from [SPEAR](https://www.gfdl.noaa.gov/spear/), GFDL's MOM6-based seasonal and decadal forecasts.  Global earth system model seasonal forecasts are initialized from real-world conditions, then integrated forward in time in a freely-evolving manner for anywhere from a few months to a decade.  The CEFI suite includes 1-year seasonal forecasts, initialized 4 times per year.<br><br>

- Long-term forecasts: Decadal forecasts that are initialized once per year and extend to 10 years will be added.<br><br>
Forecast ensembles - Due to the chaotic nature of the climate system, very small differences in conditions at one time can lead to large differences in future values.  The SPEAR simulations account for this by running multiple forecast simulations with slight differences in their initial conditions, producing an ensemble of forecasts that can be used to quantify the uncertainty of predictions. The CEFI regional seasonal forecasts downscale 10 of these ensemble members.<br><br>
Note on terminology - Forecasts are usually run starting from near-present conditions to predict the future.  But they can also be initialized from past conditions. This type of forecast is sometimes referred to as a retrospective forecast/reforecast.  These differ from the historical simulations because they are not tied to real-world data during the simulation period, only at their initialization time.  The primary purpose of these simulations is to assess the skill of a forecast model by comparing the forecasts to real-world data (or to a [reanalysis](reanalyses) or historical simulation).<br><br>

- Long-term projections: Long-term projections focus on predicting the change in the climate system over time scales of 100 years.  On these time scales, the conditions at the start of the simulation are much less important than in short-term forecasts.  Instead, changes in long-term drivers, especially the concentrations of CO2 and other greenhouse gasses in the atmosphere, control the outcomes.  ESM projections are a key part of Coupled Model Intercomparison Projects (CMIP), and encompass a wide variety of simulations with different assumptions about the future trajectory of greenhouse gas emissions, land use, etc. The CEFI suite will include downscaled versions of selected simulations across parent models and scenarios.  These simulations will extend to 2100.<br><br>
```

## What is COBALT? And how is it related to the regional mom6?
```{dropdown} Answer
Carbon, Ocean Biogeochemistry and Lower Trophics (COBALT) (version 2 [COBALTv2](https://agupubs.onlinelibrary.wiley.com/doi/10.1029/2019MS002043), with enhancements for regional MOM6) is the ocean biogeochemical model associated with MOM6.  COBALTv3 includes 40 state variables that simulate nutrient cycling for carbon, alkalinity, oxygen, nitrogen, phosphorus, iron, silica, calcium carbonate, and lithogenic minerals, as well as the food web dynamics of phytoplankton and zooplankton.

The COBALT source code is included within the MOM6 component, and when active there is two-way feedback between ocean and biogeochemical state variables (for example, temperature influences many of the biological rate parameters, while phytoplankton biomass impacts solar radiation reaching and hence heating the water column).
```

## What is z* vertical coordinate? Why not use the regular height coordinate?
```{dropdown} Answer
The regional MOM6 simulations use z* as the vertical coordinate. It’s essentially a height (z) based system but shares some similarity with a terrain following (σ) coordinate system. Indeed, z*  only differs from z when the free-surface elevation is non-zero.The  coordinate system transforms the moving boundary problem of the oceans free surface into a fixed domain.

Alistair Adcroft, A., Jean-Michel Campin, J.-M., 2004: Rescaled height coordinates for accurate representation of free-surface flows in ocean circulation models, Ocean Modelling, 7, 3–4,
269-284, [https://doi.org/10.1016/j.ocemod.2003.09.003](https://doi.org/10.1016/j.ocemod.2003.09.003).

Note that this is the model coordinate system - output is archived at set depth levels. 
```

(reanalyses)=
## What is reanalysis?
```{dropdown} Answer
Reanalysis is a method that gives us the most comprehensive view of past weather and climate conditions. It combines observations and past weather forecasts using modern forecasting models to create a complete and consistent global picture over time, like a map without any gaps in time and space.

**Why it matters:** Reanalysis is crucial for understanding climate change and current weather extremes. Observations of the Earth system are not always evenly distributed and can contain errors even after entering the satellite era. Reanalysis helps fill these gaps in space and provides a consistent view of the Earth’s state at any given time, reducing any misleading interpretation of signal changes.

**How it’s done:** Reanalysis merges past weather forecasts and observations through a process called data assimilation. This process is similar to how daily weather forecasts are made. It starts with an analysis of the current state of the Earth system, which is a blend of observations and a short-range forecast based on the previous analysis. Reanalysis is typically produced at a lower resolution than current weather forecasts and use the same modern data assimilation system and forecasting model throughout the reanalysis period. Before a new reanalysis is produced, efforts are made to improve the quality and availability of past observational data. This can involve digitising old records and reprocessing existing satellite records. As reanalysis is produced, it undergo careful quality control and the reliability is assessed by comparing with reanalyses produced at other institutes.
```