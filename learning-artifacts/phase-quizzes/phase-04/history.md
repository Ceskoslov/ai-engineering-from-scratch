# Phase 04 detailed quiz history

Archive: read only when an earlier question or attempt is relevant. [Phase progress](progress.md).

### Phase04 assessment started — 2026-10-24

English questions; three scored questions per lesson across28 lessons,84 total. Pass requires at least72/84 overall and at least2/3 per lesson. All lessons remain todo until the full phase passes. Phases00–03 remain done.

### Answer history: p04-l01-concept-v1

ID: p04-l01-concept-v1
Phase04 — Computer Vision; Lesson01 — Image Fundamentals — Pixels, Channels, Color Spaces.
Question1/84; lesson question1/3; conceptual.

An image keeps the same height and width, but its intensity encoding changes from8 bits to12 bits per channel. What improves directly?

A) Spatial resolution, because the image now contains more pixel locations.
B) The number of color channels, because each pixel gains four additional channels.
C) Intensity quantization precision, increasing possible levels per channel from256 to4096.
D) Spatial anti-aliasing, because additional intensity bits recover detail missed by sampling.


Learner answer: c (normalized C). Correct answer: C. Result: correct.
Explanation: Bit depth controls intensity quantization:2**8=256 levels and2**12=4096 levels per channel. It does not increase spatial samples or channel count, or recover spatial detail lost during acquisition. Converting an existing8-bit image to12-bit storage alone does not recover previously lost intensity information.
Phase04 running initial score: 1/1. Lesson01 attempt1: 1/1; incomplete.

### Answer history: p04-l01-application-v1

ID: p04-l01-application-v1
Phase04 — Computer Vision; Lesson01 — Image Fundamentals.
Question2/84; lesson question2/3; application.

You resize a semantic-segmentation mask whose pixel values are integer class IDs, such as0,1,2. Which interpolation should you use to preserve categorical labels?

A) Nearest-neighbor interpolation, because it selects existing class IDs without blending them.
B) Bilinear interpolation, because averaging class IDs produces meaningful intermediate classes.
C) Bicubic interpolation, because its smoothness guarantees every output remains a valid class ID.
D) Any interpolation followed by rounding, because numeric distances between class IDs encode class similarity.


Learner answer: a (normalized A). Correct answer: A. Result: correct.
Explanation: Nearest-neighbor selects source labels rather than interpolating their numerical IDs. Averaging arbitrary categorical IDs can invent labels or change their meaning, even if results are rounded.
Phase04 running initial score: 2/2. Lesson01 attempt1: 2/2; incomplete.

### Answer history: p04-l01-code-v1

ID: p04-l01-code-v1
Phase04 — Computer Vision; Lesson01 — Image Fundamentals.
Question3/84; lesson question3/3; code tracing.

What are batch.shape and the standardized RGB values at its first pixel? The supplied mean/std are simplified exercise values.

```python
import numpy as np
img = np.zeros((2, 4, 3), dtype=np.uint8)
img[0, 0] = [255, 0, 0]
x = img.astype(np.float32) / 255.0
x = (x - np.array([0.5, 0.5, 0.5])) / 0.5
batch = x.transpose(2, 0, 1)[None, ...]
print(batch.shape, batch[0, :, 0, 0].tolist())
```

A) (1,2,4,3), [1.0,-1.0,-1.0]
B) (1,3,2,4), [255.0,0.0,0.0]
C) (1,3,2,4), [1.0,0.0,0.0]
D) (1,3,2,4), [1.0,-1.0,-1.0]


Learner answer: d (normalized D). Correct answer: D. Result: correct.
Explanation: The RGB pixel becomes[1,0,0] after division by255 and[1,-1,-1] after standardization. Transposing HWC to CHW and adding a batch axis yields(1,3,2,4).
Phase04 running initial score: 3/3. Lesson01 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l02-concept-v1

ID: p04-l02-concept-v1
Phase04 — Computer Vision; Lesson02 — Convolutions from Scratch.
Question4/84; lesson question1/3; conceptual.

For a stride1 convolution away from image boundaries, what does translation equivariance mean?

A) Shifting the input leaves the output feature map unchanged at every location.
B) Shifting the input shifts the output feature map correspondingly, because the same kernel is applied at each location.
C) Each spatial location learns an independent kernel to recognize translated patterns.
D) Convolution removes all information about where a pattern occurs in the image.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Reusing one kernel at all locations makes a spatial shift of the input produce the corresponding output shift for stride1 away from boundary effects. Equivariance differs from invariance, which would leave the output unchanged.
Phase04 running initial score: 4/4. Lesson02 attempt1: 1/1; incomplete.

### Answer history: p04-l02-application-v1

ID: p04-l02-application-v1
Phase04 — Computer Vision; Lesson02 — Convolutions from Scratch.
Question5/84; lesson question2/3; application.

A standard convolution takes a (3,32,32) input and has8 output channels, a3x3 kernel, stride2, padding1, dilation1, and one bias per output channel. What are its output shape and trainable parameter count?

A) (8,16,16), 224 parameters.
B) (8,16,16), 216 parameters.
C) (8,17,17), 224 parameters.
D) (3,16,16), 80 parameters.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Each spatial output size is floor((32+2-3)/2)+1=16. Weights total8*3*3*3=216, plus8 biases gives224 parameters.
Phase04 running initial score: 5/5. Lesson02 attempt1: 2/2; incomplete.

### Answer history: p04-l02-code-v1

ID: p04-l02-code-v1
Phase04 — Computer Vision; Lesson02 — Convolutions from Scratch.
Question6/84; lesson question3/3; code tracing.

What does this valid stride1 operation print? As in the lesson's implementation, the kernel is applied without flipping.

```python
import numpy as np
x = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])
kernel = np.array([[1, 0],
                   [0, -1]])
out = np.array([[np.sum(x[i:i+2, j:j+2] * kernel)
                 for j in range(2)] for i in range(2)])
print(out.tolist())
```

A) [[4, 4], [4, 4]]
B) [[-4, -5], [-7, -8]]
C) [[-4, -4], [-4, -4]]
D) [[6, 8], [12, 14]]


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Each window contributes its top-left value minus its bottom-right value:1-5,2-6,4-8,5-9. Every result is-4; no kernel flip occurs.
Phase04 running initial score: 6/6. Lesson02 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l03-concept-v1

ID: p04-l03-concept-v1
Phase04 — Computer Vision; Lesson03 — CNNs — LeNet to ResNet.
Question7/84; lesson question1/3; conceptual.

For a residual mapping y=x+F(x) with matching shapes, how does the identity shortcut help optimization?

A) It removes all trainable parameters from F and makes backpropagation unnecessary.
B) It guarantees that training and test error cannot increase when another block is added.
C) It forces F to learn the full desired mapping instead of a correction to x.
D) It provides a direct gradient path and lets the block represent identity by setting F(x)=0.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: The identity branch supplies a direct gradient contribution and permits identity when the residual branch is zero. These properties aid optimization but do not guarantee lower training or test error for every added block.
Phase04 running initial score: 7/7. Lesson03 attempt1: 1/1; incomplete.

### Answer history: p04-l03-application-v1

ID: p04-l03-application-v1
Phase04 — Computer Vision; Lesson03 — CNNs — LeNet to ResNet.
Question8/84; lesson question2/3; application.

A ResNet BasicBlock changes an input from(N,32,32,32) to a residual-branch output of(N,64,16,16). Which shortcut makes the elementwise addition valid using the lesson's design?

A) Identity, because residual addition automatically broadcasts both channels and spatial dimensions.
B) A1x1 convolution from32 to64 channels with stride2, followed by BatchNorm.
C) A1x1 convolution from32 to64 channels with stride1 and no spatial downsampling.
D) A2x2 pooling operation with stride2 alone, preserving32 channels.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: A1x1 stride2 projection maps32 input channels to64 and downsamples32x32 to16x16. BatchNorm preserves that shape, allowing addition with the residual branch.
Phase04 running initial score: 8/8. Lesson03 attempt1: 2/2; incomplete.

### Answer history: p04-l03-code-v1

ID: p04-l03-code-v1
Phase04 — Computer Vision; Lesson03 — CNNs — LeNet to ResNet.
Question9/84; lesson question3/3; code tracing.

For a backbone output shaped(4,128,8,8), what output shape and trainable parameter count does this classifier head have?

```python
head = nn.Sequential(
    nn.AdaptiveAvgPool2d(1),
    nn.Flatten(),
    nn.Linear(128, 10),  # bias=True
)
```

A) Output(4,10);1290 parameters.
B) Output(4,10);81930 parameters.
C) Output(4,128);1290 parameters.
D) Output(4,10,8,8);1280 parameters.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Adaptive average pooling reduces each8x8 map to1x1, yielding(4,128,1,1). Flatten produces(4,128), and the linear layer outputs(4,10) with128*10+10=1290 parameters. Pooling and flattening have no trainable parameters.
Phase04 running initial score: 9/9. Lesson03 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l04-concept-v1

ID: p04-l04-concept-v1
Phase04 — Computer Vision; Lesson04 — Image Classification.
Question10/84; lesson question1/3; conceptual.

Why must an ordinary classification augmentation preserve the label, unless the target is explicitly adjusted as in mixup?

A) Every augmentation must leave all pixel values unchanged to avoid distribution shift.
B) The model assumes all transformed images belong to a new class independent of the original label.
C) Keeping the original label after a transform that changes the true class creates incorrect training supervision.
D) Label preservation guarantees the model will generalize perfectly to all transformed inputs.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Ordinary augmentation asserts that the transformed example retains its class. A transform that changes the true class without changing the target supplies incorrect supervision; label-aware methods such as mixup explicitly modify targets.
Phase04 running initial score: 10/10. Lesson04 attempt1: 1/1; incomplete.

### Answer history: p04-l04-application-v1

ID: p04-l04-application-v1
Phase04 — Computer Vision; Lesson04 — Image Classification.
Question11/84; lesson question2/3; application.

Your image classifier has high overall accuracy, but you suspect it misses most examples of a rare class. Which diagnostic most directly tests that concern?

A) Check only the training loss averaged over all images.
B) Inspect the rare class's recall and its row in a confusion matrix whose rows are true labels.
C) Increase top-k until every class is included and report that accuracy alone.
D) Measure the mean of the maximum predicted probability across all images.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: Rare-class recall measures the share of actual examples of that class correctly retrieved. Its confusion-matrix row shows correct predictions on the diagonal and the classes receiving its false negatives.
Phase04 running initial score: 11/11. Lesson04 attempt1: 2/2; incomplete.

### Answer history: p04-l04-code-v1

ID: p04-l04-code-v1
Phase04 — Computer Vision; Lesson04 — Image Classification.
Question12/84; lesson question3/3; code tracing.

What mixed target and soft cross-entropy does this single-example mixup calculation print? Logarithms are natural.

```python
import math
lam = 0.75
label_a = [1.0, 0.0]
label_b = [0.0, 1.0]
target = [lam*a + (1-lam)*b for a, b in zip(label_a, label_b)]
probs = [0.8, 0.2]
loss = -sum(t * math.log(p) for t, p in zip(target, probs))
print(target, round(loss, 3))
```

A) [1.0,0.0], 0.223
B) [0.75,0.25], 0.223
C) [0.25,0.75], 1.263
D) [0.75,0.25], 0.570


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Mixup yields target[0.75,0.25]. Soft cross-entropy is-0.75*ln(0.8)-0.25*ln(0.2)=0.569717..., rounded0.570; both target components contribute.
Phase04 running initial score: 12/12. Lesson04 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l05-concept-v1

