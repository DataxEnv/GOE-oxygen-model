# Modeling Atmospheric Oxygen Accumulation on Early Earth

The rise of atmospheric oxygen is a pivotal transition in Earth’s history. It is often associated with the Great Oxidation Event. Oxygen produced by early photosynthetic organisms was initially consumed by reduced geological materials and volcanic gases, preventing significant accumulation in the atmosphere.

 Using a coupled system of ODEs, this project models the interaction between Cyanobacterial oxygen production, geological oxygen sinks, and volcanic flux. The aim is to explore conditions under which oxygen can accumulate.

#### Research Question 
How does the interaction between Cyanobacteria, reduced geological materials and Volcanic inputs control the accumulation of atmospheric oxygen levels on early Earth? 

## Conceptual Framework
The model tracks three interacting state variables:
	1.	Cyanobacterial biomass (B) – the population of oxygen-producing organisms.
	2.	Atmospheric oxygen (O) – oxygen concentration in the atmosphere.
	3.	Reduced geological reservoir (R) – available geochemical materials that consume oxygen.

Processes included in the model:
	•	Oxygen production via photosynthesis.
	•	Oxidation reactions of reduced materials.
	•	Logistic growth of cyanobacteria.
	•	Replenishment of the reduced reservoir via volcanic outgassing.


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
The system is modeled using coupled **ordinary differential equations (ODEs)**:

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
The system of ordinary differential equations (ODEs) is solved numerically using Python (`scipy.integrate.solve_ivp`). Time evolution of B(t), O(t), and R(t) is visualized using `matplotlib`. Parameter values and initial conditions are specified in the code for reproducibility.

The accompanying Jupyter Notebook contains the full model implementation, simulations, and figures.


## Results
<img width="700" height="600" alt="image" src="https://github.com/user-attachments/assets/6f8ed650-614b-4e57-b2ab-30bdd33b9055" />


## References
- Catling, D. et al. *Atmospheric Evolution on Earth and Other Planets*  
- Relevant papers/books on Great Oxidation Event, oxygen sinks, and cyanobacterial growth.
  
