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

This project presents a website-integrated hardware implementation of an LSTM-based short-term load forecasting system designed for the Sylhet Division power grid in Bangladesh.

The proposed system combines:

- 📊 Deep learning based load forecasting using LSTM
- 🌡️ Environmental data integration
- 📡 IoT-based real-time data acquisition
- 🔌 ESP32 and LoRa hardware communication
- 🌐 Website/dashboard integration for monitoring and visualization

The system is designed to support modern smart-grid applications by enabling accurate short-term electricity demand forecasting for improved grid stability and energy management.

---

# 🚀 Key Features

- ✅ LSTM-based short-term load forecasting
- ✅ 1-hour and 24-hour ahead prediction
- ✅ ESP32 hardware implementation
- ✅ LoRa wireless communication
- ✅ Website-integrated monitoring system
- ✅ Environmental parameter integration
- ✅ Real-time forecasting capability
- ✅ Historical data preprocessing pipeline

---

# 📂 Project Structure

```text
LFSC/
│
├── Dataset/
│
├── figures/
│   ├── Data_pre_processing.png
│   ├── Hardware.png
│   ├── model_workflow.png
│   └── result.png
│
├── models/
│   └── lstm_model.h5
|   └── lstm_model_1.h5
|   └── lstm_1hour.h5
|   └── lstm_1hour.h5
│
├── LSTM model/
│   ├── train.py
│   ├── predict.py
│   └── evaluate.py
│
├── hardware/
│   └── ESP32_firmware/
│
├── requirements.txt
├── config.yaml
└── README.md
```

---

# 🔧 Installation & Setup

## Prerequisites

- Python 3.8 or higher
- Arduino IDE
- CUDA-compatible GPU (recommended)

---

## Software Setup

### 1. Clone Repository

```bash
git clone https://github.com/Juman-7/Load-forecasting-for-Sylhet-Division.git

cd Load-forecasting-for-Sylhet-Division/LFSC
```

---

### 2. Create Virtual Environment

#### Linux / macOS

```bash
python -m venv venv
source venv/bin/activate
```

#### Windows

```bash
python -m venv venv
venv\Scripts\activate
```

---

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

### 4. Configure Parameters

```bash
nano config.yaml
```

---

# 🔌 Hardware Setup

## Required Components

- ESP32 Development Board
- DHT11 Temperature & Humidity Sensor
- LoRa SX1278 Module
- Breadboard and Jumper Wires
- 5V Power Supply

---

## Hardware Diagram

<p align="center">
  <img src="LFSC/figures/Hardware.png" width="700">
</p>

Refer to the hardware diagram above for complete circuit connections.

---

## Flash ESP32 Firmware

1. Open Arduino IDE
2. Load ESP32 firmware code
3. Select board: `ESP32 Dev Module`
4. Upload firmware to ESP32

---

# 🧠 Model Workflow

<p align="center">
  <img src="LFSC/figures/model_workflow.png" width="750">
</p>

The workflow consists of:

1. Historical load data collection
2. Environmental data integration
3. Data preprocessing and normalization
4. LSTM model training
5. Real-time forecasting
6. Hardware-to-web integration

---

# 📖 Usage

## Training the Model

```python
import sys

sys.path.append('LSTM model')

from train import train_lstm_model

model_1h = train_lstm_model(
    data_path='Dataset/processed/hourly_load.csv',
    lookback=168,
    horizon=1,
    epochs=100,
    batch_size=32
)

model_1h.save('models/lstm_1hour.h5')
```

---

## Making Predictions

```python
from predict import load_model_and_predict

forecast = load_model_and_predict(
    model_path='models/lstm_1hour.h5',
    current_data=sensor_readings,
    steps_ahead=24
)

print(f"Next hour predicted load: {forecast[0]:.2f} MW")
```

---

## Running Evaluation

```python
from evaluate import evaluate_model

metrics = evaluate_model(
    model_path='models/lstm_1hour.h5',
    test_data='Dataset/processed/test_data.csv'
)

print(f"MAE: {metrics['mae']:.2f}")
print(f"MAPE: {metrics['mape']:.2f}%")
```

---

# 📊 Dataset Information

## Historical Load Data

| Property | Details |
|---|---|
| Source | Bangladesh Power Development Board (BPDB) |
| Duration | 2018 – 2023 |
| Resolution | Hourly |
| Region | Sylhet Division |
| Features | Load demand, hour, day, month, year |

---

## Environmental Data

