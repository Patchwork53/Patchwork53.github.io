---
title: "D-Judge: Disrupting Multi-Turn Jailbreaks using Semantics-Preserving Output Rewriting"
collection: publications
Authors: 'Huanli Gong<sup>*</sup>, Zhipeng Wei<sup>*</sup>, Yu Fu, <b>Haz Shahgir</b>, Ananya Gupta, Yue Dong, N. Benjamin Erichson'
date: 2026-07-01
venue: 'ICML 2026'
paperurl: 'https://arxiv.org/abs/2606.02640'
codeurl: 'https://github.com/Huanli-Gong/D-Judge'
excerpt: ''
webpage: ''
---
<a href='https://arxiv.org/pdf/2606.02640.pdf' target="_blank">[Download Paper]</a> <a href='https://github.com/Huanli-Gong/D-Judge' target="_blank">[Source Code]</a>

<p align="justify">
Multi-turn jailbreaks succeed in part because attackers use an auxiliary judge to score intermediate replies and refine the next prompt. D-Judge sits in that loop: it rewrites the victim model’s output before the judge sees it, keeping the meaning (checked by a semantic gate) while changing the harmfulness signal the attacker relies on. Trained with SFT and DPO on semantically equivalent pairs that induce different judge scores, D-Judge lowers the success of strong multi-turn attacks on HarmBench without collapsing benign benchmark performance.
</p>
