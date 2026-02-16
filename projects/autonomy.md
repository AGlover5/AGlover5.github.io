---
layout: page
title: Orbital Robotic Autonomy
---

# Information-aware Excitation Trajectories for In-Orbit Mass Property Estimation

## Summary

This project implements an autonomous guidance and estimation framework for spacecraft operating under uncertain mass properties. Traditional controllers minimize tracking error but do not explicitly optimize parameter observability.

This work embeds the Fisher Information Matrix directly into a model predictive control framework to actively generate informative trajectories while maintaining control stability.

---

##  Control Scheme Goals

1. Learn mass properties as quickly as possicle
2. Disturb the ideal positon goal state trajectory as little as necesaary to achieve goal #1.
3. Consume the least amount of fuel possible to acheive goals #1 and #2.

$$
J = \sum_{k=0}^{N} \left( x_k^\top Q x_k + u_k^\top R u_k \right)
$$

*(Insert architecture diagram here)*

## System Architecture

Dynamics → Estimator → Fisher Information → MPC → Control Execution

---

## Technical Components

### Dynamics Modeling
- Nonlinear relative orbital motion
- Coupled translation and rotation
- Parameterized inertia uncertainty

### Estimation
- Extended Kalman filter
- Augmented parameter state
- Noise modeling and observability analysis

### Control
- Finite-horizon MPC
- Fisher-information-based cost term
- Tunable information–fuel tradeoff

---

## Results

*(Insert plots here)*

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
