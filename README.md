# GOE Model
This project explores oxygen dynamics during the Great Oxidation Event (GOE) using a simplified dynamical model. It documents the progression from an initial rate-based model (v1) through two redox-informed revisions (v2, v3), motivated by feedback from Professor David Catling (University of Washington).

---

## Repository Structure

- `GOE_model.ipynb` → Initial model (v1)
- `GOE_model_v2_redox.ipynb` → Redox-revised model (v2)
- `GOE_model_v3_redox.ipynb` → Fully redox-balanced model (v3, current)

---
### Version 3: Fully Redox-Balanced Model (Current)

#### Key Improvement
Every process that adds oxidising power to the atmosphere now has an equal and opposite term removing reducing power from the geological reservoir:

- **Organic carbon burial (β·α·B)**: Source in dO/dt, equal sink in dR/dt
- **H₂ escape (ε)**: Appears symmetrically in both equations
- **Geochemical oxidation (γOR)**: Depletes both O and R simultaneously

This enforces Catling's central argument: *oxygen cannot accumulate unless the system experiences a net loss of reducing power through physical processes — burial and H₂ escape — not biological production alone.*

#### Variables and Parameters

| Symbol | Value | Description |
|---|---|---|
| B(t) | — | Cyanobacteria biomass |
| O(t) | — | Atmospheric oxygen |
| R(t) | — | Reduced geological reservoir (volcanic reductants + reactive reduced species) |
| r | 0.05 | Cyanobacteria intrinsic growth rate |
| K | 1.0 | Carrying capacity |
| α | 0.05 | Gross photosynthesis rate (O₂ + CH₂O per biomass) |
| β | 0.30 | Burial efficiency (fraction of CH₂O permanently buried) |
| γ | 0.5 | Geochemical oxidation rate (pre-GOE reductant sink) |
| ε | 0.010 | H₂ escape flux (baseline — constant net oxidation driver) |
| V | 0.031 | Volcanic reductant flux |
| δ | 0.017 | Oxidative weathering rate (post-GOE O₂ sink) |

**Parameter logic:** V is tuned so that burial alone (β·α·K = 0.015) cannot deplete R, since V/2 = 0.0155 > 0.015. Only when H₂ escape (ε) is added does the net reductant loss exceed replenishment, triggering the GOE.

#### Governing Equations

$$\frac{dB}{dt} = rB\left(1 - \frac{B}{K}\right)$$

$$\frac{dO}{dt} = \underbrace{\beta\alpha B}_{\text{organic burial}} + \underbrace{\varepsilon}_{\text{H}_2\text{ escape}} - \underbrace{\gamma OR}_{\text{geochemical sink}} - \underbrace{\delta O}_{\text{weathering}}$$

$$\frac{dR}{dt} = \underbrace{V}_{\text{volcanic input}} - \underbrace{\gamma OR}_{\text{oxidation}} - \underbrace{\beta\alpha B}_{\text{burial removes reductant}} - \underbrace{\varepsilon}_{\text{H}_2\text{ escape}}$$

**Redox balance check:** Every term in dO/dt has a mirror term in dR/dt with opposite sign. This enforces conservation of redox state globally.

#### Redox Balance Verification

| Process | Effect on dO/dt | Effect on dR/dt |
|---|---|---|
| Organic burial (β·α·B) | +β·α·B | −β·α·B |
| H₂ escape (ε) | +ε | −ε |
| Geochemical oxidation (γOR) | −γOR | −γOR |
| Volcanic input (V) | — | +V |
| Oxidative weathering (δO) | −δO | — |

Note: γOR appears with the same sign in both equations, i.e., the oxidation reaction consumes both O₂ and the reductant simultaneously.

#### Methodology
The ODE system was solved numerically using Python's `scipy.integrate.solve_ivp`. Three analyses are presented:

1. **Time evolution**: Tracks B(t), O(t), and R(t) through three phases: anoxic buffering, GOE transition, and stable oxic state
2. **Phase-space analysis**: Visualises O versus R to identify the tipping point independent of time
3. **H₂ escape sensitivity**: Demonstrates that ε = 0 produces permanent anoxia regardless of burial, reproducing the key result of Claire et al. (2006) Fig. 8