ID: p04-l05-concept-v1
Phase04 — Computer Vision; Lesson05 — Transfer Learning & Fine-Tuning.
Question13/84; lesson question1/3; conceptual.

Which statement correctly distinguishes a linear probe from backbone fine-tuning?

A) A linear probe trains the whole backbone with a linear loss; fine-tuning freezes all parameters.
B) A linear probe keeps the pretrained backbone fixed and trains a linear head; fine-tuning updates some or all backbone parameters.
C) A linear probe uses the pretrained classifier unchanged and requires no target-task labels.
D) Fine-tuning always reinitializes the backbone randomly before training a new head.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: A linear probe fits a new linear classifier on a fixed pretrained representation. Backbone fine-tuning allows some or all pretrained feature parameters to adapt to the target task.
Phase04 running initial score: 13/13. Lesson05 attempt1: 1/1; incomplete.

### Answer history: p04-l05-application-v1

ID: p04-l05-application-v1
Phase04 — Computer Vision; Lesson05 — Transfer Learning & Fine-Tuning.
Question14/84; lesson question2/3; application.

On a tiny target dataset, you freeze backbone parameters with requires_grad=False but call model.train() each epoch. Its BatchNorm running statistics still change; how do you keep those statistics fixed while training the new head?

A) Set the backbone learning rate to zero; that alone prevents running-statistic updates.
B) Wrap the backbone forward pass in no_grad; that alone switches BatchNorm to evaluation mode.
C) Call model.train(), then put the backbone's BatchNorm modules in eval mode each epoch.
D) Clear the optimizer gradients twice per batch to reset BatchNorm's running statistics.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: BatchNorm running statistics are buffers updated by training-mode forward passes, independently of parameter requires_grad and optimizer learning rate. Setting those modules to eval after model.train preserves stored statistics while leaving the head trainable.
Phase04 running initial score: 14/14. Lesson05 attempt1: 2/2; incomplete.

### Answer history: p04-l05-code-v1

ID: p04-l05-code-v1
Phase04 — Computer Vision; Lesson05 — Transfer Learning & Fine-Tuning.
Question15/84; lesson question3/3; code tracing.

Assume model.fc originally maps512 features to1000 classes. After this code, which parameters are trainable, and how many trainable scalars are there?

```python
for p in model.parameters():
    p.requires_grad = False
model.fc = nn.Linear(512, 5)  # new layer, bias=True
trainable = sum(p.numel() for p in model.parameters()
                if p.requires_grad)
```

A) No parameters; the initial loop also freezes all subsequently created layers.
B) Every backbone parameter and the new head; replacing fc unfreezes the whole model.
C) Only the new head;2560 trainable scalars.
D) Only the new head;2565 trainable scalars.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: The freezing loop affects only parameters that exist then. The replacement Linear has trainable weights and biases by default, totaling512*5+5=2565. The backbone remains frozen.
Phase04 running initial score: 15/15. Lesson05 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l06-concept-v1

ID: p04-l06-concept-v1
Phase04 — Computer Vision; Lesson06 — Object Detection — YOLO from Scratch.
Question16/84; lesson question1/3; conceptual.

In the lesson's anchor-based detection head, what is the purpose of objectness, distinct from the class scores?

A) Predict whether a candidate corresponds to an object, including learning to reject empty/background candidates.
B) Predict the object's width and height in pixels without using the box-regression outputs.
C) Select the image's single class label and discard all spatial information.
D) Guarantee that overlapping candidates already contain exactly one prediction per object.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Objectness distinguishes candidate objects from background. Class scores identify their category, box outputs describe geometry, and postprocessing such as NMS addresses duplicate predictions.
Phase04 running initial score: 16/16. Lesson06 attempt1: 1/1; incomplete.

### Answer history: p04-l06-application-v1

ID: p04-l06-application-v1
Phase04 — Computer Vision; Lesson06 — Object Detection — YOLO from Scratch.
Question17/84; lesson question2/3; application.

A detector performs well at AP@IoU0.5 but drops sharply when evaluated at stricter IoU thresholds. Which issue is most directly suggested, and what should you inspect next?

A) Its class vocabulary is too large; remove all rare categories before examining boxes.
B) Its predictions must be perfectly calibrated; stop checking localization quality.
C) Its boxes locate objects roughly but not tightly; inspect box-regression errors and localization training.
D) Its confidence threshold is too high; lowering it alone guarantees tighter box alignment.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Stricter IoU thresholds demand tighter overlap with ground-truth boxes. A strong lenient-IoU score but poor strict-IoU scores suggests localization quality should be inspected; confidence changes alone do not repair coordinates.
Phase04 running initial score: 17/17. Lesson06 attempt1: 2/2; incomplete.

### Answer history: p04-l06-code-v1

ID: p04-l06-code-v1
Phase04 — Computer Vision; Lesson06 — Object Detection — YOLO from Scratch.
Question18/84; lesson question3/3; code tracing.

All boxes have the same predicted class. Greedy NMS selects the highest score and removes remaining boxes with IoU>0.5 to it. Which indices are kept, in order? Coordinates use area=(x2-x1)*(y2-y1).

```python
boxes = [[0, 0, 2, 2],
         [0, 0, 2, 1.5],
         [3, 3, 5, 5]]
scores = [0.9, 0.8, 0.7]
keep = nms(boxes, scores, iou_threshold=0.5)
```

A) [0,1,2]
B) [1,2]
C) [0]
D) [0,2]


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Box0 has the highest score. Its intersection with box1 is3 and their union is4, giving IoU0.75, so box1 is suppressed. Box2 does not overlap and is kept next.
Phase04 running initial score: 18/18. Lesson06 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l07-concept-v1

ID: p04-l07-concept-v1
Phase04 — Computer Vision; Lesson07 — Semantic Segmentation — U-Net.
Question19/84; lesson question1/3; conceptual.

What is the main role of U-Net's encoder-to-decoder skip connections?

A) Replace all decoder computations with the original RGB pixels.
B) Supply matching-resolution encoder features so the decoder can combine spatial detail with deeper context.
C) Force every pixel of the same class to receive a unique object-instance ID.
D) Convert the dense prediction problem into one label for the entire image.


Learner answer: B. Correct answer: B. Result: correct.
Explanation: U-Net concatenates matching-resolution encoder features with upsampled decoder features, supplying spatial detail that complements deep contextual representations.
Phase04 running initial score: 19/19. Lesson07 attempt1: 1/1; incomplete.

### Answer history: p04-l07-application-v1

ID: p04-l07-application-v1
Phase04 — Computer Vision; Lesson07 — Semantic Segmentation — U-Net.
Question20/84; lesson question2/3; application.

A segmentation dataset has1% foreground pixels. A model predicts background everywhere and reports99% pixel accuracy; what evaluation and training change best addresses the hidden failure?

A) Report only pixel accuracy and remove the foreground class because it contributes few pixels.
B) Increase the background loss weight and inspect only background accuracy.
C) Replace per-class metrics with the average confidence across all pixels.
D) Inspect foreground IoU/Dice and consider combining cross-entropy with a foreground-sensitive overlap loss.


Learner answer: D. Correct answer: D. Result: correct.
Explanation: Aggregate pixel accuracy hides the complete absence of foreground predictions. Foreground IoU/Dice reveals that failure; overlap-aware losses can complement cross-entropy by emphasizing mask overlap. They do not guarantee removal of every imbalance issue.
Phase04 running initial score: 20/20. Lesson07 attempt1: 2/2; incomplete.

### Answer history: p04-l07-code-v1

ID: p04-l07-code-v1
Phase04 — Computer Vision; Lesson07 — Semantic Segmentation — U-Net.
Question21/84; lesson question3/3; code tracing.

What foreground IoU and Dice does this code print? The sets contain foreground pixel indices; smoothing is omitted because the denominators are nonzero.

```python
pred = {0, 1, 2, 3}
true = {2, 3, 4}
intersection = len(pred & true)
union = len(pred | true)
iou = intersection / union
dice = 2 * intersection / (len(pred) + len(true))
print(round(iou, 3), round(dice, 3))
```

A) 0.4 0.571
B) 0.5 0.667
C) 0.286 0.571
D) 0.4 0.8


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Intersection contains2 pixels, union5, and predicted plus true sizes sum to7. IoU=2/5=0.4 and Dice=4/7≈0.571.
Phase04 running initial score: 21/21. Lesson07 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l08-concept-v1

ID: p04-l08-concept-v1
Phase04 — Computer Vision; Lesson08 — Instance Segmentation — Mask R-CNN.
Question22/84; lesson question1/3; conceptual.

Why does Mask R-CNN use RoIAlign rather than rounding proposal coordinates as in RoIPool?

A) RoIAlign removes the need for a backbone by predicting masks directly from box coordinates.
B) RoIAlign rounds more aggressively, ensuring every proposal aligns with the nearest whole feature pixel.
C) RoIAlign preserves fractional sampling locations with bilinear interpolation, reducing spatial misalignment important for masks.
D) RoIAlign forces every proposal to have the same original image width and height.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: RoIAlign samples at fractional coordinates using bilinear interpolation instead of quantizing proposal and bin boundaries, improving spatial alignment of extracted features with masks.
Phase04 running initial score: 22/22. Lesson08 attempt1: 1/1; incomplete.

### Answer history: p04-l08-application-v1

ID: p04-l08-application-v1
Phase04 — Computer Vision; Lesson08 — Instance Segmentation — Mask R-CNN.
Question23/84; lesson question2/3; application.

Your dataset has four foreground object classes. In the lesson's torchvision Mask R-CNN fine-tuning recipe, how should you configure the replacement predictors?

A) Replace only the box predictor with4 classes; the pretrained mask predictor automatically adapts.
B) Replace both box and mask predictors with5 classes, reserving class0 for background.
C) Replace both predictors with4 classes and label the four foreground categories0 through3.
D) Keep both pretrained predictors unchanged and use the RPN objectness score as the new class label.


Learner answer: A. Correct answer: B. Result: incorrect.
Explanation: The recipe replaces both the box predictor and class-specific mask predictor for the new label vocabulary. Four foreground classes require num_classes=5 because index0 is reserved for background; changing the box predictor alone does not adapt mask channels automatically.
Review: Lesson08 — replace both class-dependent predictors and include background in num_classes.
Phase04 running initial score: 22/23. Lesson08 attempt1: 1/2; incomplete.

### Answer history: p04-l08-code-v1

ID: p04-l08-code-v1
Phase04 — Computer Vision; Lesson08 — Instance Segmentation — Mask R-CNN.
Question24/84; lesson question3/3; code tracing.

For one image, the model returns three instance masks with shape(3,1,200,300). What shape and meaning does binary_masks have after this code?

```python
keep = predictions["scores"] >= 0.8  # [True, False, True]
binary_masks = (predictions["masks"][keep] > 0.5).squeeze(1)
```

A) (2,1,200,300), retaining the singleton mask-channel axis.
B) (1,200,300), merging the surviving instances into one class mask.
C) (2,200,300), one full-resolution boolean mask per retained instance.
D) (2,28,28), one low-resolution raw mask-head output per retained instance.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Filtering keeps two masks with shape(2,1,200,300). Thresholding yields booleans, and squeeze(1) removes only the singleton channel, yielding(2,200,300) while preserving separate instances.
Phase04 running initial score: 23/24. Lesson08 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes. Mask R-CNN predictor replacement remains in the review queue.

### Answer history: p04-l09-concept-v1

ID: p04-l09-concept-v1
Phase04 — Computer Vision; Lesson09 — Image Generation — GANs.
Question25/84; lesson question1/3; conceptual.

