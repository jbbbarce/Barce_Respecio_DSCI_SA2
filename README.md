# Barce_Respecio_DSCI_SA2

A Data Science project implementing and evaluating **YOLOv26n** for real-time pedestrian behavior detection. Three models were trained with distinct hyperparameter configurations and compared across overall and per-class performance metrics.

---

## 📁 Repository Contents

| File | Description |
|------|-------------|
| `Barce_Respecio_SA2.ipynb` | Main Jupyter Notebook — training, validation, and evaluation pipeline |
| `Barce_Respecio_SA2.pdf` | PDF export of the notebook with outputs and visualizations |
| `Barce_Respecio_SA2_Full Model Discussion.pdf` | Full written discussion comparing model results per class |

---

## 🎯 Objective

Detect and classify four pedestrian behaviors from street-level images using the YOLOv26n object detection architecture:

- `crossing` — pedestrian crossing at a designated crosswalk
- `jaywalking` — pedestrian crossing outside a designated area
- `pedestrian` — general pedestrian presence
- `waiting` — pedestrian waiting at a crossing point

---

## 🧪 Models Trained

| Model | Optimizer | Epochs | Batch Size | Learning Rate |
|-------|-----------|--------|------------|---------------|
| Model 1 | AdamW | 25 | 4 | 0.01 |
| Model 2 | SGD | 30 | 20 | 0.001 |
| Model 3 | Auto | 40 | Auto | 0.0001 |

All models were initialized from `yolo26n.pt` pretrained weights and trained at `imgsz=640`.

---

## 📊 Overall Validation Results

| Model | mAP50 | mAP50-95 | Precision | Recall | F1 Score |
|-------|-------|----------|-----------|--------|----------|
| Model 1 (AdamW) | 0.5430 | 0.3180 | 0.5000 | 0.6140 | 0.5510 |
| Model 2 (SGD) | 0.4340 | 0.2540 | 0.4080 | 0.5390 | 0.4660 |
| **Model 3 (Auto)** | **0.6980** | **0.4470** | **0.6750** | **0.6600** | **0.6670** |

> ✅ **Model 3** achieved the highest scores across all metrics.

---

## 🔍 Per-Class Highlights

| Class | Best Model | Best AP50 | Key Finding |
|-------|------------|-----------|-------------|
| Jaywalking | Model 3 | 0.905 | Strongest class across all models |
| Waiting | Model 3 | 0.699 | Moderate — confused with stationary pedestrians |
| Crossing | Model 3 | 0.735 | Improves significantly with longer training |
| **Pedestrian** | Model 3 | **0.453** | ⚠️ Most struggled class across all models |

The `pedestrian` class consistently underperformed due to semantic overlap with the other three behavioral classes — a stationary or moving pedestrian can visually resemble someone waiting, crossing, or jaywalking.

---

## 🛠️ Tech Stack

- **Python 3.12**
- **Ultralytics YOLOv8/YOLO26** (`ultralytics 8.4.18`)
- **PyTorch** (`torch 2.10.0 + CUDA`)
- **Google Colab** (Tesla T4 GPU)
- **Pandas**, **Matplotlib**, **NumPy**

---

## 🚀 How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/wish9-mu/Barce_Respecio_DSCI_SA2.git
   cd Barce_Respecio_DSCI_SA2
   ```

2. Open the notebook in Google Colab or Jupyter:
   ```bash
   jupyter notebook Barce_Respecio_SA2.ipynb
   ```

3. Ensure your dataset is structured as:
   ```
   dataset/
   ├── train/images/
   ├── valid/images/
   └── test/images/
   ```

4. Run all cells sequentially. Training results and weights will be saved to `runs/detect/`.

---

## 👥 Authors

- **Barce** 
- **Respecio**

*DSCI SA2 — Data Science Course Project*