#### Results
<img width="900" height="400" alt="v3_dynamic_plot" src="https://github.com/user-attachments/assets/63c62672-859d-42c2-bfbb-20f5c7bce25f" />

**Figure 1: System dynamics (v3)**


The simulation produces three distinct phases:

**Phase I - Anoxic buffering:** Cyanobacteria grow logistically but oxygen remains suppressed. The geochemical sink (γOR) dominates because R is large and volcanic input (V) continuously replenishes it. Burial and H₂ escape are insufficient to overcome this sink because V exceeds burial alone.

**Phase II - GOE transition:** Cumulative H₂ escape slowly drains the reduced reservoir. As R falls, geochemical suppression weakens and O begins to rise non-linearly — the tipping point.

**Phase III - Stable oxic state:** R is depleted. O stabilises at a new equilibrium where burial + H₂ escape is balanced by oxidative weathering (δO).

<img width="900" height="400" alt="GOE_v3_fig3_h2escape" src="https://github.com/user-attachments/assets/ac68c500-c37b-4697-9742-45bce848c463" />

**Figure 3: H₂ escape sensitivity**

When ε = 0, the system remains permanently anoxic regardless of cyanobacterial growth or burial — directly reproducing Claire et al. (2006) Fig. 8. H₂ escape is a necessary, not merely contributory, driver of the GOE.

#### Conclusion (v3)
The fully redox-balanced model confirms that the GOE cannot be explained by biological productivity alone. The transition to an oxic atmosphere requires a persistent net loss of reducing power from the Earth system, driven by organic carbon burial and, critically, the escape of hydrogen to space. Without H₂ escape, the model remains permanently anoxic, consistent with the theoretical framework of Catling (2014) and the biogeochemical modelling of Claire et al. (2006).

---
## Appendix - Model History

### Version 1: Rate-Based Model
The initial model used a coupled system of ODEs to describe interactions between cyanobacterial biomass, atmospheric oxygen, and a reduced geological reservoir. The goal was to investigate whether biological oxygen production alone could explain the timing and structure of the GOE.

#### Research Question
How does the interaction between cyanobacterial growth, reduced geological materials, and volcanic fluxes control the accumulation of atmospheric oxygen on early Earth?

#### Conceptual Framework

<img width="700" height="400" alt="fig 1" src="https://github.com/user-attachments/assets/67127670-15d7-419c-9790-8eb6d8f92e73" />

Figure 1: Conceptual structure of the dynamical model. image by Author.

The model tracks three interacting state variables:
1. Cyanobacterial biomass (B): the population of oxygen-producing organisms
2. Atmospheric oxygen (O): oxygen concentration in the atmosphere
3. Reduced geological reservoir (R): available geochemical materials that consume oxygen

Processes included:
- Oxygen production via photosynthesis
- Oxidation reactions of reduced materials
- Logistic growth of cyanobacteria
- Replenishment of the reduced reservoir via volcanic outgassing

#### Variables and Parameters

| Variable | Parameters |
|----------|------------|
| B(t): Cyanobacteria biomass | r: Cyanobacteria growth rate |
| O(t): Atmospheric oxygen concentration | K: Carrying capacity of cyanobacteria |
| R(t): Reduced geological reservoir | α: Oxygen production rate per biomass |
| | γ: Oxidation reaction rate constant |
| | V: Volcanic flux of reduced gases |

#### Governing Equations

$$\frac{dB}{dt} = rB\left(1 - \frac{B}{K}\right)$$

$$\frac{dO}{dt} = \alpha B - \gamma OR$$

$$\frac{dR}{dt} = V - \gamma OR$$

#### Assumptions
- Cyanobacteria follow logistic growth
- Oxygen production is proportional to cyanobacteria biomass
- Oxidation of reduced materials depends on both oxygen concentration and the reduced reservoir
- Volcanic input replenishes the reduced reservoir at a constant rate
- Other geological processes (sedimentation, tectonics) are not explicitly modelled

