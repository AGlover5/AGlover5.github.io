---
layout: page
title: Orbital Robotic Autonomy
---

# Information-aware Excitation Trajectories for In-Orbit Mass Property Estimation

## Read the Paper!
<div>
  <a href="/assets/posters/water-channel-poster.pdf" target="_blank">
    <img
      src="/assets/images/Paper-thumb.png?v=2"
      alt="Water channel poster preview"
      width="220"
      style="border:1px solid #ddd; border-radius:6px;"
    >
  </a>
</div>
<p><em>Click the preview to open the full poster (PDF).</em></p>


## Summary

This project implements an autonomous guidance and estimation framework for spacecraft operating under uncertain mass properties. Traditional controllers minimize tracking error but do not explicitly optimize parameter observability.

This work embeds the Fisher Information Matrix directly into a model predictive control framework to actively generate informative trajectories while maintaining control stability.

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

### Estimation
- Extended Kalman filter
- Augmented parameter state
- Noise modeling and observability analysis

### Stage Cost for Model Predicitve Control (MPC)


**Model Predictive Control (MPC)**

- Finite-horizon MPC
- Fisher-information-based cost term
- Tunable information–fuel tradeoff
*The MPC cost trades tracking error and control effort against information gain to accelerate parameter convergence.*

---

## Autonomy Stack

### MuJoCo for python
- Generated purpose-built and random superstructures from passive modular blocks
- Generated active agents from modular blocks with 4 thrusters for planar translation and rotation.
- Simulated superstructere dynamics under motion from docked agents.
- Output state history of each agent over a complete trajectory execution. 

## Results

- Estimation error convergence
- Trajectory comparison
- Control effort trade study

---

## Engineering Tradeoffs

Increasing Fisher weighting accelerated parameter convergence but increased control effort and trajectory curvature. A hybrid weighting strategy provided the best performance across mission objectives.

---

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
