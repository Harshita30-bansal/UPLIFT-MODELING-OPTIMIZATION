###📈Uplift Modeling - Optimization: DragonNet (Hard) vs T-Learner (Easy)

This project implements and compares two uplift modeling approaches:

- Optimized DragonNet (Hard Problem)  
- Two-Model T-Learner using Random Forests (Easy Problem)

The goal is to estimate individual treatment effects (ITE) and evaluate which method performs better using AUUC and Qini metrics.

---

## 🚀Overview

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

## 📊Evaluation Metrics

### AUUC (Area Under the Uplift Curve)
Measures cumulative uplift gain as users are ranked by predicted uplift.

### Qini Coefficient
A more robust uplift evaluation metric adjusting for random treatment assignment.

The notebook generates uplift and Qini curves for both models.
<img width="1490" height="615" alt="image" src="https://github.com/user-attachments/assets/228a37fc-254a-451d-a20d-df71d22b28eb" />
#T-Learner Results (Easy Baseline)

The following figures show the Uplift Curve and Qini Curve obtained using the Two-Model T-Learner baseline. This method trains two separate Random Forest models—one on treated samples and one on control samples—and computes uplift as the difference in their predictions.

Uplift Curve (AUUC = 226.77)

The uplift curve (left plot) visualizes how much incremental uplift is captured as we target users in descending order of predicted uplift.

Qini Curve (Qini = 253.86)

The Qini curve (right plot) adjusts the uplift measurement to account for random treatment assignment and provides a more realistic assessment of model performance.

<img width="1484" height="611" alt="image" src="https://github.com/user-attachments/assets/0c9c18d9-c08c-4fb4-b4bf-f918bacf8f9c" />
#Optimized DragonNet Results (Hard Problem)

The figures below show the Uplift Curve and Qini Curve produced by the Optimized DragonNet model. This approach jointly learns potential outcomes, treatment propensity, and applies targeted regularization to stabilize counterfactual predictions.

Uplift Curve (AUUC = 301.67)

The uplift curve demonstrates how effectively the model ranks users by true incremental impact.
Qini Curve (Qini = 338.24)

The Qini curve provides a more robust uplift evaluation that adjusts for treatment allocation.

<img width="870" height="591" alt="image" src="https://github.com/user-attachments/assets/37c24712-117a-4c7b-8ba6-31adceed3905" />

Uplift Curve Comparison 

DragonNet captures far more incremental uplift than the T-Learner, shown by its consistently higher curve and sharper initial rise. The AUUC of 301.67 clearly outperforms the T-Learner’s 226.77, demonstrating a stronger ability to rank high-uplift users.

<img width="866" height="581" alt="image" src="https://github.com/user-attachments/assets/0c7f5900-eb07-471b-8eb4-0da674c5e307" />

Qini Curve Comparison

The DragonNet Qini curve stays well above the T-Learner curve across the full population, indicating better treatment effect estimation. With a Qini of 338.24 vs 253.86, DragonNet delivers significantly stronger uplift performance.



---