#### Methodology
The ODE system was solved numerically using Python's `scipy.integrate.solve_ivp`. The analysis consists of three components:

1. **Time evolution** — tracking B(t), O(t), and R(t) through the anoxic-to-oxic transition
2. **Phase-space analysis** — visualising O versus R to examine non-linear coupling and identify the tipping point
3. **Sensitivity analysis** — assessing the effect of volcanic flux (V) on the timing and extent of oxygenation

#### Results

<img width="800" height="400" alt="v1 result" src="https://github.com/user-attachments/assets/6f8ed650-614b-4e57-b2ab-30bdd33b9055" />

Figure 2: Temporal dynamics of the GOE model (v1).

The model produces a delayed oxygenation pattern driven by the gradual depletion of the reduced reservoir. Oxygen accumulation occurs once biological production exceeds the system's capacity to buffer oxygen through geochemical sinks.

#### Conclusion (v1)
The model suggests that the GOE can be interpreted as a non-linear transition driven by gradual biological growth coupled to finite geological sinks. Once the reduced reservoir is depleted, the system reaches a new, more oxidised equilibrium.

#### Limitation of v1
- The model did not explicitly enforce **global redox balance**
- Oxygen accumulation was treated as a local balance problem rather than a system-wide redox process
- Oxygenic photosynthesis was treated as a net O₂ source, which is incorrect on geological timescales, since CO₂ + H₂O ⇌ O₂ + CH₂O is reversible and redox-neutral

---

### Version 2: Redox-Revised Model

#### Motivation
Following expert review, v2 incorporates system-level redox accounting. The key insight, grounded in Catling (2014) and Claire et al. (2006), is:

> Redox conservation is as inviolable as mass or energy conservation. Life on its own cannot change the net redox state of the surface of the Earth on a geological timescale. Every O₂ is balanced by organic matter (CH₂O). Net O₂ accumulation requires removal of reducing power from the system, either by burial of organic carbon or escape of hydrogen to space.

#### Revised Understanding
- Oxygen accumulation is not controlled by production alone
- Oxygenic photosynthesis produces both O₂ and CH₂O as a coupled redox pair — it does not change net atmospheric oxygen unless the reducing counterpart is removed
- Net O₂ accumulation requires:
  - Burial of organic carbon (CH₂O)
  - Escape of hydrogen (H₂) to space

> Therefore, oxygen accumulation depends on the **net removal of reducing power from the Earth system**, not biological production alone.

#### Changes from v1
- Added organic carbon burial term (β·α·B)
- Added hydrogen escape term (ε)
- Added oxidative weathering sink (δO)
- Recast system as a redox-balanced evolution rather than a simple rate competition

#### Limitation of v2
Although v2 introduced the correct terms, H₂ escape (ε) was added as a free source in dO/dt without a corresponding reduction of R, violating the redox balance it set out to enforce. The burial term was also not consistently mirrored across both equations.

---

## References

Catling, D. C. (2014). The Great Oxidation Event Transition. In *Treatise on Geochemistry* (2nd Ed.), edited by H. D. Holland and K. K. Turekian, vol. 6, Elsevier, Oxford, 177–195. https://faculty.washington.edu/dcatling/Catling2014_GreatOxidationEvent.pdf

Claire, M. W., Catling, D. C., & Zahnle, K. J. (2006). Biogeochemical modelling of the rise in atmospheric oxygen. *Geobiology*, 4(4), 239–269. https://faculty.washington.edu/dcatling/Claire2006-Geobiology.pdf

Holland, H. D. (2006). The oxygenation of the atmosphere and oceans. *Philosophical Transactions of the Royal Society B: Biological Sciences*, 361(1470), 903–915. https://doi.org/10.1098/rstb.2006.1838

Lyons, T. W., Reinhard, C. T., & Planavsky, N. J. (2014). The rise of oxygen in Earth's early ocean and atmosphere. *Nature*, 506, 307–315. https://doi.org/10.1038/nature13068
