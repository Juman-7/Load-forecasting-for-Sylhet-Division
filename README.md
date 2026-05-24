# ⚡ Website-Integrated Hardware Implementation of LSTM-Based Short-Term Load Forecasting Model
## A Case Study for Sylhet Division, Bangladesh

<p align="center">
  <img src="LFSC/figures/model_workflow.png" width="750">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.8+-blue.svg">
  <img src="https://img.shields.io/badge/TensorFlow-LSTM-orange.svg">
  <img src="https://img.shields.io/badge/License-MIT-green.svg">
  <img src="https://img.shields.io/badge/Conference-QPAIN2026-red.svg">
</p>

---

# 📌 Overview

This project presents a **website-integrated hardware implementation of an LSTM-based short-term load forecasting system** for the Sylhet Division power grid in Bangladesh.

It combines:

- 📊 LSTM-based deep learning for load forecasting  
- 🌡️ Environmental feature integration (temperature, humidity, etc.)  
- 📡 IoT-based real-time data acquisition using ESP32  
- 🔌 LoRa communication for data transmission  
- 🌐 Web-based dashboard for visualization and monitoring  

The system is designed for smart grid applications to improve forecasting accuracy and grid stability.

---

# 🚀 Key Features

- Hourly and daily load forecasting using LSTM
- Dual-model architecture (short-term + long-term)
- Separate scalers for each forecasting horizon
- ESP32 + DHT11 + LoRa-based hardware system
- Real-time prediction pipeline
- Web-integrated visualization system

---

# 📂 Project Structure

```text
LFSC/
│
├── Dataset/
│   ├── 1 hour data/
│   └── hourly data/
│
├── figures/
│   ├── Data_pre_processing.png
│   ├── Hardware.png
│   ├── model_workflow.png
│   └── result.png
│
├── models/
│   ├── lstm_model_hourly.h5
│   ├── lstm_model_daily.h5
│   ├── scaler_hourly.pkl
│   └── scaler_daily.pkl
│
├── LSTM model/
│   ├── 1 day lstm model.ipynb
│   ├── 1 hour lstm model.ipynb
│
│
├── requirements.txt
└── README.md
```

---

# 🔧 Installation & Setup

## Prerequisites

- Python 3.8+
- Arduino IDE
- CUDA-compatible GPU (recommended)

---

## 1. Clone Repository

```bash
git clone https://github.com/Juman-7/Load-forecasting-for-Sylhet-Division.git
cd Load-forecasting-for-Sylhet-Division/LFSC
```

---

## 2. Create Virtual Environment

### Windows
```bash
python -m venv venv
venv\Scripts\activate
```

### Linux / macOS
```bash
python -m venv venv
source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# 🔌 Hardware Setup

## Components Required

- ESP32 Development Board  
- DHT11 Temperature & Humidity Sensor  
- LoRa SX1278 Module  
- Breadboard + Jumper Wires  
- 5V Power Supply  

---

## Hardware Diagram

<p align="center">
  <img src="LFSC/figures/Hardware.png" width="700">
</p>

---

## Flash Firmware

1. Open Arduino IDE  
2. Load ESP32 firmware  
3. Select board: **ESP32 Dev Module**  
4. Upload code  

---

# 🧠 Model Usage

## 📈 Hourly Forecasting Model

```python
import tensorflow as tf
import joblib
from predict import load_model_and_predict

model_hourly = tf.keras.models.load_model("models/lstm_model_hourly.h5")
scaler_hourly = joblib.load("models/scaler_hourly.pkl")

forecast_hourly = load_model_and_predict(
    model_path="models/lstm_model_hourly.h5",
    scaler=scaler_hourly,
    current_data=sensor_readings,
    steps_ahead=24
)

print("Hourly Forecast:", forecast_hourly)
```

---

## 📉 Daily Forecasting Model

```python
model_daily = tf.keras.models.load_model("models/lstm_model_daily.h5")
scaler_daily = joblib.load("models/scaler_daily.pkl")