For the lesson's non-saturating GAN objective, which description correctly states the generator's goal?

A) Minimize -log(D(G(z))), encouraging generated images to receive high realness scores.
B) Minimize -log(1-D(G(z))), encouraging generated images to receive low realness scores.
C) Minimize the discriminator's classification accuracy by replacing all real images with noise.
D) Match each random noise vector to a fixed real image using a required one-to-one target pairing.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: Minimizing the non-saturating generator loss -log(D(G(z))) encourages high discriminator realness scores for generated samples. The discriminator itself learns to distinguish real from generated data.
Phase04 running initial score: 24/25. Lesson09 attempt1: 1/1; incomplete.

### Answer history: p04-l09-application-v1

ID: p04-l09-application-v1
Phase04 — Computer Vision; Lesson09 — Image Generation — GANs.
Question26/84; lesson question2/3; application.

Your GAN produces visually convincing images, but many different noise vectors yield nearly identical samples and entire types of training images are missing. What failure does this suggest, and what should evaluation examine?

A) Successful convergence; realistic individual samples prove the full data distribution is covered.
B) Excessive image resolution; reducing resolution necessarily restores all missing image types.
C) Mode collapse; inspect sample diversity and distribution coverage alongside visual quality.
D) Perfect discriminator calibration; confidence alone measures generated-sample diversity.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: Mode collapse means the generator covers only a narrow subset of the data distribution. Realistic individual samples do not establish diversity or coverage, so evaluate those separately.
Phase04 running initial score: 25/26. Lesson09 attempt1: 2/2; incomplete.

### Answer history: p04-l09-code-v1

ID: p04-l09-code-v1
Phase04 — Computer Vision; Lesson09 — Image Generation — GANs.
Question27/84; lesson question3/3; code tracing.

Assume G and D are separate networks and G's parameter gradients start as None. After this discriminator backward pass, which statement is correct?

```python
fake = G(z)
fake_logits = D(fake.detach())
loss_d = F.binary_cross_entropy_with_logits(
    fake_logits, torch.zeros_like(fake_logits)
)
loss_d.backward()
```

A) Gradients reach both G and D because fake was originally produced by G.
B) Gradients reach G but not D because detach freezes the discriminator.
C) No gradients reach either network because detach disables all autograd globally.
D) Gradients reach D, while detach blocks this loss's gradient path into G.


Learner answer: B. Correct answer: D. Result: incorrect.
Explanation: fake.detach() disconnects the fake tensor from the generator's computation graph. D still builds its own graph and receives this loss's gradients; the generator receives none from this backward pass. Detach does not freeze D or disable autograd globally.
Review: Lesson09 — detach blocks gradients into the producer G while allowing D to train on the detached fake input.
Phase04 running initial score: 25/27. Lesson09 attempt1 complete: 2/3, meeting the lesson minimum. Lessons remain todo until the full phase passes.

### Answer history: p04-l10-concept-v1

ID: p04-l10-concept-v1
Phase04 — Computer Vision; Lesson10 — Image Generation — Diffusion Models.
Question28/84; lesson question1/3; conceptual.

In the lesson's epsilon-prediction diffusion training, what does the network learn from a noisy image x_t and its timestep t?

A) A binary real-versus-fake label provided by an adversarial discriminator.
B) The fixed beta schedule, with no trainable image-denoising function.
C) The sampled Gaussian noise used to construct x_t, typically using an MSE objective.
D) A unique original training image assigned to each possible random-noise tensor.


Learner answer: C. Correct answer: C. Result: correct.
Explanation: In epsilon prediction, the training target is the sampled Gaussian noise in x_t=sqrt(alpha_bar_t)*x0+sqrt(1-alpha_bar_t)*epsilon. The network receives x_t and t and minimizes noise-prediction MSE.
Phase04 running initial score: 26/28. Lesson10 attempt1: 1/1; incomplete.

### Answer history: p04-l10-application-v1

ID: p04-l10-application-v1
Phase04 — Computer Vision; Lesson10 — Image Generation — Diffusion Models.
Question29/84; lesson question2/3; application.

During training, you sample a random timestep t for each clean image. How can you obtain x_t efficiently without simulating every earlier noising step?

A) Use the cumulative product alpha_bar_t and sample x_t=sqrt(alpha_bar_t)*x0+sqrt(1-alpha_bar_t)*epsilon.
B) Use x_t=x0+t*epsilon, because Gaussian noise variance always grows as t squared under the given schedule.
C) Run the learned reverse sampler from x0 for t steps and treat the result as forward-process data.
D) Replace every x_t with pure noise, because no signal remains at any positive timestep.


Learner answer: A. Correct answer: A. Result: correct.
Explanation: The Gaussian forward process has the closed-form marginal q(x_t|x0) with mean sqrt(alpha_bar_t)*x0 and covariance(1-alpha_bar_t)*I. This allows direct sampling at a chosen timestep.
Phase04 running initial score: 27/29. Lesson10 attempt1: 2/2; incomplete.

### Answer history: p04-l10-code-v1

ID: p04-l10-code-v1
Phase04 — Computer Vision; Lesson10 — Image Generation — Diffusion Models.
Question30/84; lesson question3/3; code tracing.

For this scalar example, what noisy value x_t and reconstructed clean estimate x0_est does the code print? The noise predictor is exact in this exercise.

```python
import math
alpha_bar = 0.36
x0, noise = 2.0, -1.0
xt = math.sqrt(alpha_bar)*x0 + math.sqrt(1-alpha_bar)*noise
pred_noise = -1.0
x0_est = (xt - math.sqrt(1-alpha_bar)*pred_noise) / math.sqrt(alpha_bar)
print(round(xt, 2), round(x0_est, 2))
```

A) -0.08 2.0
B) 0.4 0.4
C) 0.4 2.0
D) 1.4 2.0


Learner answer: C. Correct answer: C. Result: correct.
Explanation: sqrt(0.36)=0.6 and sqrt(0.64)=0.8, giving xt=0.6*2-0.8=0.4. Subtracting the exact noise contribution and dividing by0.6 reconstructs2.0.
Phase04 running initial score: 28/30. Lesson10 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l11-concept-v1

ID: p04-l11-concept-v1
Phase04 — Computer Vision; Lesson11 — Stable Diffusion — Architecture & Fine-Tuning.
Question31/84; lesson question1/3; conceptual.

In the lesson's Stable Diffusion pipeline, which description correctly assigns the main components' roles?

A) The text encoder decodes pixels, the VAE chooses timesteps, and the U-Net classifies prompts.
B) The VAE compresses and reconstructs images, the text encoder supplies conditioning embeddings, and the denoiser operates on noisy latents.
C) The VAE predicts every noise step directly in RGB, while the text encoder stores the optimizer state.
D) The scheduler learns all image features during inference, while the denoiser remains unused.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: The VAE maps between images and compressed latents; the text encoder supplies prompt embeddings; the conditioned denoiser predicts noise in latent space, with the scheduler controlling sampling updates.
Phase04 running initial score: 29/31. Lesson11 attempt1: 1/1; incomplete.

### Answer history: p04-l11-application-v1

ID: p04-l11-application-v1
Phase04 — Computer Vision; Lesson11 — Stable Diffusion — Architecture & Fine-Tuning.
Question32/84; lesson question2/3; application.

You want to adapt a pretrained Stable Diffusion model to a subject using limited GPU memory and distribute a small LoRA adapter. Which training setup fits this goal?

A) Train every base-model weight and save the complete updated pipeline.
B) Freeze all parameters and change only the inference random seed.
C) Train only the VAE decoder and save its full replacement weights.
D) Freeze base weights and train low-rank updates in selected attention projections.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: LoRA keeps the pretrained base weights frozen and learns low-rank weight updates in selected layers, commonly attention projections. Saving these updates produces a small adapter rather than a complete replacement model.
Phase04 running initial score: 30/32. Lesson11 attempt1: 2/2; incomplete.

### Answer history: p04-l11-code-v1

ID: p04-l11-code-v1
Phase04 — Computer Vision; Lesson11 — Stable Diffusion — Architecture & Fine-Tuning.
Question33/84; lesson question3/3; code tracing.

This code combines unconditional and text-conditioned noise predictions using classifier-free guidance. What does it print?

```python
eps_uncond = [1.0, 2.0]
eps_cond = [3.0, 1.0]
guidance_scale = 2.0
eps = [u + guidance_scale * (c - u)
       for u, c in zip(eps_uncond, eps_cond)]
print(eps)
```

A) [4.0, 3.0]
B) [5.0, 0.0]
C) [6.0, 2.0]
D) [2.0, 1.5]

Learner answer: B. Correct answer: B. Result: correct.
Explanation: Guidance computes u+2*(c-u) for each component: 1+2*(3-1)=5 and 2+2*(1-2)=0. The output is [5.0, 0.0].
Phase04 running initial score: 31/33. Lesson11 attempt1 complete: 3/3. Lessons remain todo until the full phase passes.

### Answer history: p04-l12-concept-v1

ID: p04-l12-concept-v1
Phase04 — Computer Vision; Lesson12 — Video Understanding — Temporal Modeling.
Question34/84; lesson question1/3; conceptual.

A video classifier independently encodes each frame with the same 2D CNN, averages those embeddings, then classifies the result. Why must it give the same prediction for a clip and its exact time reversal, assuming deterministic inference?

A) The CNN automatically sorts frames into their original chronological order.
B) Averaging forces all frame embeddings to become identical before classification.
C) Temporal averaging is unchanged by frame permutation, so it discards their order.
D) A 2D CNN cannot extract any spatial features from individual video frames.

Learner answer: D. Correct answer: C. Result: incorrect.
Explanation: A 2D CNN extracts spatial appearance features from each frame. Averaging the independently computed embeddings is invariant to frame order, so reversing the same frames preserves the pooled representation. The missing information is temporal order, not spatial features.
Phase04 running initial score: 31/34. Lesson12 attempt1: 0/1; incomplete. Temporal pooling order invariance added to the review queue.

### Answer history: p04-l12-application-v1

ID: p04-l12-application-v1
Phase04 — Computer Vision; Lesson12 — Video Understanding — Temporal Modeling.
Question35/84; lesson question2/3; application.

Your labels distinguish an object moving left-to-right from the same object moving right-to-left. Which setup is best suited to learning this motion direction?

A) Sample consecutive frames in order and use a 3D convolutional model over time and space.
B) Average independent frame embeddings and use a larger final linear classifier.
C) Shuffle every clip's frames randomly and train a temporal model on the shuffled order.
D) Repeat one selected frame across all time positions and train a 3D convolutional model.

Learner answer: C. Correct answer: A. Result: incorrect.
Explanation: Consecutive frames in chronological order preserve the motion signal for a 3D convolution over time and space. Randomly shuffling each clip destroys the consistent temporal direction needed to distinguish left-to-right from right-to-left motion.
Phase04 running initial score: 31/35. Lesson12 attempt1: 0/2; incomplete. A fresh full lesson retake will be required because the initial set can no longer reach the 2/3 lesson minimum.

### Answer history: p04-l12-code-v1

ID: p04-l12-code-v1
Phase04 — Computer Vision; Lesson12 — Video Understanding — Temporal Modeling.
Question36/84; lesson question3/3; code tracing.

To inflate a 2D convolution into a 3D convolution with a temporal kernel of length 3, the lesson copies its weights along time and divides them by 3. Ignoring boundaries and bias, what is the result when all three input frames are identical?

```python
# Each original 2D convolution would produce 6.0 at this location.
frame_responses = [6.0, 6.0, 6.0]
response_3d = sum(r / 3 for r in frame_responses)
print(response_3d)
```

