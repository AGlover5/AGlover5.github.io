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
      alt="Paper Preview"
      width="220"
      style="border:1px solid #ddd; border-radius:6px;"
    >
  </a>
</div>
<p><em>Click the preview to open the full paper (PDF).</em></p>

This document reflects the version submitted for course evaluation. The project is currently being extended with additional sensing and estimation components toward a potential publication.

## Summary

This project implements an autonomous guidance and estimation framework for spacecraft operating under uncertain mass properties. Traditional controllers minimize tracking error but do not explicitly optimize parameter observability.

This work embeds the Fisher Information Matrix directly into a model predictive control framework to actively generate informative trajectories while maintaining control stability.

---

# My Role

This project was developed as a collaborative research effort. My primary contributions focused on the formulation of the MPC control architecture and cost function design. I led the implementation and tuning of the Fisher Information–weighted cost structure and performed the simulation experiments used to evaluate the trade-offs between trajectory tracking and parameter excitation.

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
      alt="block" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Individual Floatbot Agent (active with simulated control thrusters)
    </figcaption>
  </figure>

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/superstructure.png" 
      alt="Superstructure" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Randomly generated superstructure 
    </figcaption>
  </figure>

</div>

A team member developed the on-orbit superstructure model used in the MuJoCo simulation environment. I used this model to evaluate the behavior of the MPC controller under different cost formulations and excitation trajectories.

### CasADi for Trajectory Optimization
**Choice of IPOPT for the nonlinear programming (NLP) function**
- IPOPT was chosen because it is well suited option for:
    - nonlinear dynamics and/or constraints
    - offline trajectory calculations (comes with longer compute time)
    - inequality-constrained states and control inputs
    - when the system needs an initial plan from a cold start. 
  
- Investigation of other optimizers is necessary for future online MPC applications that require faster computation speed (more on this in the future work)
 
### Model Predictive Control in Python (MPC)

The optimal control problem is formulated for the MPC controller in python.

<p align="center">
<img width="286" height="174" alt="OCP" src="https://github.com/user-attachments/assets/86b62fe9-b1e8-469f-aab2-e2c44ff66722" />
</p>

## Engineering Outputs

---

### Tuning the Fisher Term

<p align="center">
<img width="318" height="31" alt="stage-cost" src="https://github.com/user-attachments/assets/2f442a7a-90db-405e-9535-83fab30ac5ac" />
</p>


<div style="display:flex; align-items:center; gap:12px; flex-wrap:wrap;">

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/mass-error.png" 
      alt="mass error" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Individual Floatbot Agent (active with simulated control thrusters)
    </figcaption>
  </figure>

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/inertia-error.png" 
      alt="inertia error" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Randomly generated superstructure 
    </figcaption>
  </figure>

</div>

<br>
***Key Insights***
Mass estimation error was reduced to <1% when the individual costs can be tuned with a set of individual λ combinations shown by the color scale for the mass and inertia parameters. 

---

### Heurisitc Approach for a Dynamic Fisher-term Weighting

An exponential decay term was applied at each step k to heuristically decrease the relative importance of the Fisher Information component within the total cost function over the MPC horizon.

<p align="center">
<img width="257" height="55" alt="decay" src="https://github.com/user-attachments/assets/bad74129-efb4-490c-a4cb-f33cb69cbbdd" />
</p>

The Fisher Information for the mass property estimates was treated as a scalar (trace of the FIM) to single out this new approach from the earlier comparison of weighing each parameter individually. Thus the cost term was changed to the following: 

<p align="center">
<img width="378" height="80" alt="screenshot 2026-03-05 at 8 06 34 PM" src="https://github.com/user-attachments/assets/524df193-e283-4a27-afb1-f1974d499dc0" />
</p>

The six state vectors showed the following response to the applicaton of γ = 0.2 and γ = 0.9, respectively in the decaying FIM weight, λ.

<div style="display:flex; align-items:center; gap:12px; flex-wrap:wrap;">

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/lambda02.png" 
      alt="lambda 02" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      State trajectories over time using γ = 0.2.
    </figcaption>
  </figure>

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/lambda09.png" 
      alt="lambda 09" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      State trajectories over time using γ = 0.9.
    </figcaption>
  </figure>

</div>

***Key Insights***
The γ = 0.2 case shows greater excitation since a higher relative priority on exploratory attitudes is applied for longer. Conversely, the γ = 0.9 case predictably shows a much more state convergence oriented trajectory. Since this demonstrates that the priority on the state convergence and information exploration can be traded by the amount the FIM weight decays, it is worth evaluating the mass convergence performance in both cases to get insight on the optimal decay rate. 

<br>

---

### Mass Convergence

<div style="display:flex; align-items:center; gap:12px; flex-wrap:wrap;">

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/mass-conv-02.png" 
      alt="mass convergence 02" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Individual Floatbot Agent (active with simulated control thrusters)
    </figcaption>
  </figure>

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/mass-conv-09.png" 
      alt="mass convergence 09" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Randomly generated superstructure 
    </figcaption>
  </figure>

</div>

<br>

---

## Engineering Tradeoffs

Increasing Fisher weighting accelerated parameter convergence but increased control effort and trajectory curvature. A hybrid weighting strategy provided the best performance across mission objectives.

---

## Future and Planned Work

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
- NumPy  
- CasADi  
- MATLAB  
