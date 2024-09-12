Frequent Ask Questions
===

## Why regional MOM6? How is it different from other operational models?
```{dropdown} Answer
Regional models have some benefits over global models, including being able to represent finer scale features more rapidly. They can also be “tuned” (have their many parameter values adjusted) to better represent conditions in the region of interest. NOAA did not have regional ocean model capability and so building off the expertise in developing global models, MOM6 was then developed for regional applications, particularly for fishery and ocean habitat applications.

## What are differences between historical run, forecast, and projection?
The goal of historical simulations is to match what happens in the actual ocean over time. 
Regional models use observationally-based fields (usually from [atmosphere and ocean reanalyses](reanalyses), which combine observations from multiple platforms with a model) as boundary conditions for the regional ocean model. For regional MOM6, the simulations currently begin in 1993 and continue to the near-present (ocean reanalyses generally end a year or two before the present date). Historical runs can be used to test the accuracy of the regional model, although they have many other uses.

In a forecast, an initial estimate of the actual ocean conditions are used to have the regional model close to conditions in the real world.  Then the model is integrated forward in time. For the regional MOM6 forecasts, the boundary conditions are currently obtained from [SPEAR, a global forecast model](https://www.gfdl.noaa.gov/spear/).  The plan for CEFI is to make “seasonal” forecasts, which extend out to a year, initialized four times per year. There are also plans to make decadal forecasts out to 10 years once a year.  The skill of these forecast systems will be validated against observations. In addition to model error and the difficulty of matching real-world conditions at the start of the forecast, the chaotic nature of the climate system will cause forecast accuracy to decrease with time. So these forecasts will be made as ensembles, with 10 runs started at a given time, to provide a measure of uncertainty in the forecasts.

The critical aspect of a projection, is the change in the climate system due to the increase in greenhouse gasses due to human activity. The conditions at the start of a simulation are much less important than the greenhouse gas induced changes (“forcing”). CO<sub>2</sub> and concentrations of other greenhouse gasses can be incorporated into climate models from observations. In projections different “scenarios” are used that provide different estimates on how greenhouse gasses and other factors, such as land use, change with time. For CEFI, the plan is to use fields from different global climate models and different scenarios to provide the boundary conditions for regional MOM6. These simulations will extend to 2100.
```

(reanalyses)=
## What is reanalyses?
```{dropdown} Answer
Reanalysis is a method that gives us the most comprehensive view of past weather and climate conditions. It combines observations and past weather forecasts using modern forecasting models to create a complete and consistent global picture over time, like a map without any gaps in time and space.

**Why it matters:** Reanalysis is crucial for understanding climate change and current weather extremes. Observations of the Earth system are not always evenly distributed and can contain errors even after entering the satellite era. Reanalysis helps fill these gaps in space and provides a consistent view of the Earth’s state at any given time, reducing any misleading interpretation of signal changes.

**How it’s done:** Reanalysis merges past weather forecasts and observations through a process called data assimilation. This process is similar to how daily weather forecasts are made. It starts with an analysis of the current state of the Earth system, which is a blend of observations and a short-range forecast based on the previous analysis. Reanalyses are typically produced at a lower resolution than current weather forecasts and use the same modern data assimilation system and forecasting model throughout the reanalysis period. Before a new reanalysis is produced, efforts are made to improve the quality and availability of past observational data. This can involve digitising old records and reprocessing existing satellite records. As reanalyses are produced, they undergo careful quality control and their reliability is assessed by comparing them with reanalyses produced at other institutes.
```

## What is COBALT? And how is it related to the regional mom6?
```{dropdown} Answer
Carbon, Ocean Biogeochemistry and Lower Trophics (version 2 COBALTv2, with enhancements for regional MOM6), is a biogeochemical model within the ocean that includes multiple chemical constituents for carbon, nitrogen, phosphorus and silicate. In addition, it includes variables representing classes of phytoplankton and zooplankton. There are a total of 40 variables. In many of the CEFI simulations COBALT will be coupled with the MOM6, so that the physical model variables from MOM6 will influence those in COBALT (e.g. temperature impact on metabolism) and COBALT values will influence those in MOM6 (the influence of plankton on the absorption of solar radiation).
```