A) 18.0, because the temporal kernel sums three unscaled copies.
B) 2.0, because only one of the three frames contributes.
C) 0.0, because identical frames cancel along the time axis.
D) 6.0, because division by the temporal length preserves the response.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Each copied temporal slice contributes 6/3=2, so the sum is6. Dividing inflated weights by temporal kernel length preserves the response for identical frames away from boundaries.
Phase04 running initial score: 32/36. Lesson12 attempt1 complete: 1/3, below the 2/3 minimum. Fresh full three-question retake required after initial phase coverage; lessons remain todo until phase pass.

### Answer history: p04-l13-concept-v1

ID: p04-l13-concept-v1
Phase04 — Computer Vision; Lesson13 — 3D Vision — Point Clouds & NeRFs.
Question37/84; lesson question1/3; conceptual.

A point cloud is an unordered set. How does PointNet produce a global feature that is unchanged when the input points are reordered?

A) Flatten all point coordinates and apply a separate learned weight to each point index.
B) Apply the same MLP to each point, then take a coordinate-wise maximum over the point features.
C) Assign each point a sequence-position embedding, then concatenate features in input order.
D) Connect consecutive input points with temporal convolutions, then keep the last output.

Learner answer: C. Correct answer: B. Result: incorrect.
Explanation: PointNet applies identical shared weights to every point and aggregates with a symmetric coordinate-wise max. Reordering points leaves that maximum unchanged. Sequence-position embeddings and ordered concatenation instead introduce dependence on input order.
Phase04 running initial score: 32/37. Lesson13 attempt1: 0/1; incomplete. PointNet permutation invariance added to the review queue.

### Answer history: p04-l13-application-v1

ID: p04-l13-application-v1
Phase04 — Computer Vision; Lesson13 — 3D Vision — Point Clouds & NeRFs.
Question38/84; lesson question2/3; application.

You have photographs of a static scene with known camera poses and want to train a NeRF for novel-view synthesis. Which training procedure matches the lesson?

A) Predict one class per photograph and optimize classification accuracy across camera poses.
B) Sort all image pixels by brightness and treat that sequence as a complete 3D point cloud.
C) Query only the camera's position and compare the network output with the entire image.
D) Sample camera rays, query density and colour along each ray, composite pixels, and minimize error against the photographs.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: NeRF training renders pixels by querying density and colour at samples along posed camera rays and compositing with transmittance-weighted opacity. Pixel reconstruction error backpropagates through this rendering process into the network.
Phase04 running initial score: 33/38. Lesson13 attempt1: 1/2; incomplete.

### Answer history: p04-l13-code-v1

ID: p04-l13-code-v1
Phase04 — Computer Vision; Lesson13 — 3D Vision — Point Clouds & NeRFs.
Question39/84; lesson question3/3; code tracing.

Two samples lie along a camera ray, ordered front to back. Each has opacity 0.5. With a black background, what RGB colour does this transmittance-weighted compositing code print?

```python
alpha = [0.5, 0.5]
colours = [(1.0, 0.0, 0.0), (0.0, 0.0, 1.0)]
transmittance = 1.0
pixel = [0.0, 0.0, 0.0]
for a, colour in zip(alpha, colours):
    weight = transmittance * a
    pixel = [p + weight * c for p, c in zip(pixel, colour)]
    transmittance *= 1.0 - a
print(pixel)
```

A) [0.5, 0.0, 0.25]
B) [0.5, 0.0, 0.5]
C) [0.25, 0.0, 0.5]
D) [1.0, 0.0, 1.0]

Learner answer: A. Correct answer: A. Result: correct.
Explanation: The front sample has weight1*0.5=0.5. Remaining transmittance is0.5, so the back sample has weight0.5*0.5=0.25. Black background contributes zero, giving [0.5, 0.0, 0.25].
Phase04 running initial score: 34/39. Lesson13 attempt1 complete: 2/3, meeting the lesson minimum. PointNet permutation invariance remains in the review queue; Lesson12 still requires a fresh full retake. Lessons remain todo until phase pass.

### Answer history: p04-l14-concept-v1

ID: p04-l14-concept-v1
Phase04 — Computer Vision; Lesson14 — Vision Transformers (ViT).
Question40/84; lesson question1/3; conceptual.

In the lesson's ViT, what are the distinct roles of positional embeddings and the [CLS] token?

A) Positional embeddings specify class labels; the [CLS] token stores the original pixel grid.
B) Positional embeddings replace self-attention; the [CLS] token sets each patch's spatial coordinates.
C) Positional embeddings supply patch-location information; the final [CLS] representation feeds the image classifier.
D) Positional embeddings remove patch boundaries; the [CLS] token independently classifies every pixel.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Positional embeddings add information about where patches occur. The learned [CLS] token interacts with patches through the encoder, and its final representation is read by the image classification head.
Phase04 running initial score: 35/40. Lesson14 attempt1: 1/1; incomplete.

### Answer history: p04-l14-application-v1

ID: p04-l14-application-v1
Phase04 — Computer Vision; Lesson14 — Vision Transformers (ViT).
Question41/84; lesson question2/3; application.

For a fixed 224x224 image, you reduce a ViT's square patch size from16 to8. Ignoring the [CLS] token, how do patch-token count and the number of entries in each full self-attention score matrix change?

A) Tokens double; attention-score entries quadruple.
B) Tokens quadruple; attention-score entries increase sixteenfold.
C) Tokens quadruple; attention-score entries also quadruple.
D) Tokens halve; attention-score entries fall to one quarter.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: The patch grid grows from14x14=196 tokens to28x28=784 tokens, a factor of4. Each full attention score matrix has n*n entries, so its entry count grows by4 squared=16. This refers to attention-score entries, not total model FLOPs.
Phase04 running initial score: 36/41. Lesson14 attempt1: 2/2; incomplete.

### Answer history: p04-l14-code-v1

ID: p04-l14-code-v1
Phase04 — Computer Vision; Lesson14 — Vision Transformers (ViT).
Question42/84; lesson question3/3; code tracing.

What is the shape of tokens after this patch embedding and [CLS] concatenation? The convolution uses no padding.

```python
import torch
from torch import nn
x = torch.zeros(2, 3, 64, 64)
proj = nn.Conv2d(3, 192, kernel_size=16, stride=16)
patches = proj(x).flatten(2).transpose(1, 2)
cls = torch.zeros(1, 1, 192).expand(x.size(0), -1, -1)
tokens = torch.cat([cls, patches], dim=1)
print(tuple(tokens.shape))
```

A) (2, 16, 192)
B) (2, 192, 17)
C) (2, 197, 192)
D) (2, 17, 192)

Learner answer: D. Correct answer: D. Result: correct.
Explanation: The convolution produces a4x4 grid of192-dimensional patch embeddings per image. Flattening and transposing gives(2,16,192); prepending one class token gives(2,17,192).
Phase04 running initial score: 37/42. Lesson14 attempt1 complete: 3/3. Lesson12 still requires a fresh full retake; lessons remain todo until phase pass.

### Answer history: p04-l15-concept-v1

ID: p04-l15-concept-v1
Phase04 — Computer Vision; Lesson15 — Real-Time Vision — Edge Deployment.
Question43/84; lesson question1/3; conceptual.

Two vision models have similar parameter counts, but different operators. What evidence should drive the choice for an edge device with a strict latency and memory budget?

A) Benchmark warmed-up models on the target device at production input sizes, measuring latency percentiles, peak memory, and accuracy.
B) Choose the model with fewer FLOPs, since FLOP count determines latency on every device.
C) Compare training throughput on a workstation and assume the same ranking on the edge device.
D) Choose the smaller weight file, since weight storage determines all peak inference memory.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Deployment decisions require measurements on the actual target at production shapes after warmup. Operator support, memory traffic and runtime optimizations affect latency; parameter counts and FLOPs alone do not determine it. Peak memory includes activations and runtime buffers as well as weights.
Phase04 running initial score: 38/43. Lesson15 attempt1: 1/1; incomplete.

### Answer history: p04-l15-application-v1

ID: p04-l15-application-v1
Phase04 — Computer Vision; Lesson15 — Real-Time Vision — Edge Deployment.
Question44/84; lesson question2/3; application.

You are applying static INT8 post-training quantisation to a compatible vision model. Why run representative calibration images through the prepared model before conversion?

A) To update all pretrained weights using gradients from the calibration labels.
B) To measure activation ranges for quantisation scales and zero points.
C) To guarantee identical predictions for every possible future input.
D) To determine camera resolution from the number of calibration images.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: Calibration observers collect activation statistics on representative inputs to choose quantisation parameters such as scales and zero points. Static PTQ calibration does not train base weights and generally does not need labels. Accuracy must still be validated after conversion.
Phase04 running initial score: 39/44. Lesson15 attempt1: 2/2; incomplete.

### Answer history: p04-l15-code-v1

ID: p04-l15-code-v1
Phase04 — Computer Vision; Lesson15 — Real-Time Vision — Edge Deployment.
Question45/84; lesson question3/3; code debugging.

The model and input are on a CUDA GPU, warmup is complete, and inference runs without gradients. What change makes this CPU wall-clock timing wait for the GPU work being measured?

```python
t0 = time.perf_counter()
y = model(x)
elapsed_ms = (time.perf_counter() - t0) * 1000
```

A) Call model.eval() after stopping the timer.
B) Increase the batch size until the timer reports a larger number.
C) Synchronize CUDA immediately before t0 and after model(x), before reading the end time.
D) Divide elapsed_ms by the number of CUDA cores.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: CUDA work is asynchronous with respect to CPU execution. Synchronizing before the start excludes outstanding work; synchronizing after the forward pass and before reading the end time waits for completion of the measured GPU work.
Phase04 running initial score: 40/45. Lesson15 attempt1 complete: 3/3. Lesson12 still requires a fresh full retake; lessons remain todo until phase pass.

### Answer history: p04-l16-concept-v1

ID: p04-l16-concept-v1
Phase04 — Computer Vision; Lesson16 — Build a Complete Vision Pipeline — Capstone.
Question46/84; lesson question1/3; conceptual.

A detector emits boxes as (cx, cy, width, height), but the crop stage expects absolute-pixel (x1, y1, x2, y2). Both are tuples of four floats. What makes this interface reliable?

A) Declare a four-float tuple type; it automatically identifies and converts coordinate conventions.
B) Rename the tuple field to box; downstream code can then infer the coordinate meaning.
C) Pass the values unchanged, because all four-number box formats use the same crop indices.
D) Specify the format and units, explicitly convert coordinates, and validate geometric bounds before cropping.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Tuple shape and numeric types do not encode coordinate semantics. A reliable boundary specifies units and convention, explicitly converts from center/size to corners, and validates or clamps geometry before cropping. The lesson's bare four-float schema alone cannot detect this mismatch.
Phase04 running initial score: 41/46. Lesson16 attempt1: 1/1; incomplete.

### Answer history: p04-l16-application-v1

ID: p04-l16-application-v1
Phase04 — Computer Vision; Lesson16 — Build a Complete Vision Pipeline — Capstone.
Question47/84; lesson question2/3; application.

A valid image decodes successfully, but the detector finds no objects. How should the pipeline handle this expected case?

A) Return a successful structured response with empty detections and classifications, and skip crop classification.
B) Return an internal-server error because every valid image must contain at least one detectable object.
C) Insert a full-image detection with confidence1.0 so the classifier always receives a crop.
D) Retry detection indefinitely until at least one object is returned.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Empty detections are a valid result for a successfully decoded image. The pipeline returns empty structured lists and skips classification rather than inventing objects, crashing, or retrying indefinitely.
Phase04 running initial score: 42/47. Lesson16 attempt1: 2/2; incomplete.

