---
title: "Cardiac Sex Differences and Antidepressant-Induced Arrhythmias"
date: 2026-03-14
tags: []
author: "Alexandre Bismuth"
description: "Computational Medicine mini-project: using in-silico cardiomyocyte models to quantify how electrophysiologic sex differences affect vulnerability to antidepressant-induced arrhythmias."
summary: "Computational Medicine mini-project at the University of Oxford. Uses the ToR-ORd cardiomyocyte model and a population-of-models approach to show that female hearts are quantifiably more vulnerable to antidepressant-induced arrhythmias, supporting sex-differentiated prescription guidelines."
cover:
    image: "cover.png"
    alt: "Action potentials showing early afterdepolarisations in female but not male cardiomyocytes"
---

---

*Computational Medicine, MSc in Advanced Computer Science, University of Oxford.*

<div class="buttons" style="display:flex;flex-wrap:wrap;justify-content:space-between;gap:10px;margin:14px 0 10px 0;">
  <a class="button" style="flex:1;text-align:center;margin:0;padding:5px 10px;background:rgba(0,0,0,0.1);" href="report.pdf"><span class="button-inner">Report</span></a>
  <a class="button" style="flex:1;text-align:center;margin:0;padding:5px 10px;background:rgba(0,0,0,0.1);" href="https://github.com/alexandre-bismuth/Computational-Medicine/tree/main/Mini-Project"><span class="button-inner">Code</span></a>
</div>

---

##### Overview

While antidepressant prescriptions have tripled in 20 years, their cardiac ion channel block — which can trigger arrhythmias such as Torsades de Pointes — remains under-evaluated, particularly for women whose reduced baseline *I<sub>Kr</sub>* elevates risk not accounted for in current sex-neutral models and prescribing guidelines. This study leverages the ToR-ORd ventricular cell model to quantify how electrophysiological sex differences affect vulnerability to arrhythmias induced by sertraline (an SSRI), amitriptyline and desipramine (two TCAs).

We find that female models develop early afterdepolarisations at therapeutic doses whereas male models do not; sertraline shows the greatest risk followed by amitriptyline, while desipramine remains EAD-free due to compensatory *I<sub>CaL</sub>* block. These results provide sex-differentiated evidence of quantifiably higher antidepressant-induced arrhythmic risk for women.

---

##### Method: a population of in-silico hearts

ToR-ORd represents cardiomyocytes on MATLAB by capturing depolarisation, repolarisation, and calcium dynamics through the Hodgkin-Huxley framework, where ionic currents are modelled as conductance-gating products and drug effects are captured by the Hill equation. Rather than relying on a single average-patient simulation, the study combines it with a population-of-models approach — generating 30 samples per sex with Latin Hypercube Sampling over seven ion channel conductances — which detects minority cases that average simulations miss. Sex differences are introduced by scaling six ionic conductances in line with existing literature, notably reducing *I<sub>Kr</sub>* by 18% for female models. To bridge single-cell results to clinical ECGs, single-cell *APD*<sub>90</sub> is mapped to QTc and validated against PTB-XL, a public dataset of 21,837 annotated 12-lead ECGs filtered down to 8,798 normal records. To keep the pipeline reproducible, IC<sub>50</sub> values and Hill coefficients are taken from published literature and the sampling seed is fixed.

<figure style="margin:10px auto;text-align:center;">
  <img src="action-potentials.png" alt="Action potentials of male (left) and female (right) populations at the maximum therapeutic dose of sertraline" style="width:100%;">
  <figcaption style="font-size:0.82em;opacity:0.75;margin-top:6px;">Action potentials at the maximum therapeutic dose of sertraline — <strong>left: male patients</strong>, <strong>right: female patients</strong>.</figcaption>
</figure>

Sex-driven additional arrhythmia risk is evident from the early afterdepolarisations (EADs) — the secondary depolarising humps — observed in a subset of the female population (right) at the maximum therapeutic dose of sertraline, which are entirely absent in the male population (left).

---

##### Arrhythmia is driven by I<sub>Kr</sub> block

Varying the basic cycle length shows that sertraline is more dangerous at rest: at slower heart rates, *I<sub>Kr</sub>* block yields longer action potentials, allowing calcium channels to recover from inactivation and re-activate early, creating EADs. Comparing the three compounds isolates the mechanism — sertraline's lower *I<sub>Kr</sub>* IC<sub>50</sub> achieves the strongest fractional hERG block and the highest risk, while desipramine triggers no EADs despite producing 73% greater *APD*<sub>90</sub> prolongation than amitriptyline, because its compensatory *I<sub>CaL</sub>* block reduces the inward current that sustains the plateau and triggers EADs. This directly supports the claim that QTc prolongation alone is an insufficient predictor of arrhythmic risk. Baseline and drug-induced *APD*<sub>90</sub> nonetheless correlate closely, and the top 23% of female models show extreme prolongation (3× longer than the bottom 80%) — a boundary used to define a simulation-derived risk threshold.

![EAD incidence across heart rates and baseline versus drug-induced APD90](ead-incidence.png)

---

##### Mapping simulation onto real ECGs

Applying the simulation-derived risk threshold to 8,705 normal PTB-XL ECGs, **20% of women fall into the elevated-risk category compared to only 14% of men** — a split that closely matches the simulation data to within 3%. Comparing both sexes across all antidepressants and dosages confirms that women consistently experience greater QTc prolongation. The model is stress-tested for credibility: baseline *APD*<sub>90</sub> reproduces the known sex gap in normal PTB-XL ECGs, the QTc-prolongation ranking aligns with clinical thresholds distinguishing torsadogens, and varying the most sensitive parameters (IC<sub>50</sub> by ±25% and the female *I<sub>Kr</sub>* factor by ±10%) leaves the ranking intact, with women remaining the only patients to trigger EAD.

![QTc distributions and prolongation by drug and therapeutic dose in PTB-XL](qtc-violin.png)

---

##### Key results

+ Female cardiomyocyte models develop early afterdepolarisations at therapeutic antidepressant doses, whereas male models do not.
+ Arrhythmic risk is driven by **I<sub>Kr</sub> block**, with sertraline the most cardiotoxic and desipramine EAD-free despite greater *APD*<sub>90</sub> prolongation — showing QTc prolongation alone is an insufficient predictor.
+ Mapping onto 8,705 PTB-XL ECGs places **20% of women vs 14% of men** in the elevated-risk tier, supporting sex-differentiated prescription guidelines.
