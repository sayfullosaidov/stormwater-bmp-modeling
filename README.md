# Stormwater BMP Modeling

This repository contains Python-based analysis and modeling of stormwater Best Management Practices (BMPs).

Stormwater BMPs are systems designed to manage runoff by storing, slowing, infiltrating, or releasing water during and after rainfall events. This project uses monitored rainfall, water-level, inflow, and outflow data to investigate how different BMPs respond to storm events.

## Objectives

The main goals of this repository are to:

- clean and organize field monitoring data,
- identify and analyze individual storm events,
- compare rainfall, inflow, storage, and outflow behavior,
- perform event-scale water-balance checks,
- develop and test different hydrologic modeling approaches,
- calibrate model parameters using observed data,
- compare modeled and measured hydrographs,
- evaluate the strengths and limitations of different modeling methods.

## Data

Depending on the monitoring site, available data may include:

- rainfall depth and intensity,
- inflow discharge,
- outlet discharge,
- water level,
- sensor timestamps,
- contributing drainage area.

The monitoring records are processed and synchronized onto common time intervals before analysis and modeling.

## Modeling

Different BMP sites may require different modeling approaches depending on the available data and the physical behavior of the system.

Models explored in this repository may range from simple conceptual storage models to more detailed hydrologic or hydraulic approaches.

The purpose is not necessarily to reproduce every physical component of a BMP individually, but to determine which modeling approaches can reasonably represent observed system behavior.

## Event Analysis

Before fitting a model, observed data are examined using basic hydrologic checks.

For example, rainfall volume over a contributing drainage area can be estimated as

$$
V_{\mathrm{rain}} = P A
$$

where:

- $V_{\mathrm{rain}}$ is rainfall volume,
- $P$ is total rainfall depth,
- $A$ is the contributing drainage area.

Observed discharge volume can be estimated numerically from the measured hydrograph:

$$
V_{\mathrm{out}}
\approx
\sum Q_i \Delta t
$$

These checks help identify possible issues with drainage-area assumptions, sensor measurements, event selection, or model inputs before calibration.

Each BMP site can have its own notebook and documentation describing the available data, preprocessing steps, modeling approach, and results.

## Tools

The analysis primarily uses:

- Python
- pandas
- NumPy
- Matplotlib
- Jupyter Notebook / Google Colab

Additional modeling tools may be incorporated as the project develops.

## Status

This is an ongoing project exploring different approaches for modeling monitored stormwater BMPs. Methods and site analyses will be expanded as additional data and modeling approaches are evaluated.
