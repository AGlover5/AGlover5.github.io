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

## Autonomy and Simulation Stack

### MuJoCo Physics Simulation Environment
- Assisted lead member in modelling of coupling and attitude dynamics of agent-structure for implementation into MPC structure.
- Superstructures generated out of passive modular blocks (random or procedurally built)
- Active agents generated from modular blocks with 4 thrusters for planar translation and rotation.
- Output state history produced for each agent over a complete trajectory execution.

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

A team member led the developement of the on-orbit floatbot agent and superstructure models used in the MuJoCo simulation environment. I used this model to evaluate the behavior in an MPC controller under different cost formulations and excitation trajectories.

### CasADi for Trajectory Optimization
**Choice of IPOPT for the nonlinear programming (NLP) function**
- IPOPT was chosen because it is well suited option for:
    - nonlinear dynamics and/or constraints
    - offline trajectory calculations (comes with longer compute time)
    - inequality-constrained states and control inputs
  
- Investigation of other optimizers is necessary for future online MPC applications that require faster computation speed (more on this in the future work)
 
### Model Predictive Control in Python (MPC)

Optimal control problem formulation for IPOPT:

<p align="center">
<img width="286" height="174" alt="OCP" src="https://github.com/user-attachments/assets/86b62fe9-b1e8-469f-aab2-e2c44ff66722" />
</p>

The Fisher Information Matrix implementation into the cost function is described in the last two equations where F is computed at each step k, and where Φ is a function of the parameter θ.

## Engineering Outputs

---

### Tuning the Fisher Term

In this first case, the cost function individually tunes the FIM weight on each parameter by taking the diagonal of the matrix.

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
Property estimation error was reduced to <1% when the individual costs could be tuned with a set of individual λ combinations, shown by the color scale for the mass and inertia parameters (full comparison with uniform λ case described in paper).

---

### Heurisitc Approach for a Dynamic Fisher Information Term Weighting

An exponential decay term was applied at each step k to heuristically decrease the relative importance of the Fisher Information component within the total cost function over the MPC horizon.

<p align="center">
<img width="257" height="55" alt="decay" src="https://github.com/user-attachments/assets/bad74129-efb4-490c-a4cb-f33cb69cbbdd" />
</p>

The Fisher Information for the mass property estimates was treated as a scalar (trace of the FIM) to single out this new approach from the earlier comparison of weighing each parameter individually. Thus, the cost term was changed to the following: 

<p align="center">
<img width="378" height="80" alt="screenshot 2026-03-05 at 8 06 34 PM" src="https://github.com/user-attachments/assets/524df193-e283-4a27-afb1-f1974d499dc0" />
</p>

The six state vectors showed the following response to the application of γ = 0.2 and γ = 0.9, respectively in the decaying FIM weight, λ.

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

The mass property estimation was plotted against time for the cases described above. 
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
***Key Insights***
Although the γ = 0.9 case paradoxically seems to converge quicker, in the example of mass, it converges to roughly 0.2 kg off of the true values and seemingly lacks the excitation to correct the estimate. 

---

## Engineering Conclusions

- Tuning the Fisher Information weighting-either dynamically decaying over time or biasing toward an individual mass parameter-can strongly influence estimation performance by generating a desired amount of excitation along a trajectory.
- While the heuristic tuning approaches performed offline were sufficient to demonstrate the tradeoff between excitation and state convergence, more robust controllers would benefit from online parameter estimation and control.

---

## Future and Planned Work

### Parameter Estimation
- Online MPC
- Extended Kalman filter to incoporate sensior and model noise
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
