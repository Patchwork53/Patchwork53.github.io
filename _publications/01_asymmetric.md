---
title: "Asymmetric Bias in Text-to-Image Generation with Adversarial Attacks"
collection: publications
Authors: '<b>Haz Sameen Shahgir</b>, Xianghao Kong, Greg Ver Steeg, Yue Dong.'
date: 04/2024
venue: 'Findings of ACL 2024'
paperurl: 'https://arxiv.org/pdf/2312.14440.pdf'
codeurl: 'https://github.com/Patchwork53/AsymmetricAttack'
excerpt: ''
webpage: ''
---
---
<a href='https://arxiv.org/pdf/2312.14440.pdf' target="_blank">[Download Paper]</a><a href='https://github.com/Patchwork53/AsymmetricAttack' target="_blank">[Source Code]</a>

<p align="justify">
The widespread use of Text-to-Image (T2I) models in content generation requires careful examination of their safety, including their robustness to adversarial attacks. Despite extensive research into this, the reasons for their effectiveness are underexplored. This paper presents an empirical study on adversarial attacks against T2I models, focusing on analyzing factors associated with attack success rates (ASRs). We introduce a new attack objective - entity swapping using adversarial suffixes and two gradient-based attack algorithms. Human and automatic evaluations reveal the asymmetric nature of ASRs on entity swap: for example, it is easier to replace "human" with "robot" in the prompt "a human dancing in the rain." with an adversarial suffix but is significantly harder in reverse. We further propose probing metrics to establish indicative signals from the model's beliefs to the adversarial ASR. We identify conditions resulting in a 60% success probability for adversarial attacks and others where this likelihood drops below 5%.
</p>
