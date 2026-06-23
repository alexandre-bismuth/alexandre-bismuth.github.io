---
title: "Bachelor Thesis: Optimising Gunshot Detection in Tropical Forests for Wildlife Protection with TinyML"
date: 2025-04-01
tags: []
author: "Alexandre Bismuth"
description: "Bachelor thesis: real-time, on-device gunshot detection for tropical forests using TinyML."
summary: "Bachelor thesis supervised by Professor Alex Rogers developing a two-stage gunshot detection pipeline for tropical forests in a low-power Arduino microcontroller through model compression and knowledge distillation."
cover:
    image: "bachelor-thesis-cover.jpeg"
    alt: "A hunter in a tropical forest detected by a low-power TinyML acoustic sensor"
---

---

*Advisor: Professor Alex Rogers, St Anne's College, University of Oxford.*

<div class="buttons" style="display:flex;flex-wrap:wrap;justify-content:space-between;gap:10px;margin:14px 0 10px 0;">
  <a class="button" style="flex:1;text-align:center;margin:0;padding:5px 10px;background:rgba(0,0,0,0.1);" href="thesis.pdf"><span class="button-inner">Thesis</span></a>
  <a class="button" style="flex:1;text-align:center;margin:0;padding:5px 10px;background:rgba(0,0,0,0.1);" href="defense-slides.pdf"><span class="button-inner">Defense slides</span></a>
  <a class="button" style="flex:1;text-align:center;margin:0;padding:5px 10px;background:rgba(0,0,0,0.1);" href="https://github.com/alexandre-bismuth/BachelorThesis"><span class="button-inner">Code</span></a>
</div>

---

##### Overview

Unsustainable hunting is one of the leading factors of the acceleration of biodiversity loss, prompting the creation of wildlife protection laws in countries home to vast tropical forests. In this context, acoustic detection using low-cost audio loggers offers a practical way to monitor hunting pressure over wide areas.

I optimise a two-stage unconstrained pipeline that employs EfficientNets and Mel Spectrograms for gunshot detection in tropical forests, achieving a **5.72% improvement in F1 score** and a **6.67% improvement in AUPRC** over the current state-of-the-art. To address the storage and real-time limitations of such a system, I then leverage AI-oriented microcontrollers to provide real-time detection and immediate alerts. The resulting compact model, deployable on an **Arduino Nano 33 BLE Sense Rev2**, achieves an **F1 score of 0.840** and an **AUPRC score of 0.849** — offering near state-of-the-art accuracy while drastically reducing computational costs.

Leveraging TinyML for on-device inference, this approach mitigates storage bottlenecks while enabling instant alerts, yielding a scalable, real-time solution that closes the loop between data collection and active law enforcement.

---

##### Contributions

1. **Analytical framework** — crafting a ReLU network that approximates a gunshot signal with any error, providing indications regarding minimal model complexity.
2. **Unconstrained pipeline** — optimising gunshot detection through experimentations with various preprocessing methods and adjustments in model architectures.
3. **Lightweight architecture** — designing gunshot detection systems for embedded devices by combining efficient design choices with model compression methods.

---

##### Comparing preprocessing methods

A comparative study of preprocessing methods (power spectrograms, Mel spectrograms, raw waveforms, LFCCs, and MFCCs) determines how best to capture the distinctive audio signature of a gunshot before classification.

![Comparing preprocessing methods](preprocessing.png)

---

##### A TinyML model for biodiversity protection

Through knowledge distillation from the optimised EfficientNetB3 teacher and a model compression pipeline, the compact convolutional network is squeezed to ≈115 thousand parameters so that it fits within the ≈900 kB of storage and 256 kB of RAM available after compression on the Arduino device.

![Architecture of the TinyML convolutional neural network](architecture.png)

---

##### Key results

+ Optimised pipeline outperforms the current state-of-the-art by **5.72% in F1 score** and **6.67% in AUPRC**.
+ Knowledge distillation lifts the on-device student model by **12.0% in F1 score** and **5.6% in AUPRC**.
+ Final compression yields a **91.4%** reduction to a TensorFlow Lite model and a C header file deployable on the Arduino Nano 33 BLE Sense Rev2.
