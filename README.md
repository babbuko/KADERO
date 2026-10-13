# KADERO
Real-time PPE compliance detection and worker tracking using custom PyTorch CNN and OpenCV.
# KADERO: Kinetic Automated Detection of Equipment in Real-time Operations

**Author:** Kamron Robinson  
**Institution:** Houston Community College  
**Course:** ITAI 1378 Computer Vision and AI  
**Tier Level:** Tier 2 (Custom PyTorch Object Detection + Multi-Object Tracking)

---

## 📌 Project Overview
KADERO is a real-time computer vision monitoring application engineered to detect Personal Protective Equipment (PPE) compliance on industrial and construction sites. The system pairs a custom-designed PyTorch convolutional detector with a multi-object tracking module to identify workers, verify required safety gear (such as hard hats, safety vests, masks, and gloves), and monitor compliance over time across live camera feeds and uploaded imagery.

---

## 🏗️ Architecture & Technical Approach
KADERO operates as a multi-component pipeline:
1. **Input Handling:** OpenCV (`cv2`) handles frame-by-frame capture from a live webcam feed or image uploads.
2. **Detection Network:** A custom Deep Convolutional Neural Network (CNN) built from scratch in pure PyTorch (`torch.nn`), featuring dual output heads:
   - Coordinate regression head predicting bounding boxes $[x, y, w, h]$.
   - Classification head outputting class logits.
3. **Tracking Module:** Multi-object tracking (benchmarking Centroid Tracking and ByteTrack) to maintain continuous tracking IDs for individual workers across consecutive video frames.
4. **Safety Rule Engine:** Flags workers missing mandatory gear and logs safety compliance status.

---

## 📊 Dataset & Target Classes
* **Source:** Roboflow Workspace (`w211444371-student-hccs-edu`)
* **Total Volume:** 2,750 pre-annotated images
* **Classes (5 Categories):**
  1. `Hardhat`
  2. `Safety Vest`
  3. `Mask`
  4. `Gloves`
  5. `NO-Gloves` (direct non-compliance tracking)
* **Pipeline Integration:** Automated retrieval into Google Colab and local training pipelines via the Roboflow SDK, feeding into custom PyTorch `DataLoader` batches with coordinate normalization and data augmentation.

---

## 🎯 Target Success Metrics
* **Primary Metric (Detection Accuracy):** $\ge 75\%$ Mean Average Precision ($\text{mAP}@0.50$) on the validation/test splits.
* **Secondary Metric (Inference Speed):** $20\text{–}30\text{ FPS}$ on real-time live webcam video ($\le 50\text{ ms}$ latency per frame).
* **Image Upload Latency:** $\le 1.0\text{ second}$ per evaluated static image.

---

## 🗓️ 16-Week Milestone Plan

| Week | Phase | Milestone | Deliverable |
| :--- | :--- | :--- | :--- |
| **Week 10** | 🧭 Blueprint | Midterm Submission | Architecture blueprint, repository setup, slide deck |
| **Week 12** | 🔌 First Working Demo | Pipeline Prototype | Custom PyTorch model structure defined; forward pass verified |
| **Week 13** | 🛠 Make It Yours | Training & Integration | Model trained on Roboflow data; live OpenCV video + tracker integrated |
| **Week 14** | 📈 Improve & Measure | Evaluation & Tuning | Benchmark test mAP@0.50, measure FPS, refine tracking stability |
| **Week 15** | 🎥 Package & Present | Final Delivery | 3–5 minute video demonstration, finalized codebase, and documentation |

---

## ⚠️ Risk Management & Plan B

| Identified Risk | Impact | Contingency Plan (Plan B) |
| :--- | :--- | :--- |
| **Data Quality Issues** | Mismatched or noisy annotations degrading model training | Fall back to an alternative verified PPE dataset on Roboflow Universe |
| **Local Conversion Errors** | File structure mismatch between local drives and PyTorch loaders | Ingest and download the dataset directly into Google Colab via Roboflow API |
| **Tracking / Zone Logic Complexity** | Complex spatial boundary zones overloading pipeline | De-scope virtual boundary zones and focus strictly on worker ID tracking |

---

## 💻 Tech Stack & Cost
* **Frameworks & Libraries:** PyTorch, Torchvision, OpenCV, NumPy
* **Data & Version Control:** Roboflow, Git, GitHub
* **Compute:** Google Colab (Free T4 GPU), Local Laptop
* **Budget:** **$0.00 (100% Free Tier)**
