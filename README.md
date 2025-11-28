# Cancer Detection using CNNs

DL assignment for binary classification of histopathologic cancer images using CNN.

**Course:** Deep Learning Intro 
**Assignment:** Week 3 CNN Project

---

## Overview

**Competition:** [Kaggle - Histopathologic Cancer Detection](https://www.kaggle.com/c/histopathologic-cancer-detection)

**Objective:** Build CNN models to identify cancer in small pathology image patches (96×96 pixels)

**Kaggle Evaluation Metric:** AUC-ROC (Area Under the ROC Curve)

**Dataset:**
- Training: 220,025 labeled images
- Test: 57,458 images
- Image size: 96×96×3 (RGB)
- Classes: Binary (0 = No Cancer, 1 = Cancer)

---

## In-depth EDA

### Class Distribution

*Dataset contains 59.5% no-cancer and 40.5% cancer images (imbalance ratio: 1.47:1)*

**Key Findings:**
- No Cancer: 130,908 images (59.5%)
- Cancer: 89,117 images (40.5%)
- Manageable imbalance handled with class weights

### Sample Images

*Visual comparison of cancer vs non-cancer tissue samples*

**Observations:**
- Cancer tissue: Dense purple-stained cellular regions
- Non-cancer tissue: More uniform pink/light purple background, less concentrated cells
- High within-class variation requires robust feature extraction

## Model Architectures

### Three CNN Models Compared

**1. Baseline CNN**
- 3 convolutional blocks (single conv layer each)
- Minimal regularization 
- Simple architecture for baseline comparison

**2. Regularized CNN**
- 3 convolutional blocks
- BatchNormalization after each layer
- Dropout after each block (0.25) and dense layer (0.5)
- Larger dense layer (512 units)

**3. Deep CNN** 
- Two convolutional layers per block for hierarchical feature learning
- GlobalAveragePooling2D reduces parameters (prevents overfitting)
- Strategic dropout placement throughout network

## Results

### Model Comparison

*Performance comparison across three CNN architectures*

Baseline CNN | 85.65% | 0.9342 | Good baseline 
Regularized CNN | 80.78% | 0.9268 | Heavy regularization 
**Deep CNN** | **86.92%** | **0.9439** | **Best Model** 

### Deep CNN performance

*Confusion matrix showing classification performance on validation set*

**Confusion Matrix Analysis:**
- Overall Accuracy: 86.80%
- True Positives: High cancer detection rate
- Low false negative rate: Critical for medical screening

*Precision, recall, and F1-scores for both classes*

**Classification Metrics:**

No Cancer | 0.93 | 0.84 | 0.88 | 3,497 
Cancer | 0.80 | 0.91 | 0.85 | 2,503 
**Accuracy** | - | - | **0.87** | **6,000** 
**Weighted Avg** | 0.88 | 0.87 | 0.87 | 6,000 

**Insights:**
- **High cancer recall (91%):** Catches 91% of cancer cases 
- **High no-cancer precision (93%):** 93% confidence when predicting no cancer
- **Low false negative rate:** Only 9% of cancers missed
- Appropriate bias for medical screening (prioritizes catching cancer over false alarms)

## Computational Challenges

**Training Complexity:**
- Training time: 30-60 minutes per model (M-series Mac GPU)
- Full dataset: 220,025 images (13+ GB uncompressed)

**References:**
- Goodfellow, I., Bengio, Y., & Courville, A. (2016). *Deep Learning*. MIT Press. Chapter 9: Convolutional Networks
- Course CNN Module (Week 3)

## Lessons Learned

**Technical Insights:**
- High AUC doesn't guarantee high accuracy at default threshold (0.5)
- Medical imaging benefits from strong data augmentation
- GlobalAveragePooling superior to Flatten for image classification
- Class weights effectively handle moderate class imbalance

**Practical Lessons:**
- Computational budgets constrain experimentation in real-world ML
- Local training offers memory persistence advantages over cloud notebooks
- Honest reporting of limitations strengthens analysis
- Iterative model improvement demonstrates ML engineering skills
- Proper generator handling critical for aligned predictions

## Contact

**Author:** Philipp Adrian  
**Course:** Intro to Deep Learning 
**Date:** November 2024  
