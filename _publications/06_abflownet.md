---
title: "AbFlowNet: Optimizing Antibody-Antigen Binding Energy via Diffusion-GFlowNet Fusion"
collection: publications
Authors: 'Abrar Rahman Abir<sup>*</sup>, <b>Haz Shahgir</b><sup>*</sup>, Rownok Zahan Ratul, Toki Tahmid, Greg Ver Steeg, Yue Dong'
date: 2026-12-01
venue: 'NeurIPS 2026'
paperurl: 'https://arxiv.org/abs/2505.12358'
codeurl: 'https://github.com/Patchwork53/abflownet'
excerpt: ''
webpage: ''
---
<a href='https://arxiv.org/pdf/2505.12358.pdf' target="_blank">[Download Paper]</a> <a href='https://github.com/Patchwork53/abflownet' target="_blank">[Source Code]</a>

<p align="justify">
Antibody CDR design methods typically optimize reconstruction losses and leave binding energy to a separate, expensive reinforcement-learning stage. AbFlowNet folds GFlowNet training into diffusion: each denoising step is a GFlowNet state, so reconstruction and binding-energy rewards are optimized together. Relative to a diffusion baseline, AbFlowNet improves amino-acid recovery, geometric reconstruction, and the fraction of designs with better binding energy, without online RL or pseudo-labeling the test set.
</p>