| Property | Details |
|---|---|
| Source | NASA POWER Project |
| Parameters | Temperature, humidity, solar radiation |
| Spatial Resolution | 0.5° × 0.5° |
| Temporal Resolution | Hourly |

---

# 📈 Results & Performance

<p align="center">
  <img src="LFSC/figures/result.png" width="750">
</p>

Figure: Actual vs predicted load demand for hourly and daily forecasting models.

---

## Model Performance

| Forecast Horizon | MAE (MW) | MAPE (%) |
|---|---|---|
| 1-Hour Ahead | 18.47 | 5.35 |
| 24-Hour Ahead | 27.48 | 7.78 |

---

# 🔬 Comparison with Existing Methods

| Model | Improvement |
|---|---|
| Support Vector Regression (SVR) | 25.5% |
| Hybrid CNN-LSTM | 53.0% |
| Traditional ARIMA | 76.6% |

The proposed LSTM model demonstrates superior forecasting performance for short-term electricity demand prediction.

---

# 📌 Key Findings

- LSTM effectively captures temporal dependencies and seasonal patterns.
- Environmental parameters significantly influence electricity demand.
- Hardware integration introduces minimal latency.
- Real-time forecasting supports proactive grid management.

---

# 🧩 Dependencies

| Package | Version |
|---|---|
| Python | 3.8+ |
| TensorFlow | 2.x |
| NumPy | Latest |
| Pandas | Latest |
| Matplotlib | Latest |
| Scikit-learn | Latest |

---

# 🔁 Reproducibility

To ensure reproducibility, fixed random seeds were used during training.

```python
import tensorflow as tf
import numpy as np
import random

tf.random.set_seed(42)
np.random.seed(42)
random.seed(42)
```

---

# 🎓 Citation

If you use this work in your research, please cite:

```bibtex
@inproceedings{islam2026lstm,
  title={Website-Integrated Hardware Implementation of LSTM-Based Short-Term Load Forecasting Model: A Case Study for Sylhet Division},
  author={Islam, Saydul},
  booktitle={2nd IEEE International Conference on Quantum Photonics, Artificial Intelligence, and Networking (QPAIN)},
  year={2026},
  organization={IEEE},
  address={Chattogram, Bangladesh}
}
```

---

# 🤝 Contributing

Contributions are welcome.

## Contribution Steps

1. Fork the repository
2. Create a feature branch

```bash
git checkout -b feature/AmazingFeature
```

3. Commit your changes

```bash
git commit -m "Add Amazing Feature"
```

4. Push to GitHub

```bash
git push origin feature/AmazingFeature
```

5. Open a Pull Request

---

# 🛣️ Roadmap

## Completed

- [x] LSTM model development
- [x] Hardware implementation
- [x] Data preprocessing pipeline
- [x] Model evaluation and benchmarking

---

## Planned Features

- [ ] Multi-region forecasting
- [ ] Mobile application
- [ ] Anomaly detection
- [ ] SCADA integration
- [ ] Ensemble forecasting models
- [ ] Edge AI deployment
- [ ] Real-time alert system

---

# 📚 Related Publication

Presented at:

- **2nd IEEE International Conference on Quantum Photonics, Artificial Intelligence, and Networking (QPAIN 2026)**
- **Paper ID:** 4311
- **Date:** April 16–18, 2026
- **Location:** CUET IT Business Incubator, Chattogram, Bangladesh

---

# 🔗 Useful Links

- Bangladesh Power Development Board (BPDB)  
  http://www.bpdb.gov.bd/

- NASA POWER Project  
  https://power.larc.nasa.gov/

- TensorFlow Documentation  
  https://www.tensorflow.org/

- ESP32 Documentation  
  https://docs.espressif.com/projects/esp-idf/en/latest/esp32/

---

# 👨‍💻 Author

**Saydul Islam**  
Department of Electrical & Electronic Engineering  
Sylhet Engineering College (SEC)  
Sylhet, Bangladesh

### Contact

- GitHub: https://github.com/Juman-7
- Repository: https://github.com/Juman-7/Load-forecasting-for-Sylhet-Division

---

# 🙏 Acknowledgments

- Bangladesh Power Development Board (BPDB)
- NASA POWER Project
- IEEE QPAIN 2026
- Sylhet Engineering College
- All contributors and researchers

---

# 📄 License

This project is licensed under the MIT License.

---

# ⭐ Support

If you find this project useful, please consider giving it a star on GitHub.
