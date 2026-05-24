---

## 🔧 Installation & Setup

### Prerequisites
- Python 3.8 or higher
- Arduino IDE (for hardware programming)
- CUDA-compatible GPU (recommended for training)

### Software Setup

1. **Clone the repository**
```bash
   git clone https://github.com/Juman-7/Load-forecasting-for-Sylhet-Division.git
   cd Load-forecasting-for-Sylhet-Division/LFSC
```

2. **Create virtual environment**
```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. **Install dependencies**
```bash
   pip install -r requirements.txt
```

4. **Configure parameters**
```bash
   # Edit configuration file with your settings
   nano config.yaml
```

### Hardware Setup

1. **Components Required**
   - ESP32 development board
   - DHT11 temperature/humidity sensor
   - LoRa SX1278 module
   - Jumper wires and breadboard
   - Power supply (5V, 1A minimum)

2. **Wiring Diagram**
   Refer to `figures/Hardware.png` for complete circuit diagram

3. **Flash Firmware**
```bash
   # Open Arduino IDE
   # Load the ESP32 firmware code
   # Select board: ESP32 Dev Module
   # Upload to ESP32
```

---

## 📖 Usage

### Training the Model

```python
import sys
sys.path.append('LSTM model')
from train import train_lstm_model

# Train 1-hour ahead model
model_1h = train_lstm_model(
    data_path='Dataset/processed/hourly_load.csv',
    lookback=168,  # 1 week of hourly data
    horizon=1,
    epochs=100,
    batch_size=32
)

# Save trained model
model_1h.save('models/lstm_1hour.h5')
```

### Making Predictions

```python
from predict import load_model_and_predict

# Load model and make forecast
forecast = load_model_and_predict(
    model_path='models/lstm_1hour.h5',
    current_data=sensor_readings,
    steps_ahead=24
)

print(f"Next hour predicted load: {forecast[0]:.2f} MW")
```

### Running Evaluation

```python
from evaluate import evaluate_model

# Evaluate model performance
metrics = evaluate_model(
    model_path='models/lstm_1hour.h5',
    test_data='Dataset/processed/test_data.csv'
)

print(f"MAE: {metrics['mae']:.2f}")
print(f"MAPE: {metrics['mape']:.2f}%")
```

---

## 📊 Dataset Information

### Historical Load Data
- **Source**: Bangladesh Power Development Board (BPDB)
- **Duration**: 5 years (2018-2023)
- **Resolution**: Hourly
- **Coverage**: Sylhet Division regional grid
- **Features**: Total load (MW), time features (hour, day, month, year)

### Environmental Data
- **Source**: NASA POWER Project
- **Parameters**: Temperature, humidity, solar radiation
- **Spatial Resolution**: 0.5° × 0.5° (approx. 50km)
- **Temporal Resolution**: Hourly

---

## 📈 Results & Discussion

### Model Performance

![Results Comparison](LFSC/figures/result.png)

The LSTM model demonstrates exceptional accuracy in short-term load forecasting:

- **1-Hour Model**: MAE = 18.47 MW, MAPE = 5.35%
- **24-Hour Model**: MAE = 27.48 MW, MAPE = 7.78%

### Key Findings

1. **Temporal Dependencies**: LSTM effectively captures weekly and seasonal patterns
2. **Environmental Impact**: Temperature variations show strong correlation with load demand
3. **Real-time Feasibility**: Hardware integration adds minimal latency (<2 seconds)
4. **Practical Utility**: Forecasts enable proactive grid management and reserve optimization

### Comparison with State-of-the-Art

Our LSTM implementation outperforms:
- **Support Vector Regression (SVR)** by 25.5%
- **Hybrid CNN-LSTM** by 53.0%
- **Traditional ARIMA** by 76.6%

The figure above shows the actual vs. predicted load curves for both hourly and daily forecasting models, demonstrating the high accuracy of our approach.

---

## 🎓 Citation

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

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Areas for Contribution
- Improving model accuracy with advanced architectures
- Adding support for additional regions
- Developing mobile applications
- Enhancing web dashboard features
- Documentation improvements

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

**Saydul Islam**  
Department of Electrical & Electronic Engineering  
Sylhet Engineering College (SEC)  
Sylhet, Bangladesh

- 📧 Email: [your.email@example.com]
- 🔗 LinkedIn: [Your LinkedIn Profile]
- 🌐 GitHub: [@Juman-7](https://github.com/Juman-7)

---

## 🙏 Acknowledgments

- **Bangladesh Power Development Board (BPDB)** for providing historical load data
- **NASA POWER Project** for environmental datasets
- **2nd IEEE International Conference on Quantum Photonics, Artificial Intelligence, and Networking (QPAIN 2026)**
- **Sylhet Engineering College** for research support
- All contributors and researchers who have supported this project

---

## 📞 Contact & Support

For questions, issues, or collaboration opportunities:

- **GitHub Issues**: [Report a bug or request a feature](https://github.com/Juman-7/Load-forecasting-for-Sylhet-Division/issues)
- **Email**: your.email@example.com
- **Pull Requests**: Contributions are always welcome!

---

## 🗺️ Roadmap

### Current Status
- [x] LSTM model development and training
- [x] Hardware implementation with ESP32 and LoRa
- [x] Data preprocessing pipeline
- [x] Model evaluation and benchmarking

### Planned Features
- [ ] Multi-region forecasting support
- [ ] Mobile application (Android/iOS)
- [ ] Advanced anomaly detection
- [ ] Integration with SCADA systems
- [ ] Ensemble model with uncertainty quantification
- [ ] Edge computing deployment for offline operation
- [ ] Real-time alert system for grid operators

### Future Research Directions
- Attention mechanisms for interpretability
- Transfer learning for other regions in Bangladesh
- Multi-variate forecasting (solar, wind integration)
- Federated learning for distributed grids
- Integration with renewable energy sources

---

## 📚 Related Publications

This work was presented at:
- **QPAIN 2026**: 2nd IEEE International Conference on Quantum Photonics, Artificial Intelligence, and Networking
- **Paper ID**: 4311
- **Conference Dates**: April 16-18, 2026
- **Location**: CUET IT Business Incubator, Chattogram, Bangladesh

---

## 🔗 Useful Links

- [Bangladesh Power Development Board (BPDB)](http://www.bpdb.gov.bd/)
- [NASA POWER Project](https://power.larc.nasa.gov/)
- [TensorFlow Documentation](https://www.tensorflow.org/)
- [ESP32 Documentation](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/)

---

**⭐ If you find this project useful, please consider giving it a star on GitHub!**

---

## 📸 Visual Documentation

All figures and diagrams are available in the `LFSC/figures/` directory:

- **Data_pre_processing.png**: Complete data preprocessing workflow
- **Hardware.png**: Hardware implementation and circuit diagram
- **model_workflow.png**: LSTM model architecture and training pipeline
- **result.png**: Model performance and prediction results
