# Climate Change Modeling Project

Welcome to the Climate Change Modeling repository! This project analyzes historical temperature data to uncover trends, forecast future temperatures, and detect anomalies using time series models like ARIMA and LSTM. As a data scientist with a passion for environmental insights, I built this to explore how our planet's temperatures have evolved and what might lie ahead. It's a mix of exploratory analysis, feature engineering, and predictive modeling—all wrapped in a Jupyter notebook for easy replication.

If you're into climate data, machine learning, or just curious about global warming patterns, dive in! This README breaks down everything you need to know.

## Table of Contents

- [Project Overview]
- [Data Sources]
- [Installation]
- [Usage]
- [Methodology]
- [Key Findings]
- [Models and Comparisons]
- [Limitations and Future Work]
- [Contributing]
- [License]

## Project Overview

This repository contains a comprehensive analysis of global temperature datasets to model climate change. The core is a Jupyter notebook (`Climate-Change-Model.ipynb`) that loads, cleans, explores, and models the data. We visualize trends, merge datasets for deeper insights, engineer features, forecast temperatures with ARIMA and LSTM, and detect anomalies that stand out from expected patterns.

The goal? To highlight rising temperatures, predict future scenarios, and spot unusual events—like that wild spike in 1850. It's not just numbers; it's a story of our changing world, backed by solid data science.

Inspired by repos like TensorFlow's examples or scikit-learn's tutorials, this README keeps things clear, visual, and actionable.

## Data Sources

We used five historical temperature datasets (sourced from public climate archives like Berkeley Earth):

- **GlobalLandTemperaturesByCity.csv**: Monthly temperatures for cities worldwide (1743–2013).
- **GlobalTemperatures.csv**: Global land and ocean averages (1750–2015).
- **TemperaturesByCountry.csv**: Country-level temperatures (1743–2013).
- **TemperaturesByMajorCity.csv**: Data for major cities (1849–2013).
- **TemperaturesByState.csv**: State-level data, focused on the US (1855–2013).

These files are massive—millions of rows—so we handle them efficiently with pandas. Note: Paths in the notebook point to a Google Drive mount; adjust for your setup.

## Methodology

We follow a structured data science pipeline:

### 1. Data Loading and Exploration
- Load CSVs into DataFrames.
- Inspect shapes, heads, info, and nulls (e.g., df_city has 8.6M rows!).
- Handle missing temperatures by dropping NaNs and converting dates to datetime.

### 2. Cleaning and Preprocessing
- Drop rows with missing key values.
- Standardize column names (e.g., 'dt' to 'Date').
- Resample to yearly means for forecasting.

### 3. Exploratory Data Analysis (EDA)
- **Visuals**: Line plots for global trends, histograms for distributions, bar charts for top countries by average temp.
- **Insights**: Clear upward trend in global temps, hottest countries like Djibouti, and city/state variations (e.g., New York vs. Tokyo).

### 4. Data Merging and Feature Engineering
- Merge country and global annual averages for comparisons.
- Add features: Year/Month/Quarter, lags (e.g., previous month's temp), rolling means, and anomalies vs. a 1750–1800 baseline.

### 5. Forecasting
- **ARIMA**: Trained on data up to 2000, predicts to 2015 (RMSE: 0.1905). Extends 20 years ahead—stable around 15.66°C.
- **LSTM**: Scaled data, used a look-back of 3 years, trained with 100 epochs (RMSE: 0.0940). Predicts a gradual rise.

### 6. Anomaly Detection
- Calculate residuals (actual - predicted).
- Flag anomalies if >2 std devs from training residuals.
- ARIMA spots 1850; LSTM flags 1877, 1878, 1884.

### 7. Comparison and Interpretation
- LSTM outperforms ARIMA on test data but both struggle with rapid acceleration without external factors like CO2.

All code is in the notebook with comments—easy to follow!

## Key Findings

- **Warming Trend**: Global land temps have risen, accelerating post-1950. Top hot spots? Countries like Sudan and Mali.
- **Forecasts**: Expect continued warming (LSTM says ~0.1–0.2°C rise by 2035), but models predict conservatively.
- **Anomalies**: Big outlier in 1850 (possible data quirk or volcanic event). LSTM catches more in the late 1800s.
- **Regional Insights**: Cities like Cairo show steady heat; US states vary wildly (California warmer than New York).

Visuals in the notebook make these pop—check the plots for the full picture.

## Models and Comparisons

| Model   | Test RMSE | Future Trend       | Anomalies Detected |
|---------|-----------|--------------------|--------------------|
| ARIMA  | 0.1905   | Stable (~15.66°C) | 1 (1850)          |
| LSTM   | 0.0940   | Gradual rise      | 3 (1877–1884)     |

LSTM wins on accuracy, capturing non-linear vibes better. But ARIMA is simpler and faster for quick checks.

## Limitations and Future Work

- **Data Gaps**: Early years have missing values; interpolation helps but isn't perfect.
- **Model Limits**: No external drivers (e.g., emissions) means forecasts miss real-world complexity.
- **Compute**: LSTM needs decent hardware for training.
- **Next Steps**: Add CO2 data, try Prophet or ensemble models, or zoom into regional forecasts. Pull requests welcome!
## Installation

Get started in minutes! This project runs in a Python environment with Jupyter.

### Prerequisites
- Python 3.8+
- Jupyter Notebook or Lab
- Virtual environment (recommended: `venv` or `conda`)

### Steps
1. Clone the repo:
   ```
   git clone https://github.com/yourusername/climate-change-model.git
   cd climate-change-model
   ```

2. Create and activate a virtual environment:
   ```
   python -m venv env
   source env/bin/activate  # On Windows: env\Scripts\activate
   ```

3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```
   (If no `requirements.txt` yet, install these manually: `pandas`, `matplotlib`, `seaborn`, `statsmodels`, `scikit-learn`, `tensorflow`, `numpy`.)

4. Launch Jupyter:
   ```
   jupyter notebook
   ```
   Open `Climate-Change-Model.ipynb` and run the cells.

For Google Colab users: Upload the notebook and datasets, then mount your Drive.

## Usage

Fire up the notebook and follow along:

- **Run the Analysis**: Execute cells sequentially. It loads data, cleans it, generates plots, trains models, and outputs forecasts.
- **Customize**: Tweak parameters like ARIMA order (e.g., (5,1,0)) or LSTM epochs (default: 100) for experiments.
- **Visualize**: Check out line plots for trends, histograms for distributions, and forecast graphs.
- **Forecast Example**: Predict 20 years ahead—see how ARIMA stays flat while LSTM trends upward.
- **Anomaly Detection**: Spot outliers based on residuals (e.g., 1850 for ARIMA).

Pro tip: If you're low on compute, subsample the data for quicker runs.
MIT License—use it freely, but credit the original work. See [LICENSE](LICENSE) for details.

[1](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/88145549/ae610584-0078-4451-a730-34ddf8e75998/Climate-Change-Model.docx)
