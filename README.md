# Gender and Age Classification using CNN and DCNN

This project implements a series of Convolutional Neural Networks (CNNs) and Deformable CNNs (DCNNs) to classify gender and age based on facial images. The models are built using PyTorch and are evaluated based on test accuracy.

## 📦 Models

### 1. Model 1: Gender-Only CNN

A simple CNN that classifies gender (Male/Female) based on facial features.

- **Architecture**: 3 Convolutional Layers → 2 Fully Connected Layers → 1 Sigmoid Output Neuron
- **Loss Function**: Binary Cross Entropy
- **Activation**: Sigmoid
- **Dropout**: 0.2 on both FC layers
- **Test Accuracy**: **0.77**
- **Prediction Rule**: Output > 0.5 → Male; otherwise → Female

---

### 2. Model 2: Gender and Age CNN

An extension of Model 1 to perform **multi-task classification** (gender and age group).

- **Architecture**: Shared CNN Backbone → Two Output Heads:
  - **Gender Head**: 1 neuron (Sigmoid, BCE Loss)
  - **Age Head**: 8 neurons (Softmax, Cross Entropy Loss)
- **Loss Function**: Combined sum of gender and age losses
- **Test Accuracy**: **0.76**

---

### 3. Model 3: Gender and Age DCNN

A more advanced model replacing all standard convolutional layers with **Deformable Convolutions** to handle geometric variation.

- **Motivation**: Better feature extraction from real-world face images with scale and shape variability
- **Architecture**: Same as Model 2 but with deformable convolutional layers
- **Loss Function**: Combined gender + age loss (same as Model 2)
- **Test Accuracy**: **0.79**

---

## 📊 Results Summary

| Model         | Gender Accuracy | Age Prediction | Notes                             |
|---------------|------------------|----------------|-----------------------------------|
| Model 1 (CNN) | 0.77             | -              | Binary gender classification only |
| Model 2 (CNN) | 0.76             | Yes            | Joint learning of gender + age    |
| Model 3 (DCNN)| **0.79**         | Yes            | Best performance                  |
| Model 3 + Aug | 0.74             | Yes            | Augmentation degrades accuracy    |

---

# Model Discussion

## 🔄 Model 1 vs Model 2

- **Goal**: Model 2 explores the capacity of convolutional layers to extract both age and gender characteristics.
- **Test Accuracy**:
  - Model 1: 0.77  
  - Model 2: 0.76
- **Conclusion**: 
  - Minimal performance drop with added complexity.
  - Feasible to combine age and gender classification in a single model.
  - Highlights convolutional layers' generalization ability across tasks.

## 🔁 Model 2 vs Model 3

- **Enhancement**: Model 3 introduces *deformable convolutional layers (DCNN)* to address limitations of fixed-grid CNNs.
- **Mechanism**: 
  - DCNNs learn flexible sampling positions with 2D offsets.
  - Better at capturing varying object sizes and positions.
- **Test Accuracy**:
  - Model 2: 0.76  
  - Model 3: 0.79
- **Conclusion**: 
  - 3% improvement shows deformable convolutions improve adaptability to geometric variations in face images.

## 🔄 Effect of Data Augmentation on Model 3

- **Without Augmentation**: Accuracy = 0.79  
- **With Augmentation**: Accuracy = 0.74
- **Augmentation Used**: Random cropping, flipping, and rotations (up to 10°)
- **Insights**:
  - Augmentation may introduce noise or redundancy if DCNN already captures variation.
  - Shows that data augmentation is not always beneficial—careful tuning is necessary.

## 📊 Performance on IMDB-WIKI Dataset

- **Accuracy**:
  - Model 2: 0.78  
  - Model 3: 0.80
- **Observations**:
  - Dataset presents large variation in face sizes.
  - DCNNs perform better by adapting to scale and position variability.
  

## ✅ Conclusion

- **Model 3** (DCNN) is the most effective in capturing real-world variability in faces.
- Deformable convolutions outperform traditional CNNs and data augmentation in this task.
- Joint learning of gender and age improves performance and enables multi-task inference.
- Confirms hypothesis that deformable convolutions are more robust to real-world data diversity.

