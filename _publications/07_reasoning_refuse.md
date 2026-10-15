---
title: "Do Reasoning LLMs Refuse What They Infer in Long Contexts?"
collection: publications
Authors: 'Yu Fu, <b>Haz Shahgir</b>, Zhipeng Wei, Huanli Gong, N. Benjamin Erichson, Yue Dong'
date: 2026-12-02
venue: 'NeurIPS 2026'
paperurl: 'https://arxiv.org/abs/2602.08874'
codeurl: ''
excerpt: ''
webpage: ''
---
<a href='https://arxiv.org/pdf/2602.08874.pdf' target="_blank">[Download Paper]</a>

<p align="justify">
Long-context models can infer goals that are never stated in a single sentence. That is useful for documents and tool traces, but it is also a safety hole: harmful intent can be split across a context and become visible only after the model composes the pieces. We introduce compositional reasoning attacks, where harmful requests are broken into incomplete fragments and the final query stays neutral. Across 15 frontier models and contexts up to 64k tokens, models usually refuse explicit harmful requests, but refusal drops sharply when the same objective has to be inferred. Extra test-time reasoning helps, but it does not close the gap.
</p>