### Answer history: p04-l16-code-v1

ID: p04-l16-code-v1
Phase04 — Computer Vision; Lesson16 — Build a Complete Vision Pipeline — Capstone.
Question48/84; lesson question3/3; code tracing.

The pipeline keeps all three detections but skips classification for tiny crops. What does this code print? Each pair is (original detection index, predicted class ID).

```python
sizes = [(40, 40), (12, 50), (64, 48)]
valid_indices = []
for i, (width, height) in enumerate(sizes):
    if width < 32 or height < 32:
        continue
    valid_indices.append(i)

class_preds = [(7, 0.9), (4, 0.8)]
links = [(idx, cls_id)
         for idx, (cls_id, score) in zip(valid_indices, class_preds)]
print(links)
```

A) [(0, 7), (1, 4)]
B) [(1, 7), (2, 4)]
C) [(0, 7), (2, 4)]
D) [(7, 0), (4, 2)]

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Detection1 has width12 and is skipped; detections0 and2 pass both minimum dimensions. valid_indices=[0,2] preserves the links to original detections, producing [(0,7),(2,4)].
Phase04 running initial score: 43/48. Lesson16 attempt1 complete: 3/3. Lesson12 still requires a fresh full retake; lessons remain todo until phase pass.

### Answer history: p04-l17-concept-v1

ID: p04-l17-concept-v1
Phase04 — Computer Vision; Lesson17 — Self-Supervised Vision — SimCLR, DINO, MAE.
Question49/84; lesson question1/3; conceptual.

Which description correctly matches the three self-supervised learning methods to their training objectives?

A) SimCLR reconstructs masked pixels; DINO predicts human labels; MAE contrasts image-text pairs.
B) SimCLR matches augmented positive pairs against negatives; DINO matches an EMA teacher; MAE reconstructs masked patches.
C) SimCLR predicts point-cloud coordinates; DINO reconstructs masked pixels; MAE matches a frozen classifier's labels.
D) SimCLR needs class labels for positive pairs; DINO uses explicit negatives; MAE predicts augmentation names.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: SimCLR uses a contrastive objective on augmented views, DINO trains a student to match a moving-average teacher without explicit negatives, and MAE reconstructs masked image patches from visible ones.
Phase04 running initial score: 44/49. Lesson17 attempt1: 1/1; incomplete.

### Answer history: p04-l17-application-v1

ID: p04-l17-application-v1
Phase04 — Computer Vision; Lesson17 — Self-Supervised Vision — SimCLR, DINO, MAE.
Question50/84; lesson question2/3; application.

You want to measure how useful a self-supervised encoder's existing features are for a labelled classification task using a linear probe. Which setup follows this evaluation protocol?

A) Fine-tune the encoder and a multilayer classifier together on the labelled data.
B) Freeze a random encoder and compare only reconstruction errors on unlabelled images.
C) Continue the pretraining objective and report its training loss as classification accuracy.
D) Freeze the pretrained encoder, train only a linear classification head, and evaluate on held-out labelled data.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: A linear probe keeps the pretrained encoder fixed and learns only a linear classifier from labelled examples. Held-out evaluation measures how accessible task information is in those fixed features; updating the encoder would instead be fine-tuning.
Phase04 running initial score: 45/50. Lesson17 attempt1: 2/2; incomplete.

### Answer history: p04-l17-code-v1

ID: p04-l17-code-v1
Phase04 — Computer Vision; Lesson17 — Self-Supervised Vision — SimCLR, DINO, MAE.
Question51/84; lesson question3/3; code tracing.

In the lesson's InfoNCE implementation, z1[i] and z2[i] are two augmented views of the same image, and z is concatenated as [z1; z2]. For N=3, which targets correctly identify each row's positive partner, and why is the similarity diagonal masked?

```python
N = 3
z = torch.cat([z1, z2], dim=0)
sim = z @ z.T / tau
sim = sim.masked_fill(torch.eye(2*N, dtype=torch.bool), float('-inf'))
targets = torch.cat([torch.arange(N, 2*N), torch.arange(0, N)])
```

A) [3, 4, 5, 0, 1, 2]; masking excludes each view's comparison with itself.
B) [0, 1, 2, 3, 4, 5]; masking removes all positive partners.
C) [1, 2, 0, 4, 5, 3]; masking excludes comparisons across the two views.
D) [5, 4, 3, 2, 1, 0]; masking keeps only each view's comparison with itself.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Concatenation places each partner N positions away, giving targets [3,4,5,0,1,2]. The diagonal corresponds to the identical embedding compared with itself and is excluded; the other augmented view remains the positive target.
Phase04 running initial score: 46/51. Lesson17 attempt1 complete: 3/3. Lesson12 still requires a fresh full retake; lessons remain todo until phase pass.

### Answer history: p04-l18-concept-v1

ID: p04-l18-concept-v1
Phase04 — Computer Vision; Lesson18 — Open-Vocabulary Vision — CLIP.
Question52/84; lesson question1/3; conceptual.

What enables a pretrained CLIP model to classify images using a new set of text-described categories without training a new classification head?

A) Its image encoder contains a fixed output neuron for every possible category name.
B) Its text encoder generates new image-encoder weights whenever a category is added.
C) Its image and text encoders map inputs into an aligned space where normalized embeddings can be compared.
D) Its decoder generates a caption and must find an exact string match with a category name.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: CLIP aligns image and text embeddings through paired contrastive training. At inference, normalized image embeddings can be compared against embeddings of new class prompts without fitting a task-specific classification head.
Phase04 running initial score: 47/52. Lesson18 attempt1: 1/1; incomplete.

### Answer history: p04-l18-application-v1

ID: p04-l18-application-v1
Phase04 — Computer Vision; Lesson18 — Open-Vocabulary Vision — CLIP.
Question53/84; lesson question2/3; application.

You want to use a pretrained CLIP model to classify images as cat, dog, or bicycle without task-specific training. Which inference procedure is appropriate?

A) Encode only the image, then use its three largest embedding coordinates as class scores.
B) Encode prompts such as "a photo of a cat", normalize image and text embeddings, and choose the class with highest cosine similarity.
C) Train a three-class linear head on labelled examples before making any predictions.
D) Encode class names with an unrelated text model and compare its raw vectors directly with CLIP image embeddings.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: Zero-shot CLIP classification encodes candidate class prompts with its aligned text encoder, normalizes both modalities, and selects the highest cosine similarity. No task-specific classifier training is required.
Phase04 running initial score: 48/53. Lesson18 attempt1: 2/2; incomplete.

### Answer history: p04-l18-code-v1

ID: p04-l18-code-v1
Phase04 — Computer Vision; Lesson18 — Open-Vocabulary Vision — CLIP.
Question54/84; lesson question3/3; code tracing.

These image and class-text embeddings are already L2-normalized. Which class does the code select, and what happens to that selection if the scores are multiplied by a positive logit scale before softmax?

```python
image = [0.6, 0.8]
texts = [[1.0, 0.0], [0.0, 1.0], [-1.0, 0.0]]
classes = ['cat', 'dog', 'bicycle']
scores = [sum(a*b for a, b in zip(image, text)) for text in texts]
pred = max(range(len(scores)), key=scores.__getitem__)
print(classes[pred])
```

A) cat; positive scaling changes the selection to dog.
B) bicycle; positive scaling changes the selection to cat.
C) dog; positive scaling changes the selection to bicycle.
D) dog; positive scaling preserves the selection, though softmax probabilities change.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: The cosine scores are [0.6,0.8,-0.6], so dog is selected. Multiplying all scores by a positive scale preserves their ordering and the softmax argmax, while changing the scale generally changes the softmax probabilities.
Phase04 running initial score: 49/54. Lesson18 attempt1 complete: 3/3. Lesson12 still requires a fresh full retake; lessons remain todo until phase pass.

### Answer history: p04-l19-concept-v1

ID: p04-l19-concept-v1
Phase04 — Computer Vision; Lesson19 — OCR & Document Understanding.
Question55/84; lesson question1/3; conceptual.

What does CTC allow an OCR recognizer to learn from a line image and its transcription without requiring character-by-character alignment labels?

A) A fixed one-to-one mapping where every image column must correspond to a different character.
B) A segmentation mask that assigns a document-layout category to every pixel.
C) A sequence objective that sums probabilities over valid frame-level paths collapsing to the target text.
D) A language-only objective that ignores the image and predicts text from the character frequencies.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: CTC marginalizes over time-step label paths that collapse to the transcription by merging adjacent repeated labels and then removing blanks. Training needs the target sequence, but not a separate character-to-time alignment.
Phase04 running initial score: 50/55. Lesson19 attempt1: 1/1; incomplete.

### Answer history: p04-l19-application-v1

ID: p04-l19-application-v1
Phase04 — Computer Vision; Lesson19 — OCR & Document Understanding.
Question56/84; lesson question2/3; application.

Your invoice system transcribes nearly every character correctly but often assigns the subtotal to invoice_total. Which improvement and evaluation best address this failure?

A) Add layout-aware key-value extraction and evaluate the extracted fields against labelled ground truth, such as with field-level F1.
B) Increase image resolution and report only character error rate, ignoring which field receives each value.
C) Sort all recognized numbers numerically and always choose the largest as invoice_total.
D) Replace field extraction with text-region detection and evaluate only bounding-box overlap.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Correct transcription does not ensure correct semantic field assignment. Layout-aware key-value extraction addresses which value belongs to invoice_total; field-level evaluation checks that assignment rather than only character accuracy or box localization.
Phase04 running initial score: 51/56. Lesson19 attempt1: 2/2; incomplete.

### Answer history: p04-l19-code-v1

ID: p04-l19-code-v1
Phase04 — Computer Vision; Lesson19 — OCR & Document Understanding.
Question57/84; lesson question3/3; code tracing.

Here '_' is the CTC blank. What does this greedy decoder print?

```python
path = ['b', 'b', '_', 'o', 'o', '_', 'o', 'k', 'k']
decoded = []
prev = None
for token in path:
    if token != prev and token != '_':
        decoded.append(token)
    prev = token
print(''.join(decoded))
```

A) bok
B) bboookk
C) bookk
D) book

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Adjacent b and k repeats collapse, as does the first adjacent o pair. The blank between the two o runs resets prev, so both o characters survive. The result is book.
Phase04 running initial score: 52/57. Lesson19 attempt1 complete: 3/3. Lesson12 still requires a fresh full retake; lessons remain todo until phase pass.

### Answer history: p04-l20-concept-v1

ID: p04-l20-concept-v1
Phase04 — Computer Vision; Lesson20 — Image Retrieval & Metric Learning.
Question58/84; lesson question1/3; conceptual.

For L2-normalized query and gallery embeddings, how are ranking by highest cosine similarity and ranking by smallest squared Euclidean distance related?

A) They agree only when every embedding has exactly two coordinates.
B) They give opposite rankings because cosine measures an angle rather than a distance.
C) They give the same ranking because squared distance equals 2 minus twice the cosine similarity.
D) They agree only after training a separate classifier on the gallery labels.

Learner answer: B. Correct answer: C. Result: incorrect.
Explanation: For unit vectors, squared Euclidean distance is ||a||^2+||b||^2-2*a dot b=2-2*cos(a,b). A higher cosine therefore means a smaller squared distance. Sorting cosine descending and distance ascending yields the same ranking, subject to ties and numerical precision.
Phase04 running initial score: 52/58. Lesson20 attempt1: 0/1; incomplete. Normalized cosine/L2 ranking equivalence added to the review queue.

