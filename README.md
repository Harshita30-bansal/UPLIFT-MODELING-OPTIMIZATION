# Uplift Modeling - Optimization: DragonNet (Hard) vs T-Learner (Easy)

This project implements and compares two uplift modeling approaches:

- Optimized DragonNet (Hard Problem)  
- Two-Model T-Learner using Random Forests (Easy Problem)

The goal is to estimate individual treatment effects (ITE) and evaluate which method performs better using AUUC and Qini metrics.

---

## Overview

Uplift modeling predicts how much a treatment (such as an ad or offer) changes user behavior.  
This project includes:

### DragonNet (Hard Model)
A deep neural architecture estimating:
- Y(1): potential outcome under treatment  
- Y(0): potential outcome under control  
- Propensity score P(T=1 | X)

Features of this implementation:
- Dense residual blocks  
- Batch normalization, GELU activations, dropout  
- Trainable epsilon layer  
- Targeted regularization (TARReg loss)  

### T-Learner (Easy Baseline)
Two separate RandomForestRegressor models:
- One trained on treated samples  
- One trained on control samples  

Uplift is computed as:

```
uplift = y1_pred - y0_pred
```

---

## Evaluation Metrics

### AUUC (Area Under the Uplift Curve)
Measures cumulative uplift gain as users are ranked by predicted uplift.

### Qini Coefficient
A more robust uplift evaluation metric adjusting for random treatment assignment.

The notebook generates uplift and Qini curves for both models.

---
