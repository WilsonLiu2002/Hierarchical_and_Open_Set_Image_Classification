# Hierarchical and Open-Set Image Classification
 
**Authors:** Linshuo Li, Zhentao Yang, Jiacheng Liu  


## Overview

This project addresses hierarchical and open-set image classification tasks, where models must predict:
- A **superclass** (e.g., dog, bird, reptile)
- A **subclass** (e.g., golden retriever, hawk)

Models are expected to generalize to **unseen superclasses and subclasses** that only appear during testing.

---

## Methods

### Models Investigated
- **LeNet-5**: A shallow CNN baseline
- **ResNet-50**: A modern CNN baseline with two-phase fine-tuning
- **ViT-B/32**: Vision Transformer fine-tuned for hierarchical classification
- **Dual-Head CLIP**: CLIP vision encoder with lightweight adapters and novelty detection

### Key Techniques
- **Confidence Thresholding**: Apply tuned thresholds to softmax outputs to detect out-of-distribution inputs.
- **Synthetic Data Generation**: Create novel examples using text-to-image diffusion models (Stable Diffusion).
- **Two-Stage Inference**: Predict superclass first, then subclass conditioned on the superclass.

---

## Results

### Full Performance Table

| Model Variant | Superclass Accuracy | Seen Superclass Accuracy | Unseen Superclass Accuracy | Subclass Accuracy | Seen Subclass Accuracy | Unseen Subclass Accuracy |
|:--------------|:---------------------|:-------------------------|:---------------------------|:------------------|:------------------------|:--------------------------|
| Dual-Head CLIP | 90.50% | 99.18% | 68.48% | 25.09% | 72.74% | 12.22% |
| Dual-Head CLIP + Thresholding | 89.03% | 92.64% | 79.84% | 81.06% | 83.59% | 80.37% |
| ResNet-50 | 42.16% | 58.77% | 0.00% | 0.50% | 2.36% | 0.00% |
| ViT-Tiny + Thresholding | 26.01% | 30.92% | 13.54% | 67.08% | 0.17% | 85.14% |
| 1-stage ViT-B/32 | 25.30% | 35.06% | 0.54% | 6.12% | 1.72% | 7.30% |
| 2-stage ViT-B/32 | 24.94% | 34.68% | 0.22% | 4.67% | 1.77% | 5.45% |
| 2-stage ViT-B/32 + Thresholding | 24.74% | 12.26% | 56.42% | 74.47% | 0.13% | 94.55% |
| 1-stage ViT-B/32 + Thresholding | 24.36% | 28.49% | 13.89% | 46.42% | 0.97% | 58.70% |
| LeNet-5 | 21.50% | 29.87% | 0.00% | 0.13% | 0.59% | 0.00% |

**Note:** "Thresholding" refers to applying tuned softmax confidence thresholds for open-set detection.

---

## Findings

- **Thresholding** is crucial for effective open-set detection.
- **CLIP-based models** outperform CNN and ViT baselines, especially for unseen class detection.
- **Synthetic augmentation** with diffusion-generated data improves subclass generalization.
- **Vision-language pretraining** (as in CLIP) provides robust representations for open-world recognition.




