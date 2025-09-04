#  **Zero-Shot Defect Classification with CLIP**

This project applies **OpenAI’s CLIP model** for **zero-shot defect classification** on the **hazelnut subset of the MVTec-AD dataset**.  
The goal is to evaluate whether CLIP can distinguish between *good* and *defective* samples without additional training.  

---

## **Project Overview**
- **Dataset:** MVTec-AD (hazelnut, test split)  
- **Task:** Zero-shot classification of industrial defects  
- **Models used:**  
  - CLIP **ViT-B/32** (default)  
  - CLIP **ViT-B/16** (experiment)  
- **Defect categories:** `good`, `crack`, `cut`, `hole`, `print`  

---

##  **How It Works**
1. **Prompts Definition**  
   Example: `"A photo of a hazelnut with a crack"`  
   These serve as natural language class descriptions.  

2. **Text Encoding**  
   Prompts are tokenized and encoded using CLIP’s text encoder.  

3. **Image Encoding**  
   Test images are preprocessed and encoded with CLIP’s image encoder.  

4. **Similarity Matching**  
   - Cosine similarity is computed between image features and text features.  
   - The label of the most similar text prompt is chosen as the prediction.  

---

##  **Observations – Confusion Matrix**
- **Good** → misclassified as **Hole** in several cases.  
- **Hole** → misclassified as **Crack** frequently.  
- **Cut** → misclassified as **Print**.  
- **Print** achieved the strongest performance (most samples classified correctly).  

 This shows CLIP struggles with **subtle defect differences**, especially with a **small dataset size**.  

---

##  **Experimentation**
- **Model Variants**  
  - Started with **ViT-B/32**  
  - Tried **ViT-B/16** with shorter prompts → minimal accuracy improvement  

- **Prompt Engineering**  
  - Iteratively refined prompts (e.g., shorter, defect-specific phrasing)  
  - Did not fully resolve misclassification patterns  

- **Image Augmentation**  
  - Applied transformations (positional shifts, flips)  
  - Misclassifications still persisted  

---

##  **Conclusion**
CLIP provides a **strong zero-shot baseline**, but:  
- Misclassifications remain for **fine-grained industrial defects**  
- Performance is constrained by **small dataset size**  

**Improvements require:**  
- Larger datasets  
- Targeted fine-tuning  
- Complementary approaches beyond zero-shot prompting  
