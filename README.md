# Enhanced Cervical Cancer Cell Detection Using CNN Transfer Learning with Strategic Layer Freezing

This repository accompanies the peer-reviewed paper “Enhanced Cervical Cancer Cell Detection Using CNN Transfer Learning with Strategic Layer Freezing”, accepted and presented at 2025 7th International Conference on Cybernetics and Intelligent System (ICORIS) and published on IEEE Xplore. The published version is available via IEEE:
https://ieeexplore.ieee.org/document/11295992

## Project Overview
- Task: 5-class single-cell cervical cytology classification (superficial–intermediate, parabasal, koilocytotic, dyskeratotic, metaplastic).  
- Dataset: SIPaKMeD, 4,049 expert-labeled single-cell images, split into train/validation/test with stratified sampling to preserve class balance.  
- Goal: Improve automated cervical cancer cell detection in limited-data, low-resource settings using modern CNN backbones and transfer learning.

## Methods
- Preprocessing:
  - Resize to 224×224 pixels  
  - Per-image standardization  
  - Data augmentation: random horizontal flips, brightness and contrast jitter to simulate staining and illumination variability  
- Architectures evaluated (ImageNet pretrained):
  - EfficientNetB0  
  - ConvNeXt Tiny  
  - ResNet50V2  
  - EfficientNetV2-Small  
- Training strategy:
  - Base models: frozen convolutional backbone + new classifier head (Dense + Dropout + softmax)  
  - Fine-tuned models: unfreeze selected deeper blocks while keeping early layers frozen (strategic layer freezing)  
  - Optimization: Adam, tuned learning rates and L2 regularization, early stopping based on validation performance  

## Key Results
- ConvNeXt Tiny shows the strongest **frozen** baseline, with F1-score around 0.84.  
- Fine-tuning improves all models, with **ResNet50V2** achieving the best overall performance:
  - F1-score ≈ 0.9154  
  - Accuracy ≈ 0.914  
  - Strong per-class AUC-ROC close to 1.0 for several classes  
- EfficientNetB0 and EfficientNetV2-Small also reach F1-scores around 0.89–0.90 after fine-tuning, confirming the benefit of strategic unfreezing.

## Takeaways
- Transfer learning combined with strategic layer freezing significantly boosts cervical cell classification performance on SIPaKMeD.  
- Architecture choice and how layers are frozen/unfrozen are crucial: some models transfer well with minimal tuning, while others (like ResNet50V2) benefit from deeper adaptation.  
- The approach provides a practical pathway for AI-assisted cervical cancer screening in data-scarce, low-resource environments.
