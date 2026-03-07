# Modeling Atmospheric Oxygen Accumulation on Early Earth

The rise of atmospheric oxygen is a pivotal transition in Earth’s history. It is often associated with the Great Oxidation Event. Oxygen produced by early photosynthetic organisms was initially consumed by reduced geological materials and volcanic gases, preventing significant accumulation in the atmosphere.

Using a coupled system of ordinary differential equations (ODEs), this project models the interaction between cyanobacterial oxygen production, geological oxygen sinks, and volcanic flux. The aim is to explore conditions under which oxygen can accumulate.

#### Research Question 
How does the interaction between Cyanobacteria, reduced geological materials and Volcanic inputs control the accumulation of atmospheric oxygen levels on early Earth? 

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

  
## Methodology
The system of ordinary differential equations (ODEs) was solved numerically using Python's `scipy.integrate.solve_ivp`. 

The analysis consists of three components: 
1. **Time evolution**: Tracking *B(t), O(t)*, and *R(t)* to follow the system's transition from anoxic to oxic states.
2. **Phase-space Analysis**: visualizing *O* versus *R* to examine the non-linear coupling and identify the system's tipping point independent of time.
3. **Sensitivity Analysis**: Assessing the effect of volcanic flux *(V)* to understand how geeological outgassing thresholds control the timing and extent of oxygenation. 

All simulations are visualized using `matplotlib`. Parameter values and initial conditions are documented in the accompanying Jupyter Notebook for full reproducibility.



## Results
<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/6f8ed650-614b-4e57-b2ab-30bdd33b9055" />

Figure 2: Temporal dynamics of the Great Oxidation Event (GOE) model.


The simulation shows a clear temporal sequence in the dynamics of biomass (B), atmospheric oxygen (O), and the reduced reservoir (R).

Initially, cyanobacterial biomass *B* follows a characteristic sigmoidal (logistic) growth curve as it gradually approaches its carrying capacity *K* **(Phase I: Biomass Expansion)**. During this early phase, atmospheric oxygen *O* remains near zero because the oxygen produced is rapidly consumed by the reduced reservoir *R*, which buffers the system **(Phase II: Sink-Limited Oxygen)**.

However, as biomass continues to increase, oxygen production eventually exceeds the reducing capacity of *R*. Once *B* crosses a critical threshold, the reduced reservoir becomes rapidly depleted and atmospheric oxygen rises nonlinearly **(Phase III: The Tipping Point)**. This rapid transition represents the simulated onset of the Great Oxidation Event, shifting the system from an anoxic to a more oxygenated state.

## Discussion

The model effectively captures the tipping-point behavior often associated with the Great Oxidation Event: oxygenation is a non-linear outcome of the balance between biological Oxygen production and geological reductant supply.

The delay between the rise of Cyanobacterial biomass *(B)* and the increase in atmospheric oxygen *(O)* reflects the role of geological sinks in initially buffering the atmosphere against oxygen accumulation. During this phase, most of the oxygen produced by photosynthesis is consumed through oxidation reactions with reduced materials. This confirms that an active biological source alone is insufficient for persistent oxygenation when geological sinks are strong.

Gradual depletion of *R* via the *γOR* oxidation reaction reduces the system’s ability to remove oxygen. Once oxygen production surpasses this sink capacity, atmospheric oxygen begins to rise rapidly. Sensitivity analysis indicates that volcanic flux *(V)* modulates the rate and timing of oxygen accumulation: elevated volcanic reducing fluxes strengthen the chemical sink and can delay Oxygenation even in the presence of mature biomass. This supports the hypothesis that the timing of the GOE may not have depended solely on the biological evolution of Cyanobacteria, but also on the long-term cooling of Earth's mantle and the subsequent decline of reducing volcanic gases (Holland, 2006; Lyons et al., 2014).


## Conclusion

Ultimately, the simulation demonstrates that the GOE can be interpreted as a one-way, non-linear transition driven by gradual biological growth coupled to finite geological sinks. Once the reduced reservoir is depleted, the system reaches a new, more oxidized equilibrium that enabled the emergence of aerobic ecosystems.


## References

Holland, H. D. (2006). *The oxygenation of the atmosphere and oceans. Philosophical Transactions of the Royal Society B: Biological Sciences*, 361(1470), 903–915. https://doi.org/10.1098/rstb.2006.1838

Lyons, T. W., Reinhard, C. T., & Planavsky, N. J. (2014). *The rise of oxygen in Earth’s early ocean and atmosphere. Nature*, 506, 307–315. https://doi.org/10.1038/nature13068