### Answer history: p04-l20-application-v1

ID: p04-l20-application-v1
Phase04 — Computer Vision; Lesson20 — Image Retrieval & Metric Learning.
Question59/84; lesson question2/3; application.

Your product search must retrieve the exact shoe model shown in a query, but its results contain many different shoes of the same category. Which change best aligns training and evaluation with the goal?

A) Treat every shoe as a correct match and evaluate only category-level retrieval.
B) Train a category classifier and discard all information distinguishing shoe models.
C) Increase the index search depth and assume every same-category result is the exact model.
D) Define positives by product identity, fine-tune embeddings with instance-labelled pairs or triplets, and evaluate held-out identity matches.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Exact-product search is instance-level retrieval. Identity-labelled positives and negatives teach the embedding to distinguish different products within the same category, and held-out identity-match evaluation measures that goal directly.
Phase04 running initial score: 53/59. Lesson20 attempt1: 1/2; incomplete.

### Answer history: p04-l20-code-v1

ID: p04-l20-code-v1
Phase04 — Computer Vision; Lesson20 — Image Retrieval & Metric Learning.
Question60/84; lesson question3/3; code tracing.

This example uses unsquared Euclidean distances, matching the lesson's code implementation. What loss is printed, and does the negative satisfy the stated semi-hard condition d_ap < d_an < d_ap + margin?

```python
d_ap = 0.4
d_an = 0.5
margin = 0.2
loss = max(0.0, d_ap - d_an + margin)
print(round(loss, 2))
```

A) 0.0; no, because every negative farther than the positive has zero loss.
B) 0.1; yes, because 0.4 < 0.5 < 0.6.
C) 0.3; yes, because the margin is added to both distances.
D) 0.1; no, because semi-hard negatives must be closer than the positive.

Learner answer: D. Correct answer: B. Result: incorrect.
Explanation: The loss is max(0,0.4-0.5+0.2)=0.1. A semi-hard negative is farther than the positive but still within the margin: 0.4<0.5<0.6. A negative closer than the positive is hard, not semi-hard under this definition.
Phase04 running initial score: 53/60. Lesson20 attempt1 complete: 1/3, below the 2/3 minimum. Fresh full retakes required for Lessons12 and20 after initial coverage. Lessons remain todo until phase pass.

### Answer history: p04-l21-concept-v1

ID: p04-l21-concept-v1
Phase04 — Computer Vision; Lesson21 — Keypoint Detection & Pose Estimation.
Question61/84; lesson question1/3; conceptual.

Which statement correctly distinguishes top-down and bottom-up multi-person pose estimation?

A) Top-down predicts all joints before grouping them; bottom-up detects people before processing each crop.
B) Both methods must run a separate keypoint network for every detected person.
C) Top-down detects people then estimates joints per crop; bottom-up predicts joints across the image then groups them into people.
D) Top-down outputs only 3D joints; bottom-up outputs only 2D bounding boxes.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Top-down estimates keypoints within detected person crops. Bottom-up predicts keypoint candidates over the image and associates them into person instances afterward.
Phase04 running initial score: 54/61. Lesson21 attempt1: 1/1; incomplete.

### Answer history: p04-l21-application-v1

ID: p04-l21-application-v1
Phase04 — Computer Vision; Lesson21 — Keypoint Detection & Pose Estimation.
Question62/84; lesson question2/3; application.

A bottom-up pose model finds several shoulder and elbow candidates in a crowd. How can Part Affinity Fields help decide which shoulder and elbow belong together?

A) Match every shoulder to the highest-confidence elbow, regardless of position or limb direction.
B) Treat each keypoint heatmap's peak value as a unique person identifier.
C) Sort shoulders and elbows by horizontal position and pair them by index in every image.
D) Score candidate connections by alignment with the predicted limb vector field along the segment between them.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: PAFs predict limb-direction vectors over the image. A candidate shoulder-elbow connection is scored by sampling the vector field along its segment and aggregating alignment with the connection direction, helping associate joints into instances.
Phase04 running initial score: 55/62. Lesson21 attempt1: 2/2; incomplete.

### Answer history: p04-l21-code-v1

ID: p04-l21-code-v1
Phase04 — Computer Vision; Lesson21 — Keypoint Detection & Pose Estimation.
Question63/84; lesson question3/3; code tracing.

A keypoint heatmap has height3 and width4 and is flattened in row-major order. What (x,y) coordinates does this code print for its peak? Coordinates are zero-indexed in the heatmap grid.

```python
width = 4
flat_heatmap = [0.1, 0.0, 0.2, 0.1,
                0.0, 0.3, 0.1, 0.2,
                0.1, 0.9, 0.2, 0.0]
idx = max(range(len(flat_heatmap)), key=flat_heatmap.__getitem__)
y = idx // width
x = idx % width
print((x, y))
```

A) (1, 2)
B) (2, 1)
C) (9, 0)
D) (1, 3)

Learner answer: A. Correct answer: A. Result: correct.
Explanation: The peak0.9 occurs at flattened index9. With width4, y=9//4=2 and x=9%4=1, giving heatmap-grid coordinates(1,2).
Phase04 running initial score: 56/63. Lesson21 attempt1 complete: 3/3. Lessons12 and20 still require fresh full retakes; lessons remain todo until phase pass.

### Answer history: p04-l22-concept-v1

ID: p04-l22-concept-v1
Phase04 — Computer Vision; Lesson22 — 3D Gaussian Splatting from Scratch.
Question64/84; lesson question1/3; conceptual.

Which description correctly contrasts the core scene representation and rendering approach of 3D Gaussian Splatting with a conventional MLP-based NeRF?

A) 3DGS stores one independent RGB image per camera and retrieves the nearest view without projecting geometry.
B) 3DGS stores explicit Gaussian primitives, projects their footprints to the image, and depth-orders them for alpha compositing.
C) 3DGS stores the scene only as MLP weights and queries that MLP hundreds of times along every pixel ray.
D) 3DGS converts every scene into a watertight triangle mesh and renders only opaque surfaces.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: 3DGS represents the scene with explicit Gaussian parameters, projects each Gaussian to a screen-space footprint, and composites depth-ordered contributions. A conventional NeRF instead queries a learned density-and-colour field at samples along rays.
Phase04 running initial score: 57/64. Lesson22 attempt1: 1/1; incomplete.

### Answer history: p04-l22-application-v1

ID: p04-l22-application-v1
Phase04 — Computer Vision; Lesson22 — 3D Gaussian Splatting from Scratch.
Question65/84; lesson question2/3; application.

During 3DGS training, a large Gaussian has a high position-gradient magnitude in an underfit detailed region, while other Gaussians have nearly zero opacity. Which adaptive update matches the lesson's strategy?

A) Enlarge the high-gradient Gaussian further and duplicate every near-transparent Gaussian.
B) Freeze all Gaussian positions and remove spherical harmonics from the entire scene.
C) Split the large high-gradient Gaussian into smaller ones and prune the nearly transparent Gaussians.
D) Delete all high-gradient Gaussians and retain only those with near-zero opacity.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Splitting a large high-gradient Gaussian adds smaller primitives where more detail is needed. Pruning nearly transparent Gaussians removes primitives making little contribution. The adaptive changes complement gradient updates to existing parameters.
Phase04 running initial score: 58/65. Lesson22 attempt1: 2/2; incomplete.

### Answer history: p04-l22-code-v1

ID: p04-l22-code-v1
Phase04 — Computer Vision; Lesson22 — 3D Gaussian Splatting from Scratch.
Question66/84; lesson question3/3; code tracing.

This 2D example forms a Gaussian covariance from positive axis scales and a 90-degree rotation. What does it print, rounded to one decimal place?

```python
import numpy as np
scales = np.array([2.0, 1.0])
R = np.array([[0.0, -1.0], [1.0, 0.0]])
cov = R @ np.diag(scales ** 2) @ R.T
print(np.round(cov, 1).tolist())
```

A) [[2.0, 0.0], [0.0, 1.0]]
B) [[4.0, 0.0], [0.0, 1.0]]
C) [[0.0, -2.0], [1.0, 0.0]]
D) [[1.0, 0.0], [0.0, 4.0]]

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Squaring the scales gives variances4 and1 along the original axes. The90-degree rotation swaps their orientation, giving covariance [[1,0],[0,4]].
Phase04 running initial score: 59/66. Lesson22 attempt1 complete: 3/3. Lessons12 and20 still require fresh full retakes; lessons remain todo until phase pass.

### Answer history: p04-l23-concept-v1

ID: p04-l23-concept-v1
Phase04 — Computer Vision; Lesson23 — Diffusion Transformers & Rectified Flow.
Question67/84; lesson question1/3; conceptual.

In the lesson's rectified-flow convention, x_t=(1-t)*x0+t*epsilon, where x0 is clean data and epsilon is noise. What velocity target is used for training, and in which direction does sampling integrate time?

A) Target epsilon-x0; sampling moves from t=1 toward t=0.
B) Target epsilon-x0; sampling moves from t=0 toward t=1.
C) Target x0 alone; sampling moves from t=1 toward t=0.
D) Target epsilon alone; sampling keeps t fixed at1.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Differentiating the interpolation with respect to t gives epsilon-x0. With this convention, t=1 is noise and t=0 is clean data, so generation integrates the learned velocity backward in time.
Phase04 running initial score: 60/67. Lesson23 attempt1: 1/1; incomplete.

### Answer history: p04-l23-application-v1

ID: p04-l23-application-v1
Phase04 — Computer Vision; Lesson23 — Diffusion Transformers & Rectified Flow.
Question68/84; lesson question2/3; application.

You are implementing the lesson's DiT block and want timestep conditioning to affect transformer computation while making each residual block start as an identity mapping. Which design achieves both?

A) Add a constant timestep label to the training loss while leaving every transformer operation unconditioned.
B) Replace all patch tokens with the timestep embedding and remove the residual path.
C) Predict adaptive LayerNorm scale, shift, and residual gates from conditioning, initializing the gates to zero.
D) Initialize all residual gates to one and discard the conditioning vector before normalization.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Adaptive LayerNorm uses conditioning-derived scale and shift to modulate normalized tokens. Zero-initialized residual gates initially suppress attention and MLP updates, so the full residual block initially returns its input. Training can then learn conditioning-dependent updates.
Phase04 running initial score: 61/68. Lesson23 attempt1: 2/2; incomplete.

### Answer history: p04-l23-code-v1

ID: p04-l23-code-v1
Phase04 — Computer Vision; Lesson23 — Diffusion Transformers & Rectified Flow.
Question69/84; lesson question3/3; code tracing.

For this scalar training pair, assume an oracle predicts the exact constant path velocity at every sampling step. What does the code print?

```python
x0 = 2.0
epsilon = -1.0
t = 0.25
xt = (1 - t) * x0 + t * epsilon
velocity = epsilon - x0

x = epsilon
for _ in range(4):
    x = x - 0.25 * velocity
print(xt, velocity, x)
```

A) 1.25 -3.0 -4.0
B) 1.25 -3.0 2.0
C) 0.5 3.0 2.0
D) 1.25 -1.0 0.0

Learner answer: B. Correct answer: B. Result: correct.
Explanation: xt=0.75*2+0.25*(-1)=1.25 and velocity=-1-2=-3. Each backward Euler step adds0.75, so four steps take x from-1 to2. Exact reconstruction here relies on the stipulated oracle constant velocity.
Phase04 running initial score: 62/69. Lesson23 attempt1 complete: 3/3. Lessons12 and20 still require fresh full retakes; lessons remain todo until phase pass.

