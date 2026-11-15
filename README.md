# ☀️SolarVision - Rooftop Solar Panel Detection 

An end-to-end computer vision web application built with **YOLO11 Instance Segmentation** and **Gradio** to detect, outline, and count rooftop solar panels from satellite, aerial, and drone imagery—along with estimating surface area (m²) and potential kilowatt (kW) capacity.

## 🚀 Key Features
- **Instance Segmentation & Counting:** Accurately identifies individual solar panels and arrays even when angled on pitched roofs, outputting both exact counts and tight polygon masks.
- **Area & Power Estimation:** Converts detected polygon pixel masks into real-world surface area (m²) and estimated solar capacity (kW) using adjustable spatial resolution (meters/pixel).
- **Interactive Web Interface:** Built with Gradio for real-time image uploads, confidence threshold tuning, and visual inspection.

## 🛠️ Tech Stack
- **Model Architecture:** Ultralytics YOLO11 (`yolo11s-seg`)
- **Dataset:** Roboflow Universe (`solar-panels-seg`)
- **Frontend & Deployment:** Gradio & Hugging Face Spaces
- **Image Processing:** OpenCV, NumPy

## 📂 Project Structure
```text
├── app.py              # Gradio web application and inference pipeline
├── best.pt             # Trained YOLO11 instance segmentation weights
├── requirements.txt    # Python dependencies
└── README.md           # Project documentation
```

## 💻 Local Setup & Installation

1. **Clone the repository:**
   ```bash
   git clone https://github.com
   cd rooftop-solar-detector
   ```

2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the Gradio app:**
   ```bash
   python app.py
   ```
   Open the local URL shown in your terminal (typically `http://127.0.0.1:7860`).

## 🧠 Model Training Summary
The model was trained in Google Colab (T4 GPU) on aerial and drone rooftop imagery annotated with polygon masks:
- **Base Weights:** `yolo11s-seg.pt`
- **Image Size:** `640x640`
- **Epochs:** `40`
- **Batch Size:** `16`

## 📐 How Capacity is Estimated
1. **Pixel Area:** Counts total pixels inside all predicted solar panel polygon masks.
2. **Surface Area ($\text{m}^2$):** $\text{Total Pixels} \times (\text{Meters per Pixel})^2$
3. **Estimated Output ($\text{kW}$):** $\text{Surface Area} \times 0.20\text{ kW/m}^2$ *(assumes ~20% standard commercial/residential PV panel efficiency under standard test conditions)*.

## ⚠️ Limitations
- Capacity estimates are approximations and do not account for roof tilt angle, azimuth orientation, shading, or inverter losses.
- Very low-resolution satellite imagery ($> 0.5\text{ m/pixel}$) may merge closely spaced individual panels into a single array count.
