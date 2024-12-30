# Stability Prediction of the Crystal Structures of Nickel-Based Compounds Using Deep Learning

## Abstract  
Determining the stability of chemical compounds is essential for advancing material discovery. In this study, we introduce a novel deep neural network model designed to predict a crystal's **formation energy**. The model leverages **elemental fractions** derived from material compositions and incorporates **space group** data as an additional feature. Space group classifications represent crystal polymorphs and are critical for understanding phase transitions in materials. Our findings demonstrate that the integration of space group information significantly enhances predictive performance. Furthermore, the same model architecture was applied to predict **energy above the hull**, an essential indicator of material stability, with **formation energy** included as an additional input feature.  

---

## Table of Contents  
- [Overview](#overview)  
- [Features](#features)  
- [Model Architecture](#model-architecture)  
- [Datasets](#datasets)
- [Results](#results)
- [Stability Prediction of Manganese-Nickel-Oxygen Chemical System](#stability-prediction-of-manganese-nickel-oxygen-chemical-system)  
- [Conclusion](#conclusion)  
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

## Results  

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
  ![Formation Energy Scatter Plot](figures/pred_v_true_f_e-eps-converted-to.pdf)  

- **True vs. Predicted Formation Energy Values with Symmetry Information**:  
  ![Formation Energy with Symmetry](figures/pred_v_true_f_e_2x2-eps-converted-to.pdf)  

### Energy Above Hull Prediction  
- **True vs. Predicted Energy Above Hull Values**:  
  ![Energy Above Hull Scatter Plot](figures/pred_v_true_ehull-eps-converted-to.pdf)  

---

## Stability Prediction of Manganese-Nickel-Oxygen Chemical System  
We now have two models: one that predicts formation energy and another that predicts energy above the hull. We systematically generated potential ternary compounds of the **Manganese-Nickel-Oxygen** chemical system, combining Manganese, Nickel, and Oxygen using the **itertools** library. By considering possible subscripts ranging from 1 to 8 for each element, we permuted and assigned these numbers to every conceivable combination to construct compounds. Subsequently, we assigned each generated compound to all possible space group symmetries, resulting in a total of **77,280 combinations**. We removed compounds assigned to space groups **168** and **207**, as these space groups do not exist in the Materials Project data, reducing the total to **76,608 entries**. However, the unique compounds numbered only **336**. Using **Pymatgen**, we converted the compounds into their chemical compositions and then featurized them into elemental fractions with **Matminer**.

Leveraging our developed model, we determined the most stable space group symmetry for each of the newly generated compounds from this meticulously curated dataset. Table 1 shows the top 5 materials predicted to be stable according to our model, along with their predicted formation energy and energy above hull values (in eV/atom), as well as their space group symmetries.

| Material              | Space Group | Predicted Formation Energy (eV/atom) | Predicted Energy Above Hull (eV/atom) |
|-----------------------|-------------|---------------------------------------|---------------------------------------|
| Mn<sub>2</sub>Ni<sub>3</sub>O               | 103         | -2.223632                             | 0.007018                              |
| Mn<sub>2</sub>Ni<sub>3</sub>O<sub>4</sub>              | 103         | -2.419526                             | 0.007018                              |
| Mn<sub>2</sub>Ni<sub>3</sub>O<sub>5</sub>              | 214         | -2.419526                             | 0.007018                              |
| Mn<sub>2</sub>Ni<sub>3</sub>O<sub>6</sub>              | 196         | -2.468194                             | 0.007018                              |
| Mn<sub>2</sub>Ni<sub>3</sub>O<sub>7</sub>              | 196         | -2.478734                             | 0.007018                              |

---

## Conclusion

This study utilized materials data from the Materials Project, processed using **matminer** for chemical formula representation and one-hot encoding for crystallographic symmetry. A deep neural network was trained in two configurations:  
1. Using only chemical formula input.  
2. Combining chemical formula with additional crystallographic symmetry features.  

The results demonstrate that incorporating symmetry information significantly improves model performance. Notably, as the detail in symmetry features increased—from **crystal system** to **point group** to **space group**—the predictive accuracy also improved, with **space group information yielding the best results**.

These findings underscore the importance of detailed structural descriptors, such as space group data, in effectively capturing material properties. Furthermore, the model was extended to predict **energy above the hull**, an essential metric for assessing material stability. By leveraging chemical and crystallographic data, the model not only enhanced the accuracy of formation energy predictions but also offered insights into the crystallographic symmetries of specific chemical compounds.

The generated chemical formulas from Mn, Ni, and O, created by combining these elements with subscripts permuted from integers 1 to 9, have the potential to form stable compounds with distinct space groups or geometrical arrangements of atoms. This hypothesis assumes that such stoichiometries may correspond to thermodynamically favorable configurations within the Mn-Ni-O compositional space.

To further validate the stability of the materials predicted by our model, it is strongly recommended to perform simulations using **Density Functional Theory (DFT)**. This approach provides a reliable method for confirming thermodynamic stability and verifying the model's predictions.

Additionally, efforts should be made to successfully perform **network dissection** on the deep learning model. While our initial attempt at network dissection was unsuccessful, refining this process could yield valuable insights into the internal representations learned by the model, thereby improving interpretability and transparency.

---

## Acknowledgments  
We appreciate stimulating discussions with H.~Aringa, V.~Convicto, and M.~Dengal. VT acknowledges the financial support through the scholarship granted by the Department of Science and Technology – STRAND.
