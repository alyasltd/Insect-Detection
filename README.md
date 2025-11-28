# 🪱 Springtail Identification — AI Challenge  
_Source: Purple Modern Minimalist Business Development Presentation.pdf_

## 1. Project Overview
This project focuses on automatic identification of springtails using deep learning.

**Main objectives:**
- Provide labeling for test image patches
- Evaluate performance on Kaggle using **F1-macro**
- Propose label correction for uncertain samples
- Provide **model explainability**

---

## 2. Dataset

### Data separation
- Split into **certain** and **uncertain** datasets  
- Created crop datasets using **YOLO-based annotations**

### Construction of Class 8 (“background”)
- Number of background images proportional to class distribution  
- Maximum **8% overlap** allowed with other crops  
- Approximately **145 images** total

### Correction of uncertain labels
Each image receives a label of type `x_x_x_x_x` (5 votes):

- The **most frequent label** is selected as the prediction  
- If a tie occurs, choose the label that has historically appeared most often  

**Example:**  
`8_8_2_2_1` → **final label = 8**

---

## 3. Baseline Models

### **ResNet50**
- Activation: Softmax  
- Loss: Sparse Categorical Cross-Entropy  
- Score: **0.35347**

### **EfficientNet-B3**
- Activation: Linear  
- Loss: Weighted Cross-Entropy  
- Score: **0.53668**

---

## 4. Exploratory Analysis

### Class imbalance & dataset mismatch
- Strong **class imbalance** observed
- Potential **mismatch** between classes and projects

### Project separability
- Visualizations (t-SNE, HSV) show that **projects differ significantly**
- Suggests the model may overfit on **project-specific artifacts**  
  (background noise, resolution, microscopy setup, textures)

---

## 5. Advanced Approaches

# Vision Transformer (ViT)
**Training characteristics:**
- Input size: **512×512**
- Embedding dimension: **768**
- Patch size: **32**
- **6 attention blocks**
- Loss: Sparse Categorical Cross-Entropy

---

# StarGAN — Domain-Invariant Representation Learning

### Goal
Learn a **project-invariant latent space** so that images are encoded only by their **biological identity (class 0–8)**.

### Training adaptations
- Identity loss prevents excessive deformation:  
  `G(x, c_org) ≈ x_real`
- Data augmentations: flips, rotations, color jitter, resized crops  
- Inputs converted to **grayscale**
- 80/20 train–test split for downstream model evaluation

---

## 6. StarGAN Experiments

### Training on 9 classes
**Problem:**  
- The GAN unintentionally encodes project information  
- Latent space becomes polluted  
- Leads to **poor generalization**

**Cause:**  
Images from the same project share strong visual patterns not related to the biological class.

**Solution:**  
Explicitly **condition the model on the project**, forcing it to disentangle "context" and "class".

**Result:**  
- XGBoost trained on latent space  
- Accuracy ≈ **30%**

---

### Training on 32 classes
**Goal:**  
- Enforce project invariance  
- The GAN encodes only biological identity  
- t-SNE plots show mixed project clusters

**Method:**  
- Train the GAN to be **sensitive only to project**  
- Add Kaggle test set as its own project

**Result:**  
- XGBoost on latent space achieves  
  **Accuracy ≈ 44%**

---

## 7. Explainability

### Grad-CAM on discriminator activations  
### CRAFT method for concept attribution  

**Process:**
- Extract random crops  
- Pass them through the generator: compute strongest activations  
- Perturb activations and measure changes in prediction  
- Identify **important visual concepts** (via Sobol indices)

---

## 8. Conclusion & Future Work

### Conclusion
- No competitive success on Kaggle  
- StarGAN produced promising disentanglement and explainability results

### Future improvements
- Train ViT for more epochs  
- Test more downstream model configurations post-GAN  
- Improve CRAFT per class and build a library of human-defined concepts

---