### Answer history: p04-l24-concept-v1

ID: p04-l24-concept-v1
Phase04 — Computer Vision; Lesson24 — SAM 3 & Open-Vocabulary Segmentation.
Question70/84; lesson question1/3; conceptual.

In the lesson, what task does Promptable Concept Segmentation describe?

A) Assign a single fixed-category label to the whole image, without localizing objects.
B) Return only a bounding box for the one object nearest a clicked point.
C) Produce a caption listing every visible object, without any pixel masks.
D) Given a concept phrase or image exemplar, produce separate masks for matching object instances.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: The lesson defines Promptable Concept Segmentation as using a concept phrase or exemplar to find matching instances and return their individual masks, rather than requiring a separate point or box prompt for each instance.
Phase04 running initial score: 63/70. Lesson24 attempt1: 1/1; incomplete.

### Answer history: p04-l24-application-v1

ID: p04-l24-application-v1
Phase04 — Computer Vision; Lesson24 — SAM 3 & Open-Vocabulary Segmentation.
Question71/84; lesson question2/3; application.

An image contains no objects matching the concept prompt "yellow school bus", but a segmentation system still returns a weak unrelated mask. What is the purpose of the lesson's presence head in addressing this problem?

A) It assesses whether the prompted concept is present, separating existence confidence from localization.
B) It guarantees every concept prompt yields at least one mask by choosing the largest region.
C) It replaces the text prompt with the most common object category in the training set.
D) It converts every candidate box into a perfect mask without inspecting the image.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: The presence head estimates whether a prompted concept occurs, distinct from predicting its location or mask. This helps reduce false positives for absent concepts; it is not a guarantee of perfect rejection.
Phase04 running initial score: 64/71. Lesson24 attempt1: 2/2; incomplete.

### Answer history: p04-l24-code-v1

ID: p04-l24-code-v1
Phase04 — Computer Vision; Lesson24 — SAM 3 & Open-Vocabulary Segmentation.
Question72/84; lesson question3/3; code tracing.

The lesson's custom run-length encoder processes a nonempty flattened binary mask. What string does this code print? Each run is stored as value x count.

```python
flat = [0, 0, 1, 1, 1, 0]
runs = []
prev, count = flat[0], 0
for value in flat:
    if value == prev:
        count += 1
    else:
        runs.append((prev, count))
        prev, count = value, 1
runs.append((prev, count))
print(';'.join(f'{v}x{c}' for v, c in runs))
```

A) 0x3;1x3
B) 0x2;1x3
C) 0x2;1x3;0x1
D) 0x1;0x1;1x1;1x1;1x1;0x1

Learner answer: C. Correct answer: C. Result: correct.
Explanation: The flattened mask contains runs of two zeros, three ones, and one zero. The final append preserves the trailing run, producing0x2;1x3;0x1. This is the lesson's custom format, not a claim of compatibility with standard COCO RLE.
Phase04 running initial score: 65/72. Lesson24 attempt1 complete: 3/3. Lessons12 and20 still require fresh full retakes; lessons remain todo until phase pass.

### Answer history: p04-l25-concept-v1

ID: p04-l25-concept-v1
Phase04 — Computer Vision; Lesson25 — Vision-Language Models — The ViT-MLP-LLM Pattern.
Question73/84; lesson question1/3; conceptual.

In the lesson's ViT-projector-LLM architecture, what is the projector's main role?

A) Convert the language model's output text back into the original image pixels.
B) Map visual token features into the LLM's embedding space so the LLM can consume them alongside text embeddings.
C) Assign every image a fixed class label and discard its patch features before the LLM runs.
D) Replace the vision encoder by tokenizing raw image bytes with the ordinary text tokenizer.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: The projector transforms visual token features into vectors compatible with the LLM's input embedding space. The language model then consumes projected visual tokens along with text embeddings to generate its answer.
Phase04 running initial score: 66/73. Lesson25 attempt1: 1/1; incomplete.

### Answer history: p04-l25-application-v1

ID: p04-l25-application-v1
Phase04 — Computer Vision; Lesson25 — Vision-Language Models — The ViT-MLP-LLM Pattern.
Question74/84; lesson question2/3; application.

You are implementing the lesson's initial VLM alignment stage using a pretrained vision encoder, a new projector, and a pretrained LLM. Which training setup matches that stage?

A) Freeze all components and change only the image-placeholder token's printed name.
B) Train only the vision encoder on class labels while bypassing the projector and LLM.
C) Freeze the vision encoder and LLM parameters, and train the projector on image-caption pairs through the caption-generation loss.
D) Train the LLM on text-only data and replace every image embedding with zeros.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: The lesson's initial alignment stage freezes pretrained vision and LLM parameters and learns the projector from image-caption pairs. The caption loss still needs to backpropagate through LLM operations to the projected visual embeddings; frozen LLM weights do not mean disabling that gradient path.
Phase04 running initial score: 67/74. Lesson25 attempt1: 2/2; incomplete.

### Answer history: p04-l25-code-v1

ID: p04-l25-code-v1
Phase04 — Computer Vision; Lesson25 — Vision-Language Models — The ViT-MLP-LLM Pattern.
Question75/84; lesson question3/3; code debugging.

In the lesson's simplified merge routine, one prompt contains two image-placeholder positions, but the projector outputs four visual tokens. All embedding widths match. What happens with this check?

```python
positions = [1, 2]
vision_token_count = 4
if len(positions) != vision_token_count:
    raise ValueError('image token count mismatch')
# Otherwise replace one placeholder embedding per visual token.
```

A) It raises ValueError; this routine requires one placeholder position per projected visual token.
B) It automatically averages four visual tokens into two placeholder embeddings.
C) It silently inserts the extra tokens and expands the attention mask.
D) It succeeds because matching embedding widths make token counts irrelevant.

Learner answer: A. Correct answer: A. Result: correct.
Explanation: Two placeholder positions do not match four projected visual tokens, so this simplified one-to-one replacement routine raises ValueError. Matching embedding widths is necessary but does not resolve a token-count mismatch.
Phase04 running initial score: 68/75. Lesson25 attempt1 complete: 3/3. Lessons12 and20 still require fresh full retakes; lessons remain todo until phase pass.

### Answer history: p04-l26-concept-v1

ID: p04-l26-concept-v1
Phase04 — Computer Vision; Lesson26 — Monocular Depth & Geometry Estimation.
Question76/84; lesson question1/3; conceptual.

A monocular model outputs relative depth with no metric calibration. What can you conclude from that output alone?

A) Every output value is a distance in metres because the input is an RGB photograph.
B) The model has recovered hidden surfaces and exact physical object dimensions.
C) It can indicate nearer-versus-farther structure, but its raw values do not establish distances in metres.
D) Every output value can be converted to metres by dividing by image width.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: Relative depth can express depth ordering without a metric scale. Raw values alone do not establish distances in metres or exact dimensions, and a single image does not reveal occluded geometry reliably.
Phase04 running initial score: 69/76. Lesson26 attempt1: 1/1; incomplete.

### Answer history: p04-l26-application-v1

ID: p04-l26-application-v1
Phase04 — Computer Vision; Lesson26 — Monocular Depth & Geometry Estimation.
Question77/84; lesson question2/3; application.

For the lesson's relative-depth evaluation protocol, predictions may differ from valid ground-truth depth by an unknown scale and shift. What should you do before reporting the aligned depth error?

A) Treat raw predictions as metres and include invalid zero-depth pixels in the error.
B) Fit scale and shift on valid pixels, align predictions, and compute metrics with invalid pixels masked out.
C) Replace predictions with ground-truth values, then report their zero reconstruction error.
D) Divide every prediction by the number of image pixels and assume this recovers physical scale.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: This protocol fits a scale-and-shift alignment using valid ground-truth pixels and excludes invalid depth values from fitting and metrics. The reported error measures relative geometry after alignment, not uncalibrated metric-distance accuracy at deployment.
Phase04 running initial score: 70/77. Lesson26 attempt1: 2/2; incomplete.

### Answer history: p04-l26-code-v1

ID: p04-l26-code-v1
Phase04 — Computer Vision; Lesson26 — Monocular Depth & Geometry Estimation.
Question78/84; lesson question3/3; code tracing.

The depth value below is camera-axis Z depth in metres, and the intrinsics correspond to the same pixel coordinate system. What camera-coordinate point does the code print?

```python
u, v = 420.0, 190.0
fx, fy, cx, cy = 500.0, 500.0, 320.0, 240.0
d = 2.0
X = (u - cx) * d / fx
Y = (v - cy) * d / fy
Z = d
print((X, Y, Z))
```

A) (0.2, -0.1, 2.0)
B) (0.4, 0.2, 2.0)
C) (100.0, -50.0, 2.0)
D) (0.4, -0.2, 2.0)

Learner answer: D. Correct answer: D. Result: correct.
Explanation: X=(420-320)*2/500=0.4, Y=(190-240)*2/500=-0.2, and Z=2. All three camera-coordinate components are in metres under the stated metric Z-depth convention.
Phase04 running initial score: 71/78. Lesson26 attempt1 complete: 3/3. Lessons12 and20 still require fresh full retakes; lessons remain todo until phase pass.

### Answer history: p04-l27-concept-v1

ID: p04-l27-concept-v1
Phase04 — Computer Vision; Lesson27 — Multi-Object Tracking & Video Memory.
Question79/84; lesson question1/3; conceptual.

What does multi-object tracking add to independent per-frame object detection?

A) A requirement that every object have exactly the same bounding-box coordinates in every frame.
B) Persistent identities that associate detections of the same physical object across frames.
C) A fixed new category label for every frame, without linking individual objects.
D) Guaranteed recovery of every fully occluded object from a single image.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: Tracking associates detections across time into persistent object identities. This enables trajectories, duration measurements, and counting without treating each frame's observation as a new object.
Phase04 running initial score: 72/79. Lesson27 attempt1: 1/1; incomplete.

### Answer history: p04-l27-application-v1

ID: p04-l27-application-v1
Phase04 — Computer Vision; Lesson27 — Multi-Object Tracking & Video Memory.
Question80/84; lesson question2/3; application.

A tracked person becomes partially occluded, lowering detection confidence. Following ByteTrack's two-stage association idea, what should happen after matching high-confidence detections?

A) Immediately delete all unmatched tracks, regardless of their recent history.
B) Create a new track for every low-confidence detection before considering existing tracks.
C) Attempt to associate remaining tracks with suitable low-confidence detections to preserve their identities.
D) Replace all low-confidence boxes with the full image and assign them the same track ID.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: ByteTrack first associates high-confidence detections, then attempts to match remaining tracks to low-confidence candidates. Some low scores come from occlusion rather than background, so suitable second-stage matches can preserve identity.
Phase04 running initial score: 73/80. Lesson27 attempt1: 2/2; incomplete.

### Answer history: p04-l27-code-v1

ID: p04-l27-code-v1
Phase04 — Computer Vision; Lesson27 — Multi-Object Tracking & Video Memory.
Question81/84; lesson question3/3; code tracing.

Rows are tracks0 and1; columns are detections0 and1. Every pair passes the association gate. Which assignment minimizes total cost, and what total does the code compute for it?

```python
iou = [[0.9, 0.8],
       [0.85, 0.1]]
cost = [[1.0 - value for value in row] for row in iou]
straight = cost[0][0] + cost[1][1]
crossed = cost[0][1] + cost[1][0]
print(round(straight, 2), round(crossed, 2))
```

