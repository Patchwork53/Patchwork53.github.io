---
title: "BiRNA-BERT: Efficient RNA language modeling with adaptive tokenization"
collection: talks
type: "Invited talk"
permalink: /talks/2025-04-07-birnabert
venue: "Mila Multiomics Reading Group"
date: 2025-02-17
location: "Montreal, Canada"
excerpt: "A walkthrough of dual NUC/BPE tokenization for RNA, why truncation is a bad default, and how a 117M-parameter encoder can cover both short structural tasks and arbitrarily long sequences."
---

I presented [BiRNA-BERT](https://www.nature.com/articles/s42003-025-08982-0) at Mila’s Multiomics Reading Group in February 2025. The talk is a practical tour of the modeling choice that matters most here: **tokenization**.

RNA models inherit a transformer habit from NLP — treat the sequence as a list of tokens, then hope the context window is long enough. For RNA that fails in two directions at once. Nucleotide-level tasks (secondary structure, torsion angles) want character resolution. Full-length non-coding RNAs can be far longer than a BERT window, so the usual fix is truncation, which throws away distal context the biology actually uses.

BiRNA-BERT’s answer is an adaptive dual tokenizer. Short or structure-sensitive inputs stay at nucleotide resolution. Long inputs switch to BPE so the same 117M-parameter encoder can run without chopping the sequence. Pretraining on 36 million coding and non-coding RNAs is enough to match much larger models on short tasks and to do well on long-sequence downstream work, at a small fraction of the pretraining compute.

The paper is now in [*Nature Communications Biology*](https://www.nature.com/articles/s42003-025-08982-0). Code and weights are on [GitHub](https://github.com/buetnlpbio/BiRNA-BERT).

<iframe src="https://docs.google.com/presentation/d/e/2PACX-1vQHW_tNTxUZSSawHEA952PqCsfPEo0IW9TBOKaF1Gv9iue_N83gKIrja2G_fB31FbMDvcw_pgW95-oi/embed?start=false&loop=false&delayms=3000" frameborder="0" width="960" height="569" allowfullscreen="true" mozallowfullscreen="true" webkitallowfullscreen="true"></iframe>
