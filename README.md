# Kidney Microvascular Segmentation with 2D U-Net

**Medical Image Analysis · MATLAB · Histopathology Image Segmentation**

An individual course project exploring **blood-vessel segmentation in PAS-stained kidney histology images**, inspired by the [HuBMAP — Hacking the Human Vasculature](https://www.kaggle.com/competitions/hubmap-hacking-the-human-vasculature) challenge.

The aim was to process annotated histology tiles, train a **2D U-Net** to distinguish vessel regions from the background, and export segmentation predictions. This repository preserves the original implementation, coursework report, trained model, and output files as a **learning and experiment record**, not a validated clinical model.

## At a Glance

| | |
| --- | --- |
| **Task** | Binary blood-vessel vs. background segmentation |
| **Input** | PAS-stained kidney histology image tiles |
| **Approach** | 2D U-Net, polygon-mask conversion, augmentation, Dice-based training |
| **Implementation** | MATLAB Live Script |
| **Outputs** | 10 sets of predicted TIFF images and corresponding JSON coordinates |
| **Context** | Individual medical image analysis coursework (2025) |

## Methodology

1. **Dataset preparation.** Worked with an instructional subset of the HuBMAP-related data, selecting 289 expert-reviewed tiles from Dataset 1 as described in the original report.
2. **Annotation processing.** Converted polygon coordinates from JSON annotations into pixel-level segmentation masks using MATLAB's `poly2mask`.
3. **Preprocessing and augmentation.** Prepared training images and masks with geometric augmentation.
4. **Segmentation model.** Constructed a 2D U-Net for vessel/background prediction and used a Dice-based loss to focus learning on the relatively small foreground regions.
5. **Training and validation.** Used an approximately 85% / 15% sample split in the coursework workflow.
6. **Prediction export.** Generated TIFF output images and JSON files representing predicted vessel-region coordinates.

This summary describes the historical coursework workflow. For implementation specifics, inspect the [MATLAB Live Script](./hw1_SegmentMicrovascular.mlx) and the [original report](./%E9%86%AB%E5%AD%B8%E5%BD%B1%E5%83%8F%E5%88%86%E6%9E%90%E5%B0%88%E9%A1%8CHW1.pdf).

## Results and Lessons Learned

- The original report recorded **approximately 92% training accuracy**. This is a *training* figure, **not** a held-out test Dice/IoU score or evidence of clinical accuracy.
- The strong background majority made overall pixel accuracy a potentially misleading metric. Investigating this motivated the use of a foreground-focused **Dice loss**.
- I considered stain normalization, including Vahadane-style methods, but **did not include it in the final pipeline** due to compatibility and dependency constraints.
- The project highlighted the importance of segmentation-aware evaluation, careful annotation processing, and distinguishing visually plausible predictions from robust quantitative evidence.

### Important evaluation limitations

The historical sample split and augmentation workflow should not be treated as proof of independent generalization. In particular, a stronger follow-up study should split data **by original image or whole-slide/patient source before augmentation**, and evaluate **Dice and IoU on genuinely held-out images**.

No external benchmark, official competition score, or independent clinical validation is claimed for this repository.

## Repository Contents

| File / folder | Purpose |
| --- | --- |
| [`hw1_SegmentMicrovascular.mlx`](./hw1_SegmentMicrovascular.mlx) | Original MATLAB Live Script — main implementation and experiment workflow |
| [`trainedModel2025-04-02-14-10.mat`](./trainedModel2025-04-02-14-10.mat) | Saved training artifact (MATLAB MAT file) |
| [`醫學影像分析專題hw1.pdf`](./%E9%86%AB%E5%AD%B8%E5%BD%B1%E5%83%8F%E5%88%86%E6%9E%90%E5%B0%88%E9%A1%8Chw1.pdf) | Original project report, explanations, and experimental illustrations |
| [`醫學影像分析專題HW1.docx`](./%E9%86%AB%E5%AD%B8%E5%BD%B1%E5%83%8F%E5%88%86%E6%9E%90%E5%B0%88%E9%A1%8CHW1.docx) | Editable copy of the original report |
| [`Predicted_images/`](./Predicted_images) | Predicted TIFF image files (two files per indexed case) |
| [`Predicted_json/`](./Predicted_json) | Prediction-coordinate JSON files (one per indexed case) |

The JSON files use fields such as `type` and `coordinates` to record predicted vessel regions. GitHub may not preview TIFF files inline; download them and open with a TIFF-capable image viewer or MATLAB.

## How to Explore

**Software:** MATLAB with relevant image-processing and deep-learning functionality. Exact required MATLAB/toolbox versions have not been independently verified.

1. Download or clone this repository:
   ```bash
   git clone https://github.com/Wendylin0112/Kidney-Microvascular-Segmentation.git
   ```
2. Open `hw1_SegmentMicrovascular.mlx` in MATLAB and read its sections before executing.
3. Review the [report PDF](./%E9%86%AB%E5%AD%B8%E5%BD%B1%E5%83%8F%E5%88%86%E6%9E%90%E5%B0%88%E9%A1%8Chw1.pdf) for the original process and examples.
4. Explore the saved model and prediction files as artifacts of the completed coursework.

**Reproducibility note:** The repository does not include the original training dataset, and the Live Script may depend on local file paths or environment settings from the coursework. It is provided as a reference implementation, **not a guaranteed one-click reproduction package**.

## Data, Attribution, and Scope

This is an educational project inspired by the **HuBMAP Hacking the Human Vasculature** segmentation task. The original dataset is **not redistributed** here; please obtain data from its original source and follow the applicable terms.

The work is separate from my later [Acute Appendicitis CT / 2D U-Net project](https://github.com/Wendylin0112/AOCR2024-AI-Challenge).

**Author:** [Wei-Chen Lin](https://github.com/Wendylin0112) · [Portfolio](https://github.com/Wendylin0112/Wendylin0112)