forecast_daily = load_model_and_predict(
    model_path="models/lstm_model_daily.h5",
    scaler=scaler_daily,
    current_data=sensor_readings,
    steps_ahead=7
)

print("Daily Forecast:", forecast_daily)
```

---


# 📊 Dataset Information

## Historical Load Data

- Source: Bangladesh Power Development Board (BPDB)
- Duration: 2018–2023
- Resolution: Hourly
- Region: Sylhet Division

## Environmental Data

- Source: NASA POWER Project
- Parameters: Temperature, humidity, solar radiation
- Resolution: Hourly (0.5° grid)

---

# 📈 Results

<p align="center">
  <img src="LFSC/figures/result.png" width="750">
</p>

## Performance Summary

| Model Type | MAE (MW) | MAPE |
|------------|----------|------|
| Hourly LSTM | 18.47 | 5.35% |
| Daily LSTM | 27.48 | 7.78% |

---

# 🔬 Key Findings

- LSTM captures seasonal and daily load patterns effectively
- Environmental variables improve forecasting accuracy
- Dual scaler approach improves stability
- Hardware integration enables real-time prediction

---

# 🧩 Dependencies

| Package | Version |
|---------|--------|
| Python | 3.8+ |
| TensorFlow | 2.x |
| NumPy | Latest |
| Pandas | Latest |
| Scikit-learn | Latest |
| Matplotlib | Latest |

---

# 🔁 Reproducibility

```python
import tensorflow as tf
import numpy as np
import random

tf.random.set_seed(42)
np.random.seed(42)
random.seed(42)
```

---
# 👨‍💻 Authors

**Md. Omar Faruk Sagor¹, Saydul Islam², Md. Shahid Iqbal³, Juman Das⁴, Jahid Hasan⁵, Mrinal Sahajee⁶**

---

## 📍 Affiliations

¹,²,⁴,⁵,⁶ Department of Electrical & Electronic Engineering  
Sylhet Engineering College, Sylhet, Bangladesh  

³ Department of Electrical & Electronic Engineering  
Mymensingh Engineering College, Mymensingh, Bangladesh  

---

## 📧 Emails

¹ faruksaagoreee02@gmail.com  
² saydul@sec.ac.bd  
³ iqbal@mec.ac.bd  
⁴ jumandas278@gmail.com  
⁵ adnanjahid420@gmail.com  
⁶ mrinal098sh@gmail.com  

---

## ⭐ Contribution Highlight

**Machine Learning / Deep Learning Lead (Primary Contributor):**  
👉 Juman Das

- Designed and implemented the LSTM-based forecasting models  
- Developed hourly and daily prediction pipelines  
- Built preprocessing and scaling pipeline (scaler_hourly & scaler_daily)  
- Integrated ML model with IoT + web system  
- Conducted evaluation and performance optimization  

---
# 🎓 Citation

@inproceedings{qpain2026lstm,
  title={Website-Integrated Hardware Implementation of LSTM-Based Short-Term Load Forecasting Model: A Case Study for Sylhet Division},
  author={Sagor, Md. Omar Faruk and Islam, Saydul and Iqbal, Md. Shahid and Das, Juman and Hasan, Jahid and Sahajee, Mrinal},
  booktitle={Proceedings of the 2nd IEEE International Conference on Quantum Photonics, Artificial Intelligence, and Networking (QPAIN)},
  year={2026},
  note={Presented at QPAIN 2026 (to be published in IEEE Xplore)},
  address={Chattogram, Bangladesh}
}

---

# 🤝 Contributing

1. Fork repository  
2. Create feature branch  
3. Commit changes  
4. Push branch  
5. Open Pull Request  

---

# 🛣️ Roadmap

- Multi-region forecasting  
- Mobile app integration  
- SCADA system integration  
- Edge AI deployment  
- Real-time alert system  

---

# 📄 License

MIT License

---

# ⭐ Support

If you like this project, please give it a ⭐ on GitHub.
