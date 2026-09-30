# Sherrerd Field Linear Reservoir Model

## Overview

This project develops a simple rainfall–outflow model for the Sherrerd Field stormwater BMP.

Rather than explicitly modeling individual soil layers, gravel storage, underdrain pipes, and the outlet structure, the BMP is represented as a single effective storage reservoir.

The model is used to investigate whether a simple storage-based representation can reproduce the observed outlet response during monitored storm events.

## Conceptual Model

The BMP is represented as:

**Rainfall → Effective BMP Storage → Outlet Flow**

The reservoir water balance is:

\[
\frac{dS}{dt} = P(t) - Q(t)
\]

where:

- \(S\) is effective BMP storage,
- \(P(t)\) is rainfall input,
- \(Q(t)\) is modeled outlet flow.

Outflow is represented using a threshold linear reservoir:

\[
Q(t) = k\max(S-S_0,0)
\]

where:

- \(k\) is the reservoir drainage coefficient,
- \(S_0\) is the effective storage threshold before measurable outflow begins.

This threshold allows the model to represent the ability of the BMP to store and infiltrate rainfall before producing outlet discharge.

## Data

The model uses monitored storm-event data consisting of:

- rainfall intensity,
- event time,
- measured outlet discharge.

Observed rainfall provides the model input, while measured outlet flow is used for calibration and model evaluation.

## Calibration

Two effective parameters are calibrated:

- **\(k\)** — controls how quickly the BMP drains once the storage threshold is exceeded,
- **\(S_0\)** — represents the effective storage available before outlet flow begins.

A simple grid search is used to identify the parameter combination that minimizes the difference between modeled and observed outlet flow.

## Model Evaluation

Model performance is evaluated using:

- observed versus modeled hydrographs,
- root mean square error (RMSE),
- Nash–Sutcliffe Efficiency (NSE),
- total outflow volume error.

If additional monitored storm events are available, they can be used for independent model validation without changing the calibrated parameters.

## Purpose

The goal of this project is not to reproduce every physical component of the BMP. Instead, it tests whether the observed rainfall–outflow behavior can be explained using a simple and interpretable reservoir model with only a small number of parameters.

This provides a compact framework for analyzing BMP storage, drainage response, and storm-event performance while remaining directly constrained by field observations.
