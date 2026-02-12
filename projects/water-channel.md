---
layout: page
title: Experimental Fluid Dynamics
---

## View the Poster from the Expo!
<div>
  <a href="/assets/posters/water-channel-poster.pdf" target="_blank">
    <img
      src="/assets/images/water-channel-poster-thumb.png?v=2"
      alt="Water channel poster preview"
      width="220"
      style="border:1px solid #ddd; border-radius:6px;"
    >
  </a>
</div>
<p><em>Click the preview to open the full poster (PDF).</em></p>

## Summary

This project investigated flow behavior around three airfoils in a controlled water channel environment. The goal was to characterize flow structures, validate scaling assumptions, and compare experimental results to theoretical predictions.

<p align="center">
<img width="868" height="242" alt="Wings" src="https://github.com/user-attachments/assets/206ba3ef-3fa9-494e-930d-43f4b875a9d1" />
</p>

The three airfoils of choice were called smooth (left), intermediately corrugated (middle), and extremely corrugated (right).  

---

## Motivation and Relevance
Low Reynolds number fluid flow is an increasingly common regime for small UAVs and underwater drones. A prior CFD studies by Tang et al [1] suggested that corrugated airfoil geometries—motivated by dragonfly wing structures—could generate higher lift coefficients and improved lift-to-drag ratios compared to conventionally smooth, teardrop shaped NACA airfoils.
The objective of this project was to experimentally validate these predicted trends and investigate the flow mechanisms responsible for performance differences in a controlled water channel environment.

**Guiding Scientific Literature**
  <div style="display:flex; align-items:center; gap:12px; flex-wrap:wrap;">

 <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/tang.png" 
      alt="tang pressure CFD" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Coefficient of pressure CFD conducted by Tang et al [1] as the insipration for the experimental airfoil design
    </figcaption>
  </figure>

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/vortex.png" 
      alt="vortex" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Diagram from Deubel [2] showing the desired vortex generation of a corrugated wing 
    </figcaption>
  </figure>

</div>

The motivating insight from both Tang et al [1] and Deubel [2] was that the corugated patterns would crete lower pressure on the top surface of the airfoil, increasing lift.

For this experiment, the smooth airfoil acted (NACA 2410) as a control, the intermediate was designed with CAD to act as an approximation of the corrugated pattern in the CFD conducted by Tang et al [1], and the extreme airfoil was made out of experimental curioisty to see what effects doubling how densly packed the corrugation pattern could have on lift and vortex generation.

## High Level Experimental Setup 
The experimental setup was designed for rapid and repeatable iterations of the lift measurements as well as for dye visualization runs at different angles of attack.

<p align="center">
  <img
    width="753"
    height="486"
    alt="Water Channel Test Bed"
    src="https://github.com/user-attachments/assets/fe9b0d69-e8b0-4f1d-89a6-bded76dc3b2a"
  />
</p>

Lift forces were converted from strain gauge measurements at the top of the cantilever beam supporting the airfoil. Lift coefficient was then calculated from the controlled wing area and dynamic pressure.

## Pragmatic and Economic Considerations
Since the limiting factor on the experiment was facility availability, it was decided that constructing a single adjustable angle-of-attack mechanism would cause unnecesary delays due to additional assembly time and angle tolerance verification. 

<p align="center">
  <img
    width="517"
    height="401"
    alt="Exploded View of Custom Frame"
    src="https://github.com/user-attachments/assets/6bbde05e-3185-41ce-ad30-2606ba49ff15"
  />
</p>

The majority of the setup used beams, slots, and connectors that were already in stock at the university, leaving considerable margin for the 3D printing budget. By making smaller and simpler individual connectors for each AOA of a standard design, a connector could be duplicated for any angle, printed, and then used in a data recording trial within 1-2 days of the 3D print order being submitted.

<p align="center">
  <img
    width="545"
    height="427"
    alt="Screenshot 2026-02-10 at 4:18:23 PM"
    src="https://github.com/user-attachments/assets/de42433b-1c87-423d-937d-3d909f4df523"
  />
</p>

---

## Measurement & Data Processing

**Generating a Calibration Curve for Strain Guage Signal to Lift Force Conversion**

<div style="display:flex; align-items:center; gap:12px; flex-wrap:wrap;">

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/strain-gauge-calibration-setup.png" 
      alt="Strain gauge calibration setup diagram" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Calibration setup (applied loads → strain gauge output)
    </figcaption>
  </figure>

  <div style="font-size:28px; line-height:1; margin: 6px 4px;">
    ➡️
  </div>

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/strain-gauge-calibration-curve.png" 
      alt="Strain gauge calibration curve" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Calibration curve (strain → equivalent lift force)
    </figcaption>
  </figure>

</div>

---

## Results
**Measured Forces and Captured Vortices**
<div style="display:flex; align-items:center; gap:12px; flex-wrap:wrap;">

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/results.png" 
      alt="CL vs alpha" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Lift Coefficients at varying angle-of-attack
    </figcaption>
  </figure>

  <figure style="flex:1 1 260px; margin:0; text-align:center;">
    <img 
      src="/assets/images/flow-vis.png" 
      alt="Flow Visualization" 
      style="width:100%; max-width:360px; height:auto; border:1px solid #ddd; border-radius:6px;"
    >
    <figcaption style="font-size:0.9em; color:#555; margin-top:6px;">
      Flow Visualization of the intermediate design at +3 degrees 
    </figcaption>
  </figure>

</div>





- Mean CL values show increase due to corrugation.
- System noise dominated with heavy uncertainty despite maximimal priority on increasing number of tests to minimize strain guage uncertainty for each airofoil and angle combination. 
- High sensitivity to flow speed variations due to motor power fluctuations and water channel geometry.

---

## Engineering Conclusions

- **Design for rapid iteration under time constraints:**  
  Simpler experimental designs enabled rapid construction, deployment, and iteration within a tight timeline, allowing earlier data collection and faster reduction of uncertainty from the strain gauge voltage data.

- **Uncertainty-cautious experiment design:**  
  Environmental uncertainties—particularly variability in water channel flow speed—dominated total measurement uncertainty despite the low noise in strain gauge voltage data. Designing experiments around dominant uncertainty sources should be the biggest 

- **Validity of the applied assumptions:**  
  Even with minimal equipment noise, the experimental implementation of CFD predictions needs to, within an acceptable tolerance, recreate the conditions that made a particular assumption valid. In this case, the infinite-aspect-ratio (airfoil) approximation neglected finite-span effects such as wingtip vortices and channel wall interactions, which likely influenced the lift regardless of measurement quality or resolution. Future exepriments should mitigate these effects by increasing wing aspect ratio and having greater clearance from the water channel walls to better approximate that two-dimensional flow assumptions.

---

## Tools

- Water channel facility at USC's Rapp Engineering Building
- Dye Flow visualization
- 3D printing with ABS and PETG for components designed with Siemens NX
- Data processing (Python / MATLAB butter filter)

## Read the Formal Report Here!

## Referenced CFD Study
1. H. Tang, Y. Lei, X. Li, and Y. Fu, ‘Numerical Investigation of the Aerodynamic Characteristics
and Attitude Stability of a Bio-Inspired Corrugated Airfoil for MAV or UAV Applications’, Energies,
vol. 12, p. 4021, 10 2019.
2. T. Deubel, S. Wanke, C. Weber, and F. Wedekind, ‘Modelling and Manufacturing of a Dragonfly
Wing as Basis for Bionic Research’, Strojarstvo, vol. 49, 01 2008.

