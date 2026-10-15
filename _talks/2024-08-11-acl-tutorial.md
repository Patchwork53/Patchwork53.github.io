---
title: "ACL 2024 tutorial: Vulnerabilities of large language models to adversarial attacks"
collection: talks
type: "Tutorial"
permalink: /talks/2024-08-11-acl-tutorial
venue: "ACL 2024"
date: 2024-08-11
location: "Bangkok, Thailand"
excerpt: "A tutorial on how safety-aligned language and multimodal models still fail under adversarial pressure, organized around text-only attacks, multimodal attacks, causes, and defenses."
---

I co-presented this [ACL 2024 tutorial](https://llm-vulnerability.github.io/) with Yue Dong’s group. The goal was not to catalog every jailbreak. It was to give NLP researchers a working map of where aligned models still break, and why that map looks the way it does.

Safety training (instruction tuning, RLHF, and related methods) is supposed to make models helpful and harmless. In practice, even strongly aligned systems remain sensitive to adversarial inputs — text-only suffixes, multimodal perturbations, and attacks that treat the model as one component in a larger system. The tutorial walks through that landscape in order:

1. What “aligned” actually means for current LLMs, and how an attacker thinks about the same system.
2. Text-only attacks, including jailbreaks and optimization-based suffixes.
3. Multimodal attacks in both directions: image-to-text and text-to-image.
4. Additional attack surfaces once models are embedded in tools or pipelines.
5. Candidate causes, then the defenses that try to close them.

Materials, slides, and recordings are collected on the [tutorial website](https://llm-vulnerability.github.io/). The ACL Anthology page is [here](https://aclanthology.org/2024.acl-tutorials.5/).
