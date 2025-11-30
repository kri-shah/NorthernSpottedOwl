# Northern Spotted Owl Population Model

## Overview
This repository implements and analyzes a discrete-time structured model for the Northern Spotted Owl.  
The population is split into:
- \(P_t\): paired owls at time \(t\)  
- \(S_{m,t}\): single male owls at time \(t\)

The model captures two key nonlinear effects:
- **Mate-finding**: when single owls are too sparse, many females fail to find mates.
- **Site availability**: when nesting sites are limited, juveniles cannot settle.

These mechanisms generate a strong **Allee effect** and a **critical habitat threshold** \(U_c \approx 149\):  
- If habitat \(U < U_c\), extinction is inevitable.  
- If habitat \(U > U_c\), there is a stable positive equilibrium and an unstable threshold equilibrium.

## Model (summary)

The update equations are:
\[
P_{t+1} = P_t p_s + S_{m,t} s_s M_t
\]
\[
S_{m,t+1} = \tfrac12 f s_J D_t P_t + S_{m,t} s_s (1 - M_t) + p_b P_t
\]

where
- \(M_t\) = fraction of females that successfully find mates (mate-finding term)  
- \(D_t\) = fraction of juveniles that successfully find unoccupied sites (dispersal term)

Default parameters (from the textbook):
\[
s_s=0.71,\ s_J=0.60,\ p_s=0.88,\ p_b=0.056,\ f=0.66,\ m=n=20,\ T=T'=1000.
\]

## Repository Structure

- `numerical.py`  
  - Solves the equilibrium equations for given habitat size \(U\)  
  - Reduces the system to a scalar nonlinear equation in \(S_m\)  
  - Computes Jacobians and eigenvalues to classify stability of equilibria

- `plots.py`  
  - Generates the root plots \(p(S_m)=0\) versus \(U\)
  - Generates phase-plane trajectories showing the Allee threshold and basins of attraction 

## Requirements
- Python 3.9+  
- Packages:
  - `numpy`
  - `matplotlib`
  - `mpmath`
  - `pandas` 
