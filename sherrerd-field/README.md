# Sherrerd Field Linear Reservoir Model

Sherrerd Field is an athletic field at Princeton University with a subsurface drainage system that collects and conveys stormwater runoff from the field and surrounding area.

When systems like this are designed to retain, slow, infiltrate, or control runoff to meet stormwater-management criteria, they can function as **Best Management Practices (BMPs)** or forms of **green infrastructure**.

This project uses available rainfall, water-level, and outlet-flow sensor data to investigate how the Sherrerd Field drainage system responds during storm events. A simplified hydrologic simulation is then used to test whether the observed behavior can be represented using an effective storage model.

The goal is not to reproduce every physical component of the drainage system individually, but to evaluate the system's overall rainfall--storage--outflow response using monitored field data. To represent the system in a simple and interpretable way, the BMP is modeled using a **linear reservoir model**.

Instead of modeling each physical component separately, such as the soil, gravel layer, drainage pipes, and outlet structure, the entire BMP is represented as one effective storage reservoir.

In simple terms, the model treats the BMP like a temporary holding system: rainfall adds water to storage, the stored water builds up, and once enough water is present, it is released through the outlet.

Conceptually:

**Rainfall → Storage → Outlet Flow**

### Water Balance

The change in storage is described by:

$$
\frac{dS}{dt} = P(t) - Q(t)
$$

where:

- $S$ = effective storage
- $P(t)$ = rainfall input
- $Q(t)$ = modeled outlet flow

### Outlet Relationship

Outflow begins once storage exceeds an effective storage threshold, $S_0$:

$$
Q(t) = k\max\left(S(t)-S_0,0\right)
$$

where:

- $S_0$ = storage threshold before outlet flow begins
- $k$ = drainage coefficient controlling how quickly stored water is released

If

$$
S \leq S_0
$$

then

$$
Q = 0
$$

and no outlet flow is produced.

If

$$
S > S_0
$$

then outlet flow increases as storage above the threshold increases.

### Numerical Solution

The storage equation is solved through time using the **Forward Euler method**:

$$ S_{n+1}=S_n+\left(P_n-Q_n\right)\Delta t $$

At each timestep, the model:

1. adds rainfall to storage,
2. calculates outlet flow based on the current storage,
3. removes that outflow from storage,
4. moves to the next timestep.

### Model Parameters

The model contains two main calibration parameters:

| Parameter | Meaning | Units |
|---|---|---|
| $k$ | Drainage coefficient controlling how quickly the BMP releases stored water | hr $^{-1}$ |
| $S_0$ | Effective storage threshold before outlet flow begins | in |

The parameters are calibrated by comparing the modeled outlet hydrograph with the observed Sherrerd Field outlet flow.

### Model Interpretation

The model is intentionally simplified. Storage $S$ does not represent the water depth in one specific BMP layer. Instead, it represents the combined effective storage behavior of the entire system.

Therefore, the model can be summarized as:

$$
\text{Rainfall}
\rightarrow
\text{Storage}
\rightarrow
\text{Threshold Exceeded}
\rightarrow
\text{Outflow}
$$

The purpose of the model is to determine whether a small number of effective parameters can reproduce the timing and magnitude of the observed rainfall--outflow response.
