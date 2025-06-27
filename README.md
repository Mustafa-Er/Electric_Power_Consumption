# 🔌 Household Energy Consumption Forecasting (24-Hour Prediction)

This project focuses on predicting **household energy consumption** 24 hours ahead using time series data collected from a home in **Sceaux, France** (near Paris).  
The goal is to forecast the **Global Active Power** for the next day based on historical electrical, time-based, and environmental features.

---

## 📦 Dataset Overview

- **Time span**: December 2006 – November 2010 (47 months)  
- **Total records**: 2,075,259 (1-minute intervals)  
- **Source**: A single household with detailed sub-metering and voltage data

---

## 🔑 Key Features

| **Feature**              | **Description**                                      |
|--------------------------|------------------------------------------------------|
| `Global_active_power`    | Total active power used (kW)                         |
| `Global_reactive_power`  | Reactive power (kW)                                  |
| `Voltage`                | Line voltage (V)                                     |
| `Sub_metering_1/2/3`     | Energy usage in kitchen, laundry, water heater/AC    |
| Time-based Features      | Hour, day of week/month/year, etc.                   |
| Weather & Solar Features | Temperature, humidity, turbidity, sun position, etc. |

---

## 🎯 Problem Statement

### 📌 Objective  
Predict the value of `Global_active_power` **24 hours into the future** using past trends and contextual features.

```python
# Define target variable
df['Target'] = df['Global_active_power'].shift(-24)  # 24 hours ahead
```

---

## 🔍 Feature Engineering

- **Dimensionality Reduction**:  
  Applied PCA to reduce redundancy; retained 99% variance using 3 components.

- **Final Feature Set**:  
  `Global_active_power`, `Hour`, `Day_ofweek`, `Day_ofmonth`, `Day_ofyear`,  
  `Week_ofyear`, `Month`, `Quarter`, `Year`, `PCA_1`, `PCA_2`, `PCA_3`

---

## 🧪 Modeling Approach

Used three different models to compare prediction performance:

| **Model**                        | **Details**                                  |
|----------------------------------|----------------------------------------------|
| ✅ XGBoost                       | Tree-based ensemble method                   |
| 🧠 Fully Connected Neural Network| Feed-forward dense layers                    |
| 🔁 LSTM (Long Short-Term Memory) | Used past 24-hour window as input sequence   |

- **Cross-Validation**:  
  Used `TimeSeriesSplit` with 5 folds to simulate realistic future prediction

---

## 📈 Results (MAE Comparison)

Mean Absolute Error (MAE) was used to evaluate model performance:

![MAE Chart](https://github.com/user-attachments/assets/a0fab91c-c078-4126-bed8-d604870e74be)

---

## 📊 Observations

- 🔁 **LSTM** consistently delivered the **lowest error** across all validation folds.
- ✅ **XGBoost** was stable and reliable but slightly less accurate than LSTM.
- 🧠 **Fully connected neural network** lagged behind, especially in early validation folds.

---

## ✅ Conclusion

- LSTM models are well-suited for **temporal prediction tasks** like energy consumption forecasting.
- XGBoost offers a simpler and faster alternative with reasonable performance.
- PCA and feature engineering significantly enhanced model input quality and interpretability.
