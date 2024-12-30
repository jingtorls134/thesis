# Stability Prediction of the Crystal Structures of Nickel-Based Compounds using Deep Learning

## Abstract  
Determining the stability of chemical compounds is essential for advancing material discovery. In this study, we introduce a novel deep neural network model designed to predict a crystal's **formation energy**. Our model leverages **elemental fractions** derived from material composition and incorporates the **space group** as an additional input feature. The materials' space group classifications represent the crystal polymorphs and are crucial for understanding phase transitions in materials. Our findings demonstrate that the integration of space group information significantly enhances the predictive performance of the developed deep learning architecture. Additionally, the same model architecture is used to predict the **energy above hull**, an indicator of material stability, with **formation energy** as an additional input feature.  

---

## Table of Contents  
- [Overview](#overview)  
- [Features](#features)  
- [Model Architecture](#model-architecture)  
- [Datasets](#datasets)   
- [Results](#results)  
- [Acknowledgments](#acknowledgments)  

---

## Overview  
This project presents a deep learning framework to predict two critical properties of crystal structures:  
1. **Formation Energy**  
2. **Energy Above Hull**  

By integrating elemental fractions and space group classifications, the model bridges material composition and structural data to enhance predictive accuracy for material stability.

---

## Features  
- Predicts formation energy based on chemical composition and space group data.  
- Predicts energy above hull using formation energy as an additional feature.  
- Supports exploratory analysis of material properties with high predictive performance.  

---

## Model Architecture  
The deep neural network model comprises **six sequential hidden layers**:  
1. **First and second layers**: 512 neurons each.  
2. **Third layer**: 256 neurons.  
3. **Fourth layer**: 128 neurons.  
4. **Fifth layer**: 64 neurons.  
5. **Sixth layer**: 32 neurons.  

### Activation Functions and Output  
- **Hidden layers**: ReLU activation function.  
- **Output layer**: Linear activation function, suitable for regression tasks (e.g., predicting formation energies).  

### Optimizer and Regularization  
- **Optimizer**: Adam optimizer, combining the advantages of AdaGrad and RMSProp for efficient training.  
- **Regularization**:  
  - Early stopping to prevent overfitting, with a patience of 10 epochs (waiting period for improvement).  
  - Training limit: 500 epochs.

### Loss Functions and Evaluation Metrics  
- **Loss functions**:  
  - Mean Absolute Error (MAE).  
  - Mean Squared Error (MSE).  
  - Root Mean Squared Error (RMSE).  
- **Performance Metric**: R-squared ($R^2$) to assess predictive confidence.  

---

## Datasets  
1. **Input Data**:  
   - Material composition (e.g., elemental fractions).  
   - Space group classification.  
2. **Target Data**:  
   - Formation energy (eV/atom).  
   - Energy above hull (eV/atom).  

Data was curated from Materials Project, Open Quantum Materials Database.  

---

## Key Results  

### Formation Energy Prediction  
1. **Using chemical formula only (with duplicates)**:  
   - **MAE**: 0.1479 eV/atom  
   - **MSE**: 0.1697 eV/atom  
   - **RMSE**: 0.4120 eV/atom  
   - **R²**: 0.8818  

2. **Using chemical formula only (without duplicates and outliers)**:  
   - **MAE**: 0.1357 eV/atom  
   - **MSE**: 0.1286 eV/atom  
   - **RMSE**: 0.3586 eV/atom  
   - **R²**: 0.9080  

3. **Using chemical formula and crystal system**:  
   - **MAE**: 0.1197 eV/atom  
   - **MSE**: 0.0672 eV/atom  
   - **RMSE**: 0.2592 eV/atom  
   - **R²**: 0.9536  

4. **Using chemical formula and point group**:  
   - **MAE**: 0.1085 eV/atom  
   - **MSE**: 0.0570 eV/atom  
   - **RMSE**: 0.2387 eV/atom  
   - **R²**: 0.9607  

5. **Using chemical formula and space group**:  
   - **MAE**: 0.1069 eV/atom  
   - **MSE**: 0.0419 eV/atom  
   - **RMSE**: 0.2046 eV/atom  
   - **R²**: 0.9709  

### Energy Above Hull Prediction  
Using the same deep learning architecture with **formation energy** as an additional input feature, we achieve:  
- **MAE**: 0.0311 eV/atom  
- **MSE**: 0.0046 eV/atom  
- **RMSE**: 0.0679 eV/atom  
- **R²**: 0.9722  

Compounds with zero or near-zero energy above the hull are predicted as stable or metastable, respectively.  

---

## Visual Results  

### Formation Energy Predictions  
- **True vs. Predicted Formation Energy Values**:  
  ![Formation Energy Scatter Plot](figures/pred_v_true_f_e.png)  

- **True vs. Predicted Formation Energy Values with Symmetry Information**:  
  ![Formation Energy with Symmetry](figures/pred_v_true_f_e_2x2.png)  

### Energy Above Hull Prediction  
- **True vs. Predicted Energy Above Hull Values**:  
  ![Energy Above Hull Scatter Plot](figures/pred_v_true_ehull.png)  

---


