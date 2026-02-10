# Scoping Document: A10 - Manufacturing Quality from Images

## 1️⃣ Problem Clarification
**Problem Statement:** The production line incurs high costs due to rare but expensive product defects. Currently, factory cameras capture images, but there is no reliable automated system to catch these defects because they occur inconsistently and lack proper labeling.

**Decision-Maker / End User:** The Quality Assurance (QA) Manager and the production line operators.

**Actionable Insight:** The system will trigger an immediate alert or stop the conveyor belt when a potential defect is detected, allowing for manual inspection before the product is shipped.

---

## 2️⃣ Problem Type Classification
**Problem Type:** **Unsupervised Learning (Anomaly Detection)**

**Justification:** Supervised learning requires thousands of labeled examples for each defect type. Since defects are rare and inconsistently labeled, we cannot train a standard classifier. Anomaly detection allows us to model "normal" products and flag anything that deviates from that norm as a potential defect.

---

## 3️⃣ Data Science Scope
**Available Data:** High-resolution images from factory cameras (existing infrastructure).

**Data Modality & Granularity:** * **Modality:** Image data (Computer Vision).
* **Granularity:** Image-level (one or more photos per unique product ID).

**Labels:** Clean labels do **not** exist. We have a vast amount of "unlabeled" data, which we assume is mostly "good" products.

**Key Data Risks (Ishikawa Factors):**
* **Machine (Camera):** Changes in lighting, vibration, or lens blur can be falsely flagged as defects.
* **Method:** Inconsistent positioning of the product on the belt.
* **Material:** Natural variations in raw materials that are NOT defects but look different.



---

## 4️⃣ Modeling Approach (High-Level)
**Proposed Approaches:**
1.  **Autoencoders (Neural Networks):** The model learns to compress and reconstruct images of "good" products. If a product has a defect, the reconstruction error will be high.
2.  **Isolation Forests or One-Class SVM:** These algorithms are specifically designed to find "outliers" in high-dimensional data (after extracting features from images).

**Inappropriate Approaches:** Standard Supervised CNN (Convolutional Neural Network) Classification. It would fail because the "Defect" class is too small (class imbalance) and labels are unreliable.

---

## 5️⃣ Use of LLMs (Reflection)
* **LLM Usage:** Used as a brainstorming partner to move from "Classification" to "Anomaly Detection" concepts.
* **Clarification Example:** The LLM helped explain how an Autoencoder can "detect" something it has never seen before by measuring reconstruction loss.
* **Refinement Example:** I challenged the LLM when it initially suggested a simple classifier, pointing out that we lack the labels for it.

---

## 6️⃣ Unknown Methods Discovery
**Technique:** **Self-Supervised Learning (SSL) for Feature Extraction.**
* **Relevance:** It allows the model to learn what a product looks like without needing any human labels.
* **In my own words:** The model "teaches itself" by looking at parts of the images and predicting other parts, creating a deep understanding of the product's shape and texture.
* **Initial Assumption:** I thought we needed at least a few hundred defect examples. I learned that with Anomaly Detection, we can start with almost zero defect labels.

# A3-SCOPING: MANUFACTURING QUALITY (A10)

## 1. BACKGROUND & PROBLEM
* **Context:** Production line cameras exist, but defect detection is manual/unreliable.
* **Pain Point:** Defects are rare but very costly. Leadership wants "AI" to reduce waste.
* **Gap:** We lack labeled "defect" images. Standard Supervised Learning won't work.

## 2. PROBLEM STATEMENT (Deliverable 1)
"Implement an automated visual inspection system to identify rare product defects. This system will alert QA managers to prevent costly faulty parts from shipping, even without a prior database of labeled defect examples."

## 3. DATA SCIENCE SCOPE (Deliverable 3)
* **Modality:** Images (Factory Cameras).
* **Granularity:** Item-level (individual products).
* **Status:** Labels do NOT exist.
* **Risks (Ishikawa):** * **Machine:** Fluctuating light/lens dust.
    * **Method:** Inconsistent item orientation on the belt.
    * **Material:** Non-defect surface variations.

## 4. PROBLEM CLASSIFICATION (Deliverable 2)
* **Type:** **Unsupervised Learning (Anomaly Detection).**
* **Justification:** Since defects are rare and unlabeled, we must model "normal" and flag everything else as an outlier.

## 5. PROPOSED APPROACH (Deliverable 4)
* **Approach A:** **Autoencoders.** Learn to reconstruct "good" images. High reconstruction error = Defect.
* **Approach B:** **One-Class SVM.** Draws a boundary around "normal" data in feature space.
* **Avoid:** Supervised CNNs (due to extreme class imbalance).

## 6. DISCOVERY & REFLECTION (Deliverables 5 & 6)
* **New Method:** **Self-Supervised Learning.** Using the model to predict rotated versions of "good" products to learn features without labels.
* **LLM Reflection:** LLM suggested a classifier first; I corrected it by emphasizing the lack of labels. This led to the "Anomaly Detection" strategy.
* **Key Insight:** I initially thought we needed a "Defect Library." Now I realize we only need a "Good Quality" baseline.


[A3-SCOPING REPORT: MANUFACTURING QUALITY (CASE A10)](./20260209_A3_Case%20A10%20Manufacturing%20Quality_SIA01.pdf)