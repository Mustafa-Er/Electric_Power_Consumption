🔌 Household Energy Consumption Forecasting (24-Hour Prediction)
This project focuses on predicting household energy consumption 24 hours ahead using time series data collected from a home in Sceaux, France (near Paris). The goal is to forecast the "Global Active Power" for the next day based on historical electrical and environmental data.

📦 Dataset Overview
Time span: December 2006 – November 2010 (47 months)

Total records: 2,075,259 (1-minute intervals)

Source: A single household with detailed sub-metering and voltage data


🔑 Key Features:
Global_active_power: Total active power used (kW)

Global_reactive_power: Reactive power (kW)

Voltage: Line voltage (V)

Sub_metering_1/2/3: Energy use in kitchen, laundry room, water heater/AC

Time-based Features: Hour, day of week/month/year, etc.

Weather & Solar Features: temp, rhum, prcp, turbidity, sun_position, etc.


🎯 Problem Statement
📌 Objective: Predict the value of Global_active_power 24 hours into the future based on past trends and contextual features.

Target definition:
python
Kopyala
Düzenle
df['Target'] = df['Global_active_power'].shift(-24)  # 24 hours ahead (1 value per hour)

🧪 Modeling Approach
I used three different models for comparison:

XGBoost

Fully Connected Neural Network

LSTM (Long Short-Term Memory) – using a window of the previous 24 hours

🔍 Feature Engineering:
Dimensionality reduction with PCA (retaining 99% variance → 3 components)

Final feature set included:

Global_active_power, Hour, Day_ofweek, Day_ofmonth, Day_ofyear, Week_ofyear, Month, Quarter, Year, PCA_1, PCA_2, PCA_3

🧪 Cross-Validation:
TimeSeriesSplit with 5 folds

📈 Results (MAE Comparison)
Mean Absolute Error (MAE) was used to evaluate performance across folds:

![image](https://github.com/user-attachments/assets/a0fab91c-c078-4126-bed8-d604870e74be)



📊 Observations:
LSTM consistently performed better than the other models

XGBoost had stable but slightly higher error than LSTM model

Fully connected network lagged behind, especially in earlier folds
