---
title: "Can Fine-Tuned Vision-Language Models Generalize Across Tasks on the Same Images?"
collection: talks
type: "Pilot experiments"
permalink: /talks/2025-04-07-vlm-generalization
venue: "Research notes"
date: 2025-04-06
location: "Riverside, CA"
excerpt: "A small experiment on whether fine-tuning a vision-language model for one visual task helps it handle other tasks on the same images."
---

A detailed caption can generate many questions about an image. But how many of those questions do we need for useful training? If a model learns to count objects, does it also learn to locate them? If it learns to count objects of one color, can it count objects of a particular shape?

These questions matter because training data often treats each image-question pair as a separate example, even when several questions draw on the same visual content. I ran a small experiment to see whether fine-tuning on one task transfers to other tasks over the same images.

Many vision-language models (VLMs) use a vision encoder aligned with text through a contrastive objective such as CLIP. Pooling patch-level image features can discard fine detail, while captions used during alignment may leave out details that later tasks require. Despite this, VLMs can perform well on OCR. Their weaknesses are more visible on tasks that depend on precise visual relationships, such as chart understanding and spatial reasoning.

## Experiment question

The experiment asks whether training on a subset of questions can help a model use an image more broadly. For example, does training on object counts transfer to locating objects, or does training on color counts transfer to shape counts?

The central idea is **image reuse during training**: when one image supports many possible questions, does a model benefit from seeing more of those questions, or can a few representative tasks teach it to use the image more effectively?

## Synthetic task design

