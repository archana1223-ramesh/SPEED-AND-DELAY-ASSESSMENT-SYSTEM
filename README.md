# 🚦 AI-Based Traffic Speed & Delay Assessment System

An AI-based prototype for estimating traffic speed and delay using machine learning, detecting vehicles from traffic footage, and visualizing simulated congestion across Chennai. The project demonstrates how data-driven techniques can support traffic monitoring and analysis.

**Tech Stack:** Python · XGBoost · scikit-learn · YOLOv8 · OpenCV · GeoPandas · Matplotlib · Streamlit

> **Note:** This project uses synthetic (simulated) traffic data for speed and delay prediction. The model results represent performance on simulated data and have not been validated against real-world traffic measurements. The project is a proof of concept, not a deployed traffic management system.

## 📌 Problem Statement

Urban areas such as Chennai experience traffic congestion due to varying vehicle volumes, road capacity, weather conditions, and traffic incidents.

This project explores how machine learning can estimate traffic speed and delay from traffic-related inputs. It also demonstrates vehicle detection and map-based visualization to help illustrate potential congestion hotspots.

## ✨ Features

- **Traffic Speed Estimation:** Uses an XGBoost regression model to estimate average traffic speed in km/h from simulated traffic conditions.
- **Traffic Delay Estimation:** Uses a separate XGBoost regression model to estimate traffic delay in minutes.
- **Interactive Dashboard:** Provides a Streamlit interface where users can enter traffic conditions and view model predictions.
- **Vehicle Detection:** Uses a pretrained YOLOv8n model with OpenCV to detect vehicles and other supported object classes in traffic footage.
- **Congestion Visualization:** Plots simulated traffic locations across Chennai on an OpenStreetMap-based map and categorizes them into Low, Medium, and High congestion levels based on assigned speeds.

## 🛠️ Technology Stack

| Category         | Technologies                      |
| ---------------- | --------------------------------- |
| Programming      | Python                            |
| Machine Learning | XGBoost, scikit-learn             |
| Object Detection | YOLOv8 (Ultralytics)              |
| Image Processing | OpenCV                            |
| Data Processing  | Pandas, NumPy                     |
| Visualization    | Matplotlib, GeoPandas, Contextily |
| Dashboard        | Streamlit                         |
| Model Storage    | Pickle (`.pkl`)                   |

## 📊 Model Evaluation

The speed and delay regression models were evaluated using a held-out 20% test split from a synthetic dataset containing 8,000 records.

| Prediction Task | R² Score | Mean Absolute Error (MAE) |
| --------------- | -------: | ------------------------: |
| Traffic Speed   |     0.94 |              Not reported |
| Traffic Delay   |     0.94 |              1.67 minutes |

**How to interpret these results:**

- The R² scores indicate how well the models explain variation in the simulated test data.
- The delay MAE of 1.67 minutes represents the average absolute prediction error on that test set.
- These results measure performance on synthetic data, not on actual Chennai traffic.
- Real-world reliability would require evaluation using real traffic measurements and appropriate validation.

*Note: Confirm these metrics against the actual model evaluation output before publishing them.*

## 🗂️ Project Structure

```text
├── app.py                 # Streamlit dashboard
├── predict.py             # Loads trained models and generates predictions
├── train_model.py         # Trains speed and delay regression models
├── data_generator.py      # Generates synthetic traffic data
├── model_speed.pkl        # Saved speed prediction model
├── model_delay.pkl        # Saved delay prediction model
├── analysis.ipynb         # Vehicle detection and congestion map visualization
├── design_report.pdf      # Project design report
├── design_slides.pptx     # Project presentation
└── requirements.txt       # Python dependencies
```

## ⚙️ How It Works

### 1. Synthetic Data Generation

The `data_generator.py` script generates 8,000 simulated traffic records. The records include variables such as:

- Hour and day
- Vehicle count and traffic density
- Road capacity
- Weather conditions
- Incident status

The synthetic data represents relationships between traffic conditions, estimated speed, and delay.

### 2. Model Training

The `train_model.py` script trains two separate XGBoost regression models:

- A model for estimating average traffic speed.
- A model for estimating traffic delay.

The documented configuration uses 300 trees and a maximum tree depth of 5. The trained models are saved as `.pkl` files for later use.

### 3. Prediction Dashboard

The `predict.py` module loads the saved models and generates predictions from the provided input features.

The `app.py` script provides a Streamlit dashboard where users can adjust traffic conditions and view estimated speed and delay.

### 4. Vehicle Detection

The `analysis.ipynb` notebook demonstrates vehicle detection using a pretrained YOLOv8n model and OpenCV.

This component identifies objects in traffic footage. Automated speed estimation from vehicle tracking and direct integration of detected vehicle counts into the regression models are planned enhancements unless explicitly implemented in the current code.

### 5. Congestion Map Visualization

The notebook generates simulated traffic locations across Chennai and visualizes them on a map.

The displayed congestion categories are based on assigned speed values:

- **Low:** Speed greater than 40 km/h
- **Medium:** Speed greater than 20 km/h and up to 40 km/h
- **High:** Speed of 20 km/h or below

These categories are used for visualization and do not represent verified real-time traffic conditions.

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or another version compatible with the dependencies in `requirements.txt`
- pip
- Git

### Installation

**1. Clone the repository**

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

Replace the repository URL and folder name with your actual GitHub repository details.

**2. Install dependencies**

```bash
pip install -r requirements.txt
```

**3. Train the models (optional)**

If you want to regenerate the saved models:

```bash
python train_model.py
```

Make sure the script creates the expected model files before running the dashboard.

**4. Launch the Streamlit dashboard**

```bash
streamlit run app.py
```

Open the local URL displayed in the terminal to interact with the dashboard.

### Running the Vehicle Detection Notebook

Install the additional dependencies if they are not already included:

```bash
pip install opencv-python ultralytics geopandas contextily shapely matplotlib
```

Launch Jupyter Notebook:

```bash
pip install notebook
jupyter notebook
```

Open `analysis.ipynb` and execute its cells. The notebook may download pretrained YOLOv8 weights and map tiles, so an internet connection may be required.

## ⚠️ Limitations

- Speed and delay models are trained using synthetic data rather than real traffic observations.
- Reported evaluation metrics have not been validated against real-world traffic data.
- The congestion map uses simulated locations and assigned speed values.
- Vehicle detection does not automatically provide accurate vehicle speed; speed estimation generally requires tracking across frames and appropriate calibration.
- The current prototype does not directly control traffic signals or provide a verified real-time traffic forecasting service.

## 🔭 Future Enhancements

- [ ] Evaluate predictions using real traffic or publicly available traffic datasets.
- [ ] Integrate vehicle counts extracted from traffic footage into the prediction pipeline.
- [ ] Estimate vehicle speed using object tracking, frame timestamps, and suitable camera calibration.
- [ ] Explore LSTM or other time-series models for traffic forecasting.
- [ ] Develop a Power BI dashboard for analyzing traffic delay and congestion hotspots.
- [ ] Compare model performance against appropriate baseline models and additional evaluation metrics.

## 👩‍💻 Author

**Archana R**

**Project Theme:** Theme 3 – AI-Based Traffic Data Generation and Monitoring Application
