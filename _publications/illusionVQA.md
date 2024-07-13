---
title: "IllusionVQA: A Challenging Optical Illusion Dataset for Vision Language Models"
collection: publications
permalink: /publication/illusionVQA
excerpt: 'This paper presents IllusionVQA, a diverse dataset of challenging optical illusions and hard-to-interpret scenes to test the capability of Vision Language Models in comprehension and soft localization tasks.'
date: 2024-03-23
venue: 'Conference On Language Modeling 2024'
paperurl: 'https://arxiv.org/pdf/2403.15952.pdf'
citation: 'Shahgir, H. S., Sayeed, K. S., Bhattacharjee, A., Ahmad, W. U., Dong, Y., & Shahriyar, R. (2024). &quot;IllusionVQA: A Challenging Optical Illusion Dataset for Vision Language Models.&quot; <i>COLM 2024</i>.'
---
The advent of Vision Language Models (VLM) has allowed researchers to investigate the visual understanding of a neural network using natural language. Beyond object classification and detection, VLMs are capable of visual comprehension and common-sense reasoning. This naturally led to the question: How do VLMs respond when the image itself is inherently unreasonable? To this end, we present IllusionVQA: a diverse dataset of challenging optical illusions and hard-to-interpret scenes to test the capability of VLMs in two distinct multiple-choice VQA tasks - comprehension and soft localization. GPT4V, the best-performing VLM, achieves 62.99% accuracy (4-shot) on the comprehension task and 49.7% on the localization task (4-shot and Chain-of-Thought). Human evaluation reveals that humans achieve 91.03% and 100% accuracy in comprehension and localization. We discover that In-Context Learning (ICL) and Chain-of-Thought reasoning substantially degrade the performance of GeminiPro on the localization task. Tangentially, we discover a potential weakness in the ICL capabilities of VLMs: they fail to locate optical illusions even when the correct answer is in the context window as a few-shot example.

[Download paper here](https://arxiv.org/pdf/2403.15952.pdf)

Recommended citation: Shahgir, H. S., Sayeed, K. S., Bhattacharjee, A., Ahmad, W. U., Dong, Y., & Shahriyar, R. (2024). "IllusionVQA: A Challenging Optical Illusion Dataset for Vision Language Models." <i>COLM 2024</i>.