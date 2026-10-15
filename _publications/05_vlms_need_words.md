---
title: "VLMs Need Words: Vision-Language Models Ignore Visual Detail in Favor of Semantic Anchors"
collection: publications
Authors: '<b>Haz Shahgir</b>, Xiaofu Chen, Yu Fu, Erfan Shayegani, Nael Abu-Ghazaleh, Yova Kementchedjhieva, Yue Dong'
date: 2026-10-01
venue: 'COLM 2026'
paperurl: 'https://arxiv.org/abs/2604.02486'
codeurl: 'https://github.com/Patchwork53/VLMs-Need-Words-COLM2026'
excerpt: ''
webpage: ''
---
<a href='https://arxiv.org/pdf/2604.02486.pdf' target="_blank">[Download Paper]</a> <a href='https://github.com/Patchwork53/VLMs-Need-Words-COLM2026' target="_blank">[Source Code]</a>

<p align="justify">
Vision-language models often fail at fine-grained visual tasks even when the needed information is present in their representations. We show that this gap comes from a language shortcut: when visual entities can be mapped to known names, VLMs skip pixel-level comparison and reason in language; when they cannot, they fall back on brittle, hallucinated descriptions. Across semantic correspondence, synthetic shape matching, and face matching, models do much better on nameable entities than unnameable ones. Teaching arbitrary names helps, and task-specific finetuning yields still stronger generalization through genuine visual comparison. The takeaway is that current failures look more like a learned training shortcut than a hard architectural limit.
</p>
