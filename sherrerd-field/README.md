# Sherrerd Field Linear Reservoir Model

The Sherrerd Field BMP is represented using a simplified **linear reservoir model**. It is a field at Princeton University used for Lacrosse and other sports activities. 

Instead of modeling each physical component of the BMP separately, such as the soil, gravel layer, drainage pipes, and outlet structure, the entire system is represented as one effective storage reservoir.

Conceptually:

**Rainfall → Storage → Outlet Flow**

Rainfall increases the amount of water stored in the BMP. The system is assumed to retain some water before measurable outflow begins. Once storage exceeds a threshold, water is released through the outlet.

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
