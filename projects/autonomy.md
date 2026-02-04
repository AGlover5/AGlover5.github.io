---
layout: page
title: Orbital Robotic Autonomy
---

# Information-Driven Autonomous Orbital Maneuvering

## Summary

This project implements an autonomous guidance and estimation framework for spacecraft operating under uncertain mass properties. Traditional controllers minimize tracking error but do not explicitly optimize parameter observability.

This work embeds the Fisher Information Matrix directly into a model predictive control framework to actively generate informative trajectories while maintaining control stability.

---

## System Architecture

*(Insert architecture diagram here)*

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