A) Track0 to detection0 and track1 to detection1; total0.10.
B) Track0 to detection0 and track1 to detection0; total0.25.
C) Track0 to detection0 and track1 to detection1; total1.00.
D) Track0 to detection1 and track1 to detection0; total0.35.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: Straight cost is0.1+0.9=1.0; crossed cost is0.2+0.15=0.35. The crossed one-to-one assignment minimizes total cost. Choosing detection0 for both tracks is not a valid one-to-one assignment.
Phase04 running initial score: 74/81. Lesson27 attempt1 complete: 3/3. Lessons12 and20 still require fresh full retakes; lessons remain todo until phase pass.

### Answer history: p04-l28-concept-v1

ID: p04-l28-concept-v1
Phase04 — Computer Vision; Lesson28 — World Models & Video Diffusion.
Question82/84; lesson question1/3; conceptual.

What distinguishes an action-conditioned world model from a video generator conditioned only on an initial text or image prompt?

A) It must render a physically exact simulation and cannot produce uncertain futures.
B) It predicts future observations using the current or past state together with actions, enabling action-dependent rollouts.
C) It ignores previous observations and samples each frame independently of the chosen actions.
D) It produces only a single category label rather than predicting future states or observations.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: An action-conditioned world model uses state or observation history and actions to predict future states or observations. Different actions can lead to different predicted futures; learned rollouts need not be physically exact.
Phase04 running initial score: 75/82. Lesson28 attempt1: 1/1; incomplete.

### Answer history: p04-l28-application-v1

ID: p04-l28-application-v1
Phase04 — Computer Vision; Lesson28 — World Models & Video Diffusion.
Question83/84; lesson question2/3; application.

In the lesson's VLM + world model + inverse dynamics robotics loop, which assignment of roles is correct?

A) The VLM produces depth maps only; the world model reads motor currents; inverse dynamics writes image captions.
B) The VLM directly measures future observations; the world model guarantees success; inverse dynamics supplies text prompts.
C) The VLM selects high-level plans; the world model predicts resulting observations; inverse dynamics estimates actions that connect observations.
D) The VLM replaces feedback; the world model supplies ground-truth physics; inverse dynamics is used only to score language fluency.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: In this architecture pattern, the VLM proposes high-level plans, a world model imagines future observations, and inverse dynamics estimates actions for observation transitions. Actual execution and new observations provide feedback; predictions do not guarantee success.
Phase04 running initial score: 76/83. Lesson28 attempt1: 2/2; incomplete.

### Answer history: p04-l28-code-v1

ID: p04-l28-code-v1
Phase04 — Computer Vision; Lesson28 — World Models & Video Diffusion.
Question84/84; lesson question3/3; code tracing.

What are the token tensor shape and (time,height,width) grid after this non-overlapping 3D patch embedding? The convolution uses no padding.

```python
import torch
from torch import nn
video = torch.zeros(1, 4, 8, 16, 16)  # batch, channels, time, height, width
proj = nn.Conv3d(4, 64, kernel_size=(2, 2, 2), stride=(2, 2, 2))
z = proj(video)
b, c, t, h, w = z.shape
tokens = z.reshape(b, c, t*h*w).transpose(1, 2)
print(tuple(tokens.shape), (t, h, w))
```

A) (1, 256, 64) and (4, 8, 8)
B) (1, 2048, 64) and (8, 16, 16)
C) (1, 64, 256) and (4, 8, 8)
D) (1, 128, 64) and (2, 8, 8)

Learner answer: A. Correct answer: A. Result: correct.
Explanation: The convolution halves time, height and width, producing grid(4,8,8). There are4*8*8=256 tokens, each with64 channels, giving token shape(1,256,64).
Phase04 initial assessment complete:77/84 (91.67%). Lesson28 attempt1 complete:3/3. Overall threshold met, but Lessons12 and20 each scored1/3, below the required2/3. Phase and all lessons remain todo until scored remediation meets both passing conditions.

### Phase04 initial assessment summary

- Initial correct:77/84 (91.67%); all28 lessons covered.
- Lesson minimum failures:12-video-understanding1/3 and20-image-retrieval-metric1/3.
- Other lessons:08,09,13 each2/3; all remaining23 lessons3/3.
- Missed question IDs: p04-l08-application-v1, p04-l09-code-v1, p04-l12-concept-v1, p04-l12-application-v1, p04-l13-concept-v1, p04-l20-concept-v1, p04-l20-code-v1.
- Next: fresh full scored retake for Lesson12, then Lesson20; no extra unscored review. Latest complete retake replaces the lesson's effective score, even if worse; incomplete sets leave effective score unchanged.

### Answer history: p04-l12-concept-v2

ID: p04-l12-concept-v2
Phase04 — Computer Vision; Lesson12 — Video Understanding — Temporal Modeling.
Retake attempt2; lesson question1/3; conceptual.

What does extending a convolutional kernel over the time dimension allow a video model to learn that independent per-frame encoding followed by simple mean pooling cannot capture?

A) A guarantee that reversing every clip leaves all motion-sensitive features unchanged.
B) Local patterns of how spatial features change across ordered neighboring frames.
C) Exact future trajectories without observing any previous frames.
D) A replacement for all spatial processing with a single frame-independent class label.

Learner answer: B. Correct answer: B. Result: correct.
Explanation: A temporal kernel learns ordered local changes across neighboring frames. Independent frame features followed by simple mean pooling discard their sequence order and cannot distinguish permutations of the same frame set.
Lesson12 attempt2 running score:1/1; incomplete. Phase04 latest complete sets remain77/84 (91.67%); cumulative scored responses85, correct78. Lesson20 retake still required.

### Answer history: p04-l12-application-v2

ID: p04-l12-application-v2
Phase04 — Computer Vision; Lesson12 — Video Understanding — Temporal Modeling.
Retake attempt2; lesson question2/3; application.

You train a 3D CNN to recognize a brief hand gesture from a long video. Each training example should preserve fine motion over eight neighboring frames. Which sampling strategy best fits that requirement?

A) Randomly choose eight frames from the entire video and shuffle their order.
B) Repeat the video's first frame eight times so every example has the correct shape.
C) Average all video frames into one image and copy it eight times.
D) Choose a contiguous eight-frame window and keep its chronological order.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: A contiguous eight-frame window in chronological order preserves neighboring motion for the temporal convolution. Random shuffling destroys order, and repeated or averaged frames remove motion information.
Lesson12 attempt2 running score:2/2; incomplete. Phase04 latest complete sets remain77/84 (91.67%); cumulative scored responses86, correct79. Lesson20 retake still required.

### Answer history: p04-l12-code-v2

ID: p04-l12-code-v2
Phase04 — Computer Vision; Lesson12 — Video Understanding — Temporal Modeling.
Retake attempt2; lesson question3/3; code tracing.

These are scalar features from the same three frames in opposite temporal orders. What does this simplified temporal convolution print?

```python
forward = [1.0, 2.0, 4.0]
reverse = list(reversed(forward))
kernel = [-1.0, 0.0, 1.0]
def temporal_response(frames):
    return sum(w * value for w, value in zip(kernel, frames))
print(temporal_response(forward), temporal_response(reverse))
```

A) 3.0 -3.0
B) 3.0 3.0
C) 7.0 7.0
D) -3.0 3.0

Learner answer: A. Correct answer: A. Result: correct.
Explanation: The forward response is -1+4=3; the reversed response is -4+1=-3. Ordered temporal weights distinguish time reversal, while an order-invariant mean would be identical for these frame sets.
Lesson12 attempt2 complete:3/3, replacing initial1/3 in the effective score. Phase04 latest complete sets79/84 (94.05%); cumulative scored responses87, correct80. Lesson20 still needs a fresh full retake; phase and lessons remain todo until phase pass.

### Answer history: p04-l20-concept-v2

ID: p04-l20-concept-v2
Phase04 — Computer Vision; Lesson20 — Image Retrieval & Metric Learning.
Retake attempt2; lesson question1/3; conceptual.

Two gallery items have cosine similarities0.9 and0.6 to a query. All three embeddings are unit length. What are their squared Euclidean distances to the query, and which item ranks first by smallest distance?

A) Distances1.8 and1.2; the item with cosine0.6 ranks first.
B) Distances0.1 and0.4; the item with cosine0.6 ranks first.
C) Distances0.2 and0.8; the item with cosine0.9 ranks first.
D) Distances0.9 and0.6; the item with cosine0.6 ranks first.

Learner answer: C. Correct answer: C. Result: correct.
Explanation: For unit vectors, squared distance=2-2*cosine. The distances are0.2 and0.8, so cosine0.9 gives the nearest item. Maximizing cosine and minimizing squared distance yield the same ranking.
Lesson20 attempt2 running score:1/1; incomplete. Phase04 latest complete sets remain79/84 (94.05%); cumulative scored responses88, correct81.

### Answer history: p04-l20-application-v2

ID: p04-l20-application-v2
Phase04 — Computer Vision; Lesson20 — Image Retrieval & Metric Learning.
Retake attempt2; lesson question2/3; application.

For triplet training with unsquared Euclidean distances, an anchor's positive is at distance0.5 and the margin is0.3. Three different-identity negatives are at distances0.2,0.65,and1.1. Which is semi-hard under d_ap < d_an < d_ap + margin?

A) Distance0.2, because it is closer than the positive.
B) Distance1.1, because it is far beyond the margin.
C) All three, because their identities differ from the anchor's.
D) Distance0.65, because it is farther than the positive but inside the margin.

Learner answer: D. Correct answer: D. Result: correct.
Explanation: The semi-hard interval is0.5<d_an<0.8, so0.65 qualifies. The0.2 negative is hard because it is closer than the positive;1.1 is an easy negative outside the margin.
Lesson20 attempt2 running score:2/2; incomplete. Phase04 latest complete sets remain79/84 (94.05%); cumulative scored responses89, correct82.

### Answer history: p04-l20-code-v2

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

A) 0.375
B) 0.75
C) 1.0
D) 0.5

Learner answer: A. Correct answer: B. Result: incorrect.
Explanation: Queries A,B,andD each have at least one correct match among their top2 results; C does not. The query hit rate is3/4=0.75. Dividing three matches by eight returned items gives0.375, a different statistic, not the lesson's recall@2.
Lesson20 attempt2 complete:2/3, replacing initial1/3 in the effective score. Phase04 latest complete sets80/84 (95.24%); cumulative scored responses90, correct82. All28 lessons now meet the minimum2/3 and the phase passes.

### Phase04 mastery completion — 2026-10-24

- Passed: latest complete lesson sets80/84 (95.24%), exceeding required72/84. Every lesson meets minimum2/3.
- Initial77/84 (91.67%) preserved. Lesson12 fresh retake3/3 and Lesson20 fresh retake2/3. All questions, answers, and explanations preserved; cumulative90 scored responses,82 correct.
- Latest scores01–28:3,3,3,3,3,3,3,2,2,3,3,3,2,3,3,3,3,3,3,2,3,3,3,3,3,3,3,3.
- All28 lessons marked done by quiz-based mastery; implementation labs not performed in this assessment. One normal progress entry per lesson added to LEARNING.md.
- Residual review: both Mask R-CNN predictors and background class(L08), detach and discriminator gradients(L09), PointNet permutation invariance(L13), retrieval query hit-rate denominator(L20). Temporal modeling and normalized cosine/L2 and semi-hard negative topics remediated in scored retakes; retained for spaced recall.
- Next: Phase05 — NLP — Foundations to Advanced, Lesson01 Text Processing — Tokenization, Stemming, Lemmatization, question1/87, not yet presented. No pending answer at phase boundary.

