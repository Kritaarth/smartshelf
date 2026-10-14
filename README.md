# 📦 SmartShelf AI: Real-Time Retail Shelf Inventory Scanner

An automated, edge-optimized computer vision platform designed to modernize inventory tracking for small to medium-sized retail enterprises (SMEs). SmartShelf AI analyzes store shelf images in real-time to detect product bounding boxes, map spatial coordinates, and instantly flag stockouts—eliminating the need for manual, error-prone auditing.

Developed as a Final Year Minor Project aligned with the **V.E.T.S. Framework** (Viability, Engineering Depth, Trend Alignment, and Social/Industrial Impact).

---

## 🚀 Key Features

* **Real-Time Object Detection:** Utilizes a custom-trained YOLOv8 architecture to identify densely packed retail products.
* **Automated Stockout Alerts:** Cross-references detected bounding boxes with coordinate-based planogram logic to trigger immediate restock warnings for empty spatial gaps.
* **Edge-Optimized Inference:** Employs INT8 post-training quantization and ONNX runtime export to ensure low-latency performance on standard retail hardware (CPUs/tablets) without requiring cloud GPUs.
* **Decoupled Microservice Architecture:** Separates the machine learning inference engine (FastAPI) from the user operations dashboard (Streamlit) for high scalability.

---

## 🧠 System Architecture

The project is built on a 4-tier decoupled architecture:

1. **Computer Vision Engine:** Custom YOLOv8 model trained on the SKU-110K dataset and empty-shelf imagery, heavily augmented to handle varied store lighting and wide-angle perspectives.
2. **Edge Optimization Module:** PyTorch weights converted to ONNX and quantized to INT8 to reduce the model footprint by 60%+ for local deployment.
3. **REST API Gateway (FastAPI):** Ingests uploaded imagery, processes matrix arrays via OpenCV/NumPy, runs inference, and returns JSON-formatted analytical payloads.
4. **Operations Dashboard (Streamlit):** An interactive, browser-based UI where store staff upload photos, view rendered bounding boxes, and monitor floor analytics.

---

## 🛠️ Tech Stack

* **Machine Learning:** PyTorch, Ultralytics (YOLOv8), ONNX Runtime
* **Computer Vision:** OpenCV, NumPy
* **Backend Server:** FastAPI, Uvicorn, Python-Multipart
* **Frontend UI:** Streamlit, Requests, Pillow (PIL)

---

## ⚙️ Installation & Setup

### 1. Clone the Repository & Environment Setup

```bash
git clone https://github.com/your-username/smartshelf-ai.git
cd smartshelf-ai

# Create and activate a virtual environment
python -m venv retail_env
# Windows: retail_env\Scripts\activate
# Mac/Linux: source retail_env/bin/activate

```

### 2. Install Dependencies

```bash
pip install -r requirements.txt

```

*(Ensure `requirements.txt` includes: fastapi, uvicorn, python-multipart, streamlit, requests, ultralytics, opencv-python-headless, numpy)*

### 3. Launch the Backend API (FastAPI)

Open your first terminal window, activate the environment, and start the inference server:

```bash
python -m uvicorn backend.main:app --reload

```

*The API will be available at `[http://127.0.0.1:8000](http://127.0.0.1:8000)`. You can view the Swagger UI documentation at `[http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)`.*

### 4. Launch the Operations Dashboard (Streamlit)

Open a **second** terminal window, activate the environment, and start the frontend UI:

```bash
python -m streamlit run dashboard/app.py

```

*The dashboard will automatically open in your default web browser.*

---

## 👥 Team Members & Contributions

This project was developed by a 4-member team, with modular responsibilities:

* **Member 1 (CV & Data Engineer):** Dataset curation (SKU-110K), annotation, CIoU occlusion tuning, and custom YOLOv8 model training.
* **Member 2 (Edge Inference Engineer):** Model optimization, ONNX conversion, and INT8 quantization for low-latency CPU processing.
* **Member 3 (Backend Architect):** FastAPI REST endpoints, JSON payload structuring, and Planogram coordinate mapping logic.
* **Member 4 (Frontend UI Engineer):** Streamlit web application, API request handling, and real-time visual analytics rendering.

---

## 📜 License

Distributed under the MIT License. See `LICENSE` for more information.
