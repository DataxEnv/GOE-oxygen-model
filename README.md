# GOE Model
This project explores oxygen dynamics during the Great Oxidation Event (GOE) using a simplified dynamical model.


---

##  Model Update (v2 – Redox-Balanced Revision)
This revision refines the original model (v1) by incorporating system-level redox accounting.


 ### Initial Approach (v1)
- Oxygenic photosynthesis treated as the net source of O₂  
- Oxygen sinks represented by reduced gases and geological reservoirs  
- Rate-based formulation (production vs consumption)


### Limitation of v1
- The model did not explicitly enforce **global redox balance**  
- Oxygen accumulation was treated as a local balance problem rather than a *system-wide* redox process

### Revised Understanding (v2)
- Oxygen accumulation is not controlled by production alone  
- Oxygenic photosynthesis produces both O₂ and reduced organic matter (CH₂O) as a coupled redox pair, so it does not change net atmospheric oxygen unless the reducing counterpart (CH₂O) is removed. 
- Net O₂ accumulation requires removal of reducing power from the system via:
  - Burial of organic carbon (CH₂O)  
  - Escape of hydrogen (H₂) to space  

> Therefore, oxygen accumulation depends on the **net removal of reducing power from the Earth system**, not biological production alone.

### Model Update (v2)

- Added organic carbon burial term  
- Added hydrogen escape term  
- Recast system as a redox-balanced evolution rather than a simple rate competition

### Results (Summary)

The updated model shows that oxygen accumulation only occurs when the system experiences a net loss of reducing power, rather than when oxygen production exceeds local sinks.

Full equations, New assumptions, and simulation results are available in:
`GOE_model_v2_redox.ipynb`

---

## Repository Structure

- `GOE_model.ipynb` → Initial model (v1)  
- `GOE_model_v2_redox.ipynb` → Updated model (v2)

---





## Appendix: Initial Model (v1)
The initial model used a coupled system of ordinary differential equations (ODEs) to describe interactions between cyanobacterial biomass, atmospheric oxygen, and a reduced geological reservoir. The goal was to investigate whether biological oxygen production alone could explain the timing and structure of the Great Oxidation Event.

### Research Question
How does the interaction between cyanobacterial growth, reduced geological materials, and volcanic fluxes control the accumulation of atmospheric oxygen on early Earth?


## Conceptual Framework

<img width="700" height="600" alt="fig 1" src="https://github.com/user-attachments/assets/67127670-15d7-419c-9790-8eb6d8f92e73" />

Figure 1: Conceptual structure of the dynamical model. image by Author.

The model tracks three interacting state variables:
1. Cyanobacterial biomass (B)- the population of oxygen-producing organisms.
2. Atmospheric oxygen (O)– oxygen concentration in the atmosphere.
3. Reduced geological reservoir (R)– available geochemical materials that consume oxygen.

Processes included in the model:
- Oxygen production via photosynthesis.
- Oxidation reactions of reduced materials.
- Logistic growth of cyanobacteria.
- Replenishment of the reduced reservoir via volcanic outgassing.

---


## Model description 
### Variables and Parameters

| Variable | Parameters |
|----------|-------------|
| B(t): Cyanobacteria biomass | r: Cyanobacteria growth rate |
| O(t):Atmospheric oxygen concentration |  K: Carrying capacity of cyanobacteria |
| R(t):  Reduced geological reservoir| α: Oxygen production rate per biomass |
|                                     | γ:  Oxidation reaction rate constant |
|                                   | V: Volcanic flux of reduced gases |


### Governing Equations
The model is governed by a system of coupled **ordinary differential equations (ODEs)**:

**dB/dt = rB (1-B/K)** 

**dO/dt = αB - γOR** 
 
**dR/dt = V - γOR**

Where:
- B = cyanobacterial biomass
- O = atmospheric oxygen
- R = reduced reservoir


### Assumptions
- Cyanobacteria follow logistic growth.
- Oxygen production is proportional to cyanobacteria biomass. 
- Oxidation of reduced materials depends on both oxygen concentration and reduced reservoir.
- Volcanic input replenishes the reduced reservoir at a constant rate.
- Other geological processes (sedimentation, tectonics) are not explicitly modeled.


---

  
## Methodology
The system of ordinary differential equations (ODEs) was solved numerically using Python's `scipy.integrate.solve_ivp`. 

The analysis consists of three components: 
1. **Time evolution**: Tracking *B(t), O(t)*, and *R(t)* to follow the system's transition from anoxic to oxic states.
2. **Phase-space Analysis**: visualizing *O* versus *R* to examine the non-linear coupling and identify the system's tipping point independent of time.
3. **Sensitivity Analysis**: Assessing the effect of volcanic flux *(V)* to understand how geeological outgassing thresholds control the timing and extent of oxygenation. 

All simulations are visualized using `matplotlib`. Parameter values and initial conditions are documented in the accompanying Jupyter Notebook for full reproducibility.

---

## Results (v1 Summary)
<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/6f8ed650-614b-4e57-b2ab-30bdd33b9055" />

Figure 2: Temporal dynamics of the Great Oxidation Event (GOE) model.


The model produces a delayed oxygenation pattern driven by the gradual depletion of the reduced reservoir. Oxygen accumulation occurs once biological production exceeds the system’s capacity to buffer oxygen through geochemical sinks.


### Conclusion (v1)

Ultimately, The model suggests that the Great Oxidation Event can be interpreted as a non-linear transition driven by gradual biological growth coupled to finite geological sinks. Once the reduced reservoir is depleted, the system reaches a new, more oxidized equilibrium that enabled the emergence of aerobic ecosystems.

---

## References
Claire, M. W., Catling, D. C., & Zahnle, K. J. (2006). Biogeochemical modelling of the rise in atmospheric oxygen. *Geobiology*, 4(4), 239–269. https://faculty.washington.edu/dcatling/Claire2006-Geobiology.pdf

Holland, H. D. (2006). *The oxygenation of the atmosphere and oceans. Philosophical Transactions of the Royal Society B: Biological Sciences*, 361(1470), 903–915. https://doi.org/10.1098/rstb.2006.1838

Lyons, T. W., Reinhard, C. T., & Planavsky, N. J. (2014). *The rise of oxygen in Earth’s early ocean and atmosphere. Nature*, 506, 307–315. https://doi.org/10.1038/nature13068