To control the visual details and question types, I generated 1,000 scenes in Blender using [this script](https://github.com/dali-does/clevr-math). Each scene contains 3–8 objects with randomized shapes, colors, materials, and sizes. Here is one example of the scene attributes:

```json
{
  "shapes": ["cube", "sphere", "cylinder"],
  "colors": ["gray", "red", "blue", "green", "brown", "purple", "cyan", "yellow"],
  "materials": ["rubber", "metal"],
  "sizes": ["large", "small"]
}
```

I designed eight tasks:

- **Extreme material, color, or shape:** identify the property of the leftmost, rightmost, farthest, or nearest object.
- **Extreme all:** identify the leftmost, rightmost, farthest, or nearest object and report its size, color, material, and shape.
- **Count material, color, or shape:** count objects with a specified property.
- **Count relative to:** count objects positioned to one side of, closer than, or farther than a specified object.

For people, I expected relative counting to be hardest because it requires finding a reference object before counting. Simple property counts should be easier, followed by identifying one property at an extreme. Identifying all four properties of an extreme object also requires a longer, precisely formatted answer, which may make it difficult for a VLM.

## Data and models

I used 800 images for training and held out 200 for testing. For evaluation, I sampled up to 1,500 questions per task from each split. I compared training on all eight tasks with training on one task at a time, including a balanced setting with about 188 examples per task (roughly 1,500 total).

The models were Qwen2-VL-2B-Instruct and Llama-3.2-11B-Vision-Instruct, both in 4-bit form. I fine-tuned each model for two epochs with QLoRA using Unsloth, keeping the vision encoder frozen. The in-domain evaluation uses images seen during training; the out-of-domain evaluation uses the held-out images.

## Results at a glance

The results suggest that fine-tuning can transfer across tasks on these synthetic scenes, though the size and direction of that transfer depend on the model and task. In the Llama evaluation, training on the **Extreme Color** task reached about 58% of the gain from training on all eight tasks, while also improving several other tasks.

A few patterns stood out:

- Training on all tasks together generally performed best.
- For Llama, performance was similar on the in-domain and held-out image sets, suggesting that the gains were not limited to memorizing the training images.
- With a budget of roughly 1,500 examples, training on Extreme Color performed comparably to splitting the budget across all eight tasks in the reported comparison.
- Qwen2-VL-2B showed little or inconsistent improvement on several tasks, suggesting that transfer also depends on the model’s starting capabilities.

These are pilot results from a controlled synthetic setting. They do not establish that the same transfer patterns will hold for natural images or other models, but they offer a useful way to study how much visual skill a model can reuse across tasks.

## Detailed results

### In-domain evaluation

Baseline and fine-tuned accuracy for Llama-3.2-11B-Vision-Instruct. Each cell shows accuracy.

![In-domain accuracy across tasks and training settings for Llama-3.2-11B-Vision-Instruct.]({{ site.baseurl }}/images/talks/vlm-generalization/accuracy-in-domain.webp)

Cross-task transfer after fine-tuning Llama-3.2-11B-Vision-Instruct on one task. Each cell shows the fraction of the improvement from full fine-tuning recovered by one-task fine-tuning:

`(one-task accuracy − baseline accuracy) / (all-task accuracy − baseline accuracy) × 100%`

![Cross-task transfer scores for Llama-3.2-11B-Vision-Instruct on in-domain images.]({{ site.baseurl }}/images/talks/vlm-generalization/transfer-in-domain.webp)

### Held-out images

Baseline and fine-tuned accuracy for Llama-3.2-11B-Vision-Instruct on held-out images. Each cell shows accuracy.

![Accuracy across tasks and training settings for Llama-3.2-11B-Vision-Instruct on held-out images.]({{ site.baseurl }}/images/talks/vlm-generalization/accuracy-held-out.webp)

Cross-task transfer on held-out images after fine-tuning on one task, using the same transfer score defined above.

![Cross-task transfer scores for Llama-3.2-11B-Vision-Instruct on held-out images.]({{ site.baseurl }}/images/talks/vlm-generalization/transfer-held-out.webp)

## Strongest cross-task transfer

Held-out images. Yellow marks the test task that benefited most from each training task, excluding the matching task.

![Held-out cross-task transfer matrix with the strongest transfer for each training task highlighted.]({{ site.baseurl }}/images/talks/vlm-generalization/strongest-transfer.webp)

<details class="vlm-results" markdown="1">
<summary>Show complete per-task results for both models (four tables)</summary>

## Complete score tables

Each cell reports accuracy; **N** is the number of questions. “All tasks” columns show multitask fine-tuning with two data budgets. The remaining columns show fine-tuning on one task at a time.

### Qwen2-VL-2B-Instruct-bnb-4bit
**In-domain images**

| Task | N | Baseline | All (1,500/task) | All (188/task) | Extreme material | Extreme color | Extreme shape | Extreme all | Count material | Count color | Count shape | Count relative |
|:--|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|
| Extreme Material | 364 | 0.5137362637362637 | 0.47527472527472525 | 0.5357142857142857 | 0.4807692307692308 | 0.5576923076923077 | 0.5274725274725275 | 0.41208791208791207 | 0\.554945054945055 | 0.510989010989011 | 0.5054945054945055 | 0.554945054945055 |
| Extreme Color | 420 | 0.11190476190476191 | 0.1523809523809524 | 0.15 | 0.1380952380952381 | 0.15476190476190477 | 0.14047619047619048 | 0.11666666666666667 | 0\.1738095238095238 | 0.14523809523809525 | 0.1619047619047619 | 0.14285714285714285 |
| Extreme Shape | 378 | 0.31746031746031744 | 0.3412698412698413 | 0\.30423280423280424 | 0.328042328042328 | 0.30952380952380953 | 0.31216931216931215 | 0.29894179894179895 | 0\.3439153439153439 | 0.36243386243386244 | 0.34656084656084657 | 0.3862433862433862 |
| Extreme All | 412 | 0.014563106796116505 | 0.009708737864077669 | 0\.01699029126213592 | 0.11407766990291263 | 0.009708737864077669 | 0.0048543689320388345 | 0.0048543689320388345 | 0\.007281553398058253 | 0.012135922330097087 | 0.009708737864077669 | 0.012135922330097087 |
| Count Material | 184 | 0.2391304347826087 | 0.25 | 0\.24456521739130435 | 0.010869565217391304 | 0.24456521739130435 | 0.25 | 0.25 | 0\.2554347826086957 | 0.21739130434782608 | 0.24456521739130435 | 0.1956521739130435 |
| Count  Color | 386 | 0.27202072538860106 | 0.07512953367875648 | 0\.07512953367875648 | 0.12435233160621761 | 0.04404145077720207 | 0.11658031088082901 | 0.38341968911917096 | 0\.054404145077720206 | 0\.5103626943005182 | 0.33678756476683935 | 0.0  |
| Count Shape | 261 | 0.2835249042145594 | 0.22988505747126436 | 0\.22988505747126436 | 0.23371647509578544 | 0.22988505747126436 | 0.26053639846743293 | 0.2950191570881226 | 0\.22988505747126436 | 0.3333333333333333 | 0.3103448275862069 | 0.0038314176245210726 |
| Count Relative To | 395 | 0.09367088607594937 | 0.16455696202531644 | 0.16455696202531644 | 0.015189873417721518 | 0.1670886075949367 | 0.1949367088607595 | 0.21012658227848102 | 0\.17215189873417722 | 0\.16455696202531644 | 0.15443037974683543 | 0.22025316455696203  |
{: .vlm-results-table}

**Held-out images**

| Task | N | Baseline | All (1,500/task) | All (188/task) | Extreme material | Extreme color | Extreme shape | Extreme all | Count material | Count color | Count shape | Count relative |
|:--|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|
| Extreme Material | 400 | 0.53 | 0.505 | 0.5225 | 0.5025 | 0.4825 | 0.4975 | 0.4475 | 0\.515 | 0.5 | 0.4975 | 0.495  |
| Extreme Color | 400 | 0.0825 | 0.1525 | 0.1275  | 0.1425  | 0.165 | 0.1525 | 0.065  | 0\.1725 | 0.15 | 0.1575 | 0.15  |
| Extreme Shape | 400 | 0.335 | 0.35 | 0.34  | 0.3525 | 0.3575 | 0.3375 | 0.31 | 0\.3275 | 0.3225  | 0.345 | 0.3075 |
| Extreme All | 400 | 0.015 | 0.0175 | 0.0075 | 0.11 | 0.0125 | 0.005 | 0.0075 | 0\.02 | 0.025 | 0.0.01 | 0.015 |
| Count Material | 190 | 0.24210526315789474 | 0.22631578947368422 | 0.22105263157894736 | 0.042105263157894736 | 0.22631578947368422 | 0.22631578947368422 | 0.24210526315789474 | 0\.21052631578947367 | 0.23684210526315788 | 0.2578947368421053 | 0.1736842105263158 |
| Count  Color | 423 | 0.13947990543735225 | 0.2458628841607565 | 0\.2458628841607565 | 0.11583924349881797 | 0.18439716312056736 | 0.13711583924349882 | 0.20803782505910165 | 0\.09929078014184398 | 0.5791962174940898 | 0.34278959810874704 | 0.06619385342789598 |
| Count Shape | 254 | 0.2440944881889764 | 0.2283464566929134 | 0\.2283464566929134 | 0.2283464566929134 | 0.1968503937007874 | 0.21653543307086615 | 0.18503937007874016 | 0\.22440944881889763 | 0.28346456692913385 | 0.33070866141732286 | 0.051181102362204724 |
| Count Relative To | 400 | 0.035 | 0.1625 | 0\.1725 | 0.0925 | 0.1375 | 0.175 | 0.0625 | 0.1475 | 0.2175 | 0\.2075 | 0.21 |
{: .vlm-results-table}

### Llama-3.2-11B-Vision-Instruct-bnb-4bit

**In-domain images**

| Task | N | Baseline | All (1,500/task) | All (188/task) | Extreme material | Extreme color | Extreme shape | Extreme all | Count material | Count color | Count shape | Count relative |
|:--|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|
| Extreme Material | 364 | 0.06868131868131869 | 0.9010989010989011   | 0.6126373626373627 | 0.760989010989011 | 0.5934065934065934 | 0.5714285714285714 | 0.046703296703296704 | 0.510989010989011 | 0.4423076923076923 | 0.2774725274725275 | 0.5274725274725275 |
| Extreme Color | 420 | 0.04285714285714286 | 0.9404761904761905    | 0.8071428571428572 | 0.10476190476190476 | 0.8357142857142857 | 0.5880952380952381 | 0.1 | 0.37142857142857144 | 0.4880952380952381 | 0.41904761904761906 | 0.45714285714285713 |
| Extreme Shape | 378 | 0.2037037037037037 | 0.91005291005291   | 0.8174603174603174 | 0.6746031746031746 | 0.8042328042328042 | 0.8835978835978836 | 0.013227513227513227 | 0.5873015873015873 | 0.6798941798941799 | 0.6322751322751323 | 0.42328042328042326 |
| Extreme All | 412 | 0.02912621359223301                                                                                                                                                                           | 0.8470873786407767 | 0.4684466019417476 | 0.0048543689320388345 | 0.09223300970873786 | 0.019417475728155338 | 0.5922330097087378 | 0.03398058252427184 | 0.07766990291262135 | 0.0412621359223301 | 0.18446601941747573 |
| Count Material | 184 | 0.10869565217391304 | 0.532608695652174  | 0.3804347826086957 | 0.358695652173913 | 0.28804347826086957 | 0.07608695652173914 | 0.0 | 0.45108695652173914 | 0.266304347826087 | 0.266304347826087 | 0.2608695652173913 |
| Count  Color | 386 | 0.266839378238342 | 0.9145077720207254 | 0.7616580310880829 | 0\.6295336787564767 | 0.7590673575129534 | 0.6528497409326425 | 0.0025906735751295338 | 0.5155440414507773 | 0.8523316062176166 | 0.7694300518134715 | 0.2772020725388601 |
| Count Shape | 261 | 0.26053639846743293       | 0.7279693486590039                | 0.5172413793103449 | 0.4099616858237548 | 0.46360153256704983 | 0.25287356321839083 | 0.007662835249042145 | 0.3448275862068966 | 0.5517241379310345 | 0.6398467432950191 | 0.26053639846743293 |
| Count Relative To | 395 | 0.12658227848101267 | 0.46329113924050636  | 0.21518987341772153 | 0.22784810126582278 | 0.22278481012658227 | 0.12658227848101267 | 0.0 | 0.22784810126582278 | 0.20506329113924052 | 0\.18227848101265823 | 0.18734177215189873 |
{: .vlm-results-table}

**Held-out images**

| Task | N | Baseline | All (1,500/task) | All (188/task) | Extreme material | Extreme color | Extreme shape | Extreme all | Count material | Count color | Count shape | Count relative |
|:--|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|--:|
| Extreme Material | 364 | 0.06   | 0.915  | 0.6225 | 0.8275 | 0.6075 | 0.6525 | 0.07  | 0.5425 | 0.5075 | 0.3675 | 0\.5175 |
| Extreme Color | 420 | 0.04   | 0.9075 | 0.8025 | 0.0975 | 0.8725 | 0.59 | 0.06 | 0.385 | 0.535 | 0.4675  | 0\.4825 |
| Extreme Shape | 378 | 0.195   | 0.9025     | 0.835 | 0.6875  | 0.82  | 0.91 | 0.015  | 0.665 | 0.68 | 0.6625 | 0\.415 |
| Extreme All | 412 | 0.035     | 0.8125 | 0.4375 | 0.005 | 0.0925 | 0.0175 | 0.56  | 0.0475 | 0.075 | 0.025  | 0.2 |
| Count Material | 184 | 0.08421052631578947  | 0.45263157894736844 | 0.3473684210526316 | 0.2789473684210526 | 0.23157894736842105 | 0.11052631578947368 | 0.0 | 0.4368421052631579 | 0.2631578947368421 | 0.2789473684210526 | 0.22105263157894736 |
| Count  Color | 386 | 0.22695035460992907 | 0.9243498817966903    | 0.8297872340425532 | 0.6335697399527187 | 0.7825059101654847 | 0.7092198581560284 | 0.002364066193853428 | 0.4846335697399527 | 0.91725768321513 | 0.8297872340425532  | 0.2907801418439716 |
| Count Shape | 261 | 0.2795275590551181       | 0.7559055118110236 | 0.5 | 0.44881889763779526 | 0.5039370078740157 | 0.24015748031496062 | 0.007874015748031496 | 0.3543307086614173 | 0.6377952755905512 | 0.6220472440944882 | 0.2795275590551181 |
| Count Relative To | 395 | 0.1425    | 0.4275   | 0.2325 | 0.1925 | 0.15 | 0.17 | 0.0 | 0.205 | 0.22 | 0.2175  | 0\.195 |
{: .vlm-results-table}

</details>
