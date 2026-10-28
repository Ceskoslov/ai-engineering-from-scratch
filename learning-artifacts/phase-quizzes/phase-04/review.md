# Phase 04 — computer-vision Review Summary

[All phases](../progress.md)

- Status: **Done / Passed**; passed on 2026-10-24; coverage: **28 lessons**.
- Initial score: **77/84**; final effective score: **80/84 (95.24%)**.
- Cumulative responses: 90, with 82 correct; **8 initial/retake mistakes** retained. Cumulative responses include retakes and are not the mastery-score denominator.
- Pass criteria: effective phase score ≥85% and final score ≥2/3 in every lesson; all criteria met. Completion basis: quiz-based mastery; implementation labs were not performed in this assessment.

## Weak points and review priorities

- Prioritize L20's query hit-rate denominator for this lesson's recall@K protocol: three successful queries out of four give 3/4, not 3/8. This item was still missed in the retake.
- L08: replace both box and mask predictors for custom instance-segmentation classes, including background. L09: fake.detach() blocks only the path back to the generator. L13: PointNet uses a shared MLP and symmetric pooling for permutation invariance.
- L12 temporal order and dense sampling reached 3/3 in the retake. L20 normalized-vector cosine/L2 ranking equivalence and semi-hard negatives were corrected; retain d_ap < d_an < d_ap + margin for spaced recall.

## Lessons with mistakes and retake outcomes

Lessons with mistakes or retakes are listed below, along with any additional rows retained from the original ledger. Unlisted lessons scored 3/3 initially and finally. A final 3/3 indicates correction in a later assessment where applicable; retain those topics for spaced recall. Lessons at 2/3 remain review priorities.

| Lesson | Initial score | Final effective score / retake |
|---|---|---|
| [Image Fundamentals — Pixels, Channels, Color Spaces](../../../phases/04-computer-vision/01-image-fundamentals/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Convolutions from Scratch](../../../phases/04-computer-vision/02-convolutions-from-scratch/docs/en.md) | attempt1: 3/3 | 3/3 |
| [CNNs — LeNet to ResNet](../../../phases/04-computer-vision/03-cnns-lenet-to-resnet/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Image Classification](../../../phases/04-computer-vision/04-image-classification/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Transfer Learning & Fine-Tuning](../../../phases/04-computer-vision/05-transfer-learning/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Object Detection — YOLO from Scratch](../../../phases/04-computer-vision/06-object-detection-yolo/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Semantic Segmentation — U-Net](../../../phases/04-computer-vision/07-semantic-segmentation-unet/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Instance Segmentation — Mask R-CNN](../../../phases/04-computer-vision/08-instance-segmentation-mask-rcnn/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Image Generation — GANs](../../../phases/04-computer-vision/09-image-generation-gans/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Image Generation — Diffusion Models](../../../phases/04-computer-vision/10-image-generation-diffusion/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Stable Diffusion — Architecture & Fine-Tuning](../../../phases/04-computer-vision/11-stable-diffusion/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Video Understanding — Temporal Modeling](../../../phases/04-computer-vision/12-video-understanding/docs/en.md) | attempt1: 1/3 | attempt2: 3/3 |
| [3D Vision — Point Clouds & NeRFs](../../../phases/04-computer-vision/13-3d-vision-nerf/docs/en.md) | attempt1: 2/3 | 2/3 |
| [Vision Transformers (ViT)](../../../phases/04-computer-vision/14-vision-transformers/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Real-Time Vision — Edge Deployment](../../../phases/04-computer-vision/15-real-time-edge/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Build a Complete Vision Pipeline — Capstone](../../../phases/04-computer-vision/16-vision-pipeline-capstone/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Self-Supervised Vision — SimCLR, DINO, MAE](../../../phases/04-computer-vision/17-self-supervised-vision/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Open-Vocabulary Vision — CLIP](../../../phases/04-computer-vision/18-open-vocab-clip/docs/en.md) | attempt1: 3/3 | 3/3 |
| [OCR & Document Understanding](../../../phases/04-computer-vision/19-ocr-document-understanding/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Image Retrieval & Metric Learning](../../../phases/04-computer-vision/20-image-retrieval-metric/docs/en.md) | attempt1: 1/3 | attempt2: 2/3 |
| [Keypoint Detection & Pose Estimation](../../../phases/04-computer-vision/21-keypoint-pose/docs/en.md) | attempt1: 3/3 | 3/3 |
| [3D Gaussian Splatting from Scratch](../../../phases/04-computer-vision/22-3d-gaussian-splatting/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Diffusion Transformers & Rectified Flow](../../../phases/04-computer-vision/23-diffusion-transformers-rectified-flow/docs/en.md) | attempt1: 3/3 | 3/3 |
| [SAM 3 & Open-Vocabulary Segmentation](../../../phases/04-computer-vision/24-sam3-open-vocab-segmentation/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Vision-Language Models — The ViT-MLP-LLM Pattern](../../../phases/04-computer-vision/25-vision-language-models/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Monocular Depth & Geometry Estimation](../../../phases/04-computer-vision/26-monocular-depth/docs/en.md) | attempt1: 3/3 | 3/3 |
| [Multi-Object Tracking & Video Memory](../../../phases/04-computer-vision/27-multi-object-tracking/docs/en.md) | attempt1: 3/3 | 3/3 |
| [World Models & Video Diffusion](../../../phases/04-computer-vision/28-world-models-video-diffusion/docs/en.md) | attempt1: 3/3 | 3/3 |

## Condensed mistake records

