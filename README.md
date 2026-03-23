# multivariate-energy-consumption-prediction
Multivariate time-series energy consumption prediction using RFE and LSTM on the UCI Household Electric Power Consumption dataset.

This project focuses on short-term household energy consumption forecasting using a multivariate time-series approach. It combines Recursive Feature Elimination (RFE) for feature selection with an LSTM neural network built in Keras to model temporal patterns in electricity usage. The work uses the UCI Individual Household Electric Power Consumption dataset and compares the proposed model against a Random Forest baseline.  ￼

Overview

Accurate short-term energy forecasting is important for smart-grid management, demand response, load balancing, and sustainable energy planning. Traditional statistical models often struggle with nonlinear and long-term dependencies in energy data. This project explores a hybrid workflow where RFE selects the most informative predictors and LSTM learns temporal dynamics from the selected features.  ￼

Objectives

	•	Forecast short-term household energy consumption using multivariate time-series data
	•	Reduce input dimensionality using Recursive Feature Elimination
	•	Capture temporal dependencies with LSTM
	•	Compare deep learning performance with a strong Random Forest baseline
	•	Build a reproducible pipeline suitable for smart-grid and IoT-oriented applications  ￼

Dataset

The project uses the UCI Individual Household Electric Power Consumption dataset, which contains more than 2 million minute-level records collected from a single household between December 2006 and November 2010. In this work, the data was resampled to hourly averages, producing roughly 35,000 samples. The target variable is Global active power.  ￼

Methodology

The workflow followed in this project includes:

	1.	Data preprocessing
	•	Missing values marked as ? were handled using time-based linear interpolation
	•	Data was resampled from minute-level to hourly averages
	•	Features were scaled using Min-Max normalization
	•	Data was split chronologically into 80% training and 20% testing sets 
	￼
	2.	Feature engineering
	•	Lag features were created from Global active power:
	•	gap lag 1
	•	gap lag 2
	•	gap lag 3  ￼
	
	3.	Feature selection using RFE
	•	RFE was applied with a Random Forest regressor
	•	The final model retained 9 features, including:
	•	Global reactive power
	•	Voltage
	•	Global intensity
	•	Sub metering 1
	•	Sub metering 2
	•	Sub metering 3
	•	gap lag 1
	•	gap lag 2
	•	gap lag 3  ￼
	
	4.	LSTM model design
	•	Input window size: 24 time steps
	•	Architecture:
	•	LSTM layer with 64 units
	•	Dropout layer with 0.2
	•	Dense output layer
	•	Training configuration:
	•	Optimizer: Adam
	•	Learning rate: 1e-3
	•	Loss: Mean Squared Error
	•	Batch size: 32
	•	Early stopping on validation loss  
	￼
	5.	Baseline model
	•	A Random Forest Regressor with 500 estimators was used as the non-sequential baseline on the same final feature set.  ￼

Evaluation Metrics

The models were evaluated using:

	•	MAE – Mean Absolute Error
	•	RMSE – Root Mean Squared Error
	•	R² – Coefficient of Determination
	•	MAPE – Mean Absolute Percentage Error  ￼

Results

Random Forest Baseline

	•	MAE: 0.01654
	•	RMSE: 0.028486
	•	R²: 0.99933
	•	MAPE: 1.72%  ￼

RFE–LSTM Model

	•	MAE: 0.47297
	•	RMSE: 0.69454
	•	R²: 0.59988
	•	MAPE: 45.99%  ￼

The Random Forest baseline outperformed the current RFE–LSTM configuration across all reported metrics. However, the RFE–LSTM still captured meaningful temporal patterns and achieved a moderate R² of about 0.60, showing that the sequence model learned useful structure from the data.  ￼

Key Findings

	•	RFE helped build a compact and interpretable feature set
	•	Lag features improved short-horizon forecasting stability
	•	The model remained relatively stable for RFE feature counts between 8 and 12
	•	A 24-step window provided a good trade-off between performance and computational cost
	•	The pipeline offers a lightweight framework that can be extended for smart-grid and IoT applications  ￼

Applications

This project can support use cases such as:

	•	household load forecasting
	•	demand response systems
	•	energy efficiency planning
	•	anomaly or leakage detection
	•	smart-grid decision support
	•	edge and IoT-based forecasting systems  ￼

Future Improvements

Possible future enhancements include:

	•	adding external variables such as weather, occupancy, and pricing
	•	experimenting with BiLSTM, GRU, and Transformer-based models
	•	applying hyperparameter optimization using GA or PSO
	•	improving long-horizon forecasting performance
	•	deploying the forecasting pipeline on Raspberry Pi or other edge devices  ￼

Research Contribution

This work presents a pipeline that combines interpretability through feature selection with deep temporal learning through LSTM. It aims to bridge the gap between classical machine learning baselines and deep learning approaches for real-world energy forecasting problems.  ￼

Author

Prischa Bajeli
