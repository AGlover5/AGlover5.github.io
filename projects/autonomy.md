---
layout: page
title: Orbital Robotic Autonomy
---

# Information-aware Excitation Trajectories for In-Orbit Mass Property Estimation

## Read the Paper! (course submission version)
<div>
  <a href="/assets/posters/ASTE_599_Final_Project-3.pdf" target="_blank">
    <img
      src="/assets/images/Paper-thumb.png?v=2"
      alt="Water channel poster preview"
      width="220"
      style="border:1px solid #ddd; border-radius:6px;"
    >
  </a>
</div>
<p><em>Click the preview to open the full poster (PDF).</em></p>

This document reflects the version submitted for course evaluation. The project is currently being extended with additional sensing and estimation components toward a potential publication.

## Summary

This project implements an autonomous guidance and estimation framework for spacecraft operating under uncertain mass properties. Traditional controllers minimize tracking error but do not explicitly optimize parameter observability.

This work embeds the Fisher Information Matrix directly into a model predictive control framework to actively generate informative trajectories while maintaining control stability.

---

# My Role

This project was developed as a collaborative research effort. My primary contributions focused on the formulation of the MPC control architecture and cost function design. I led the implementation and tuning of the Fisher Information–weighted cost structure and performed the simulation experiments used to evaluate the trade-offs between trajectory tracking and parameter excitation.

My primary technical focus was on the MPC cost formulation and the evaluation of controller performance across simulated experiments
---

##  Control Scheme Goals

1. Learn mass properties as quickly as possicle
2. Disturb the ideal positon goal state trajectory as little as possible to achieve goal #1.
3. Consume the least amount of fuel possible to acheive goals #1 and #2.

---

## Theory

### Dynamics Modeling
**Planar Dynamics**
- Nonlinear relative orbital motion
- Coupled translation and rotation
- Parameterized inertia uncertainty

**State Space Model**



### Stage Cost for Model Predicitve Control (MPC)

---

## Autonomy Stack

### MuJoCo for Physics Engine in Python (assitant capactiy to lead member)
- Generated superstructures out of passive modular blocks (random or procedurally built)
- Generated active agents from modular blocks with 4 thrusters for planar translation and rotation.
- Simulated superstructere dynamics under motion due to docked agents.
- Output state history of each agent over a complete trajectory execution.

<div style="display:flex; align-items:center; gap:12px; flex-wrap:wrap;">

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/block.png" 
      alt="CL vs alpha" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Lift Coefficients at varying angle-of-attack
    </figcaption>
  </figure>

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/superstructure.png" 
      alt="Flow Visualization" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Randomly generated superstructure 
    </figcaption>
  </figure>

</div>

A team member developed the on-orbit superstructure model used in the MuJoCo simulation environment. I used this model to evaluate the behavior of the MPC controller under different cost formulations and excitation trajectories.

### CasADI for Trajectory Optimization
**Choice of IPOPT for the nonlinear programming (NLP) function**
- IPOPT was chosen because it is well suited option for:
    - nonlinear dynamics and/or constraints
    - offline trajectory calculations (comes with longer compute time)
    - inequality-constrained states and control inputs
    - when the system needs an initial plan from a cold start. 
  
- Investigation of other optimizers is necessary for future online MPC applications that require faster computation speed (more on this in the future work)
 
### Model Predictive Control in Python (MPC)

- Tunable information seeking 

*The MPC cost trades tracking error and control effort against information gain to accelerate parameter convergence.*

## Engineering Outputs

- Estimation error convergence
- Trajectory comparison
- Control effort trade study

---

## Engineering Tradeoffs

Increasing Fisher weighting accelerated parameter convergence but increased control effort and trajectory curvature. A hybrid weighting strategy provided the best performance across mission objectives.

---
#Future and Planned Work

### Estimation
- Extended Kalman filter
- Augmented parameter state
- Noise modeling and observability analysis


## Applicable Missions

- On-orbit servicing
- Autonomous rendezvous
- Space domain awareness
- Uncooperative target capture

---

## Tools

- Python  
- NumPy / SciPy  
- CasADi  
- MATLAB  