Question IDs, prompts, selected wrong answers, correct answers, and explanations are retained. Other distractors, correct-only questions, and per-response score logs are omitted. Prompts and explanations retain their original English wording. These are historical initial/retake mistakes, not pending retake requirements.

### p04-l08-application-v1

Your dataset has four foreground object classes. In the lesson's torchvision Mask R-CNN fine-tuning recipe, how should you configure the replacement predictors?

- Learner answer: A — Replace only the box predictor with4 classes; the pretrained mask predictor automatically adapts.
- Correct answer: B — Replace both box and mask predictors with5 classes, reserving class0 for background.
- Explanation: The recipe replaces both the box predictor and class-specific mask predictor for the new label vocabulary. Four foreground classes require num_classes=5 because index0 is reserved for background; changing the box predictor alone does not adapt mask channels automatically.

### p04-l09-code-v1

Assume G and D are separate networks and G's parameter gradients start as None. After this discriminator backward pass, which statement is correct?

```python
fake = G(z)
fake_logits = D(fake.detach())
loss_d = F.binary_cross_entropy_with_logits(
    fake_logits, torch.zeros_like(fake_logits)
)
loss_d.backward()
```

- Learner answer: B — Gradients reach G but not D because detach freezes the discriminator.
- Correct answer: D — Gradients reach D, while detach blocks this loss's gradient path into G.
- Explanation: fake.detach() disconnects the fake tensor from the generator's computation graph. D still builds its own graph and receives this loss's gradients; the generator receives none from this backward pass. Detach does not freeze D or disable autograd globally.

### p04-l12-concept-v1

A video classifier independently encodes each frame with the same 2D CNN, averages those embeddings, then classifies the result. Why must it give the same prediction for a clip and its exact time reversal, assuming deterministic inference?

- Learner answer: D — A 2D CNN cannot extract any spatial features from individual video frames.
- Correct answer: C — Temporal averaging is unchanged by frame permutation, so it discards their order.
- Explanation: A 2D CNN extracts spatial appearance features from each frame. Averaging the independently computed embeddings is invariant to frame order, so reversing the same frames preserves the pooled representation. The missing information is temporal order, not spatial features.

### p04-l12-application-v1

Your labels distinguish an object moving left-to-right from the same object moving right-to-left. Which setup is best suited to learning this motion direction?

- Learner answer: C — Shuffle every clip's frames randomly and train a temporal model on the shuffled order.
- Correct answer: A — Sample consecutive frames in order and use a 3D convolutional model over time and space.
- Explanation: Consecutive frames in chronological order preserve the motion signal for a 3D convolution over time and space. Randomly shuffling each clip destroys the consistent temporal direction needed to distinguish left-to-right from right-to-left motion.

### p04-l13-concept-v1

A point cloud is an unordered set. How does PointNet produce a global feature that is unchanged when the input points are reordered?

- Learner answer: C — Assign each point a sequence-position embedding, then concatenate features in input order.
- Correct answer: B — Apply the same MLP to each point, then take a coordinate-wise maximum over the point features.
- Explanation: PointNet applies identical shared weights to every point and aggregates with a symmetric coordinate-wise max. Reordering points leaves that maximum unchanged. Sequence-position embeddings and ordered concatenation instead introduce dependence on input order.

### p04-l20-concept-v1

For L2-normalized query and gallery embeddings, how are ranking by highest cosine similarity and ranking by smallest squared Euclidean distance related?

- Learner answer: B — They give opposite rankings because cosine measures an angle rather than a distance.
- Correct answer: C — They give the same ranking because squared distance equals 2 minus twice the cosine similarity.
- Explanation: For unit vectors, squared Euclidean distance is ||a||^2+||b||^2-2*a dot b=2-2*cos(a,b). A higher cosine therefore means a smaller squared distance. Sorting cosine descending and distance ascending yields the same ranking, subject to ties and numerical precision.

### p04-l20-code-v1

This example uses unsquared Euclidean distances, matching the lesson's code implementation. What loss is printed, and does the negative satisfy the stated semi-hard condition d_ap < d_an < d_ap + margin?

```python
d_ap = 0.4
d_an = 0.5
margin = 0.2
loss = max(0.0, d_ap - d_an + margin)
print(round(loss, 2))
```

- Learner answer: D — 0.1; no, because semi-hard negatives must be closer than the positive.
- Correct answer: B — 0.1; yes, because 0.4 < 0.5 < 0.6.
- Explanation: The loss is max(0,0.4-0.5+0.2)=0.1. A semi-hard negative is farther than the positive but still within the margin: 0.4<0.5<0.6. A negative closer than the positive is hard, not semi-hard under this definition.

### p04-l20-code-v2

ID: p04-l20-code-v2
Phase04 — Computer Vision; Lesson20 — Image Retrieval & Metric Learning.
Retake attempt2; lesson question3/3; code tracing.

Under the lesson's recall@K definition (fraction of queries with at least one correct match among the top K), what does this code print? The listed results are from a separate gallery, with no query self-matches.

```python
query_ids = ['A', 'B', 'C', 'D']
top2_ids = [['X', 'A'], ['B', 'Y'], ['X', 'Y'], ['Z', 'D']]
hits = [qid in results for qid, results in zip(query_ids, top2_ids)]
recall_at_2 = sum(hits) / len(hits)
print(recall_at_2)
```

- Learner answer: A — 0.375
- Correct answer: B — 0.75
- Explanation: Queries A,B,andD each have at least one correct match among their top2 results; C does not. The query hit rate is3/4=0.75. Dividing three matches by eight returned items gives0.375, a different statistic, not the lesson's recall@2.
