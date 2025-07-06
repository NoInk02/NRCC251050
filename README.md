# Cloud and Shadow Segmentation using Deep Learning

This project implements a two-stage deep learning pipeline to segment **clouds** and **shadows** from satellite imagery using TOA reflectance and metadata. The models are trained on LISS-IV data.

---

## 📂 Project Structure

├── inference_code.ipynb                 # Main inference pipeline  
├── Requirements.txt                     # List of required dependencies  
├── Training_Files/                      # Cloud mask labeling and training scripts for ResUNet and U-Net  
├── masks/                               # Predicted cloud and shadow masks on test dataset  
├── Report.pdf                           # Detailed methodology, model architecture, and analysis  
├── NRCC251050_Inference_Training_Results.csv  # Training log (loss, accuracy, IoU, etc.)  
├── Earth_Sun_Distance.xlsx              # Earth-Sun distance values for TOA reflectance computation  
└── Training_labeled_data/               # Training dataset (input patches and masks)  

---

## 🧠 Models Used

| Task              | Model         | Input Channels                        | Output Classes |
|-------------------|---------------|----------------------------------------|----------------|
| Cloud Segmentation | ResUNet (ResNet34 encoder) | TOA Bands (B2, B3, B4)                | 2 (Clear, Cloud) |
| Shadow Segmentation | Custom U-Net | TOA Bands + Cloud Mask + Sun Elevation | 2 (Clear, Shadow) |

### 📥 Download Trained Models

You can download the trained models (ResUNet for cloud segmentation and U-Net for shadow segmentation) from the link below:

🔗 [Download Trained Models from Google Drive](https://drive.google.com/drive/folders/1xBxLID2WZCi-sdtOShIQH45Kh4kw8s-X?usp=sharing])

---

## 🛠️ Requirements

Create a new python environment(python=3.10). Navigate to the downloaded folder where requirements.txt is present.

Install dependencies using:

```bash
pip install -r requirements.txt

```
## 🚀 Inference Guide

1. Place your test folder containing B2, B3, B4 bands and metadata file.
2. Update paths inside `inference_code.ipynb`:
   - Band paths (e.g., B2.tif, B3.tif, B4.tif)
   - Metadata text file path
   - Cloud model path (`.pth`)
   - Shadow model path (`.pth`)
3. Run all cells in the notebook to get:
   - Georeferenced mask.tif with values:  
     `0 = clear`, `1 = cloud`, `2 = shadow`
   - Optional: cloud and shadow shapefiles
