---
title: "BiRNA-BERT Allows Efficient RNA Language Modeling with Adaptive Tokenization"
collection: publications
Authors: 'Md. Toki Tahmid<sup>*</sup>, <b>Haz Shahgir</b><sup>*</sup>, Sazan Mahbub, Yue Dong, Shamsuzzoha Bayzid'
date: 2025-11-20
venue: 'Nature Communications Biology'
paperurl: 'https://www.nature.com/articles/s42003-025-08982-0'
codeurl: 'https://github.com/buetnlpbio/BiRNA-BERT'
excerpt: ''
webpage: ''
---
<a href='https://www.nature.com/articles/s42003-025-08982-0' target="_blank">[Download Paper]</a> <a href='https://github.com/buetnlpbio/BiRNA-BERT' target="_blank">[Source Code]</a>

<p align="justify">
RNA language models usually have to truncate long sequences, and NLP-style tokenization does not transfer cleanly to nucleotide-level tasks. BiRNA-BERT is a 117M-parameter encoder trained on 36 million RNA sequences with an adaptive dual tokenizer: nucleotide-level encoding for short, structure-sensitive inputs and BPE for long sequences. That lets the model handle arbitrarily long RNAs without truncation, match much larger models on short-sequence tasks, and set strong results on long-sequence downstream work at a fraction of the pretraining compute.
</p>
