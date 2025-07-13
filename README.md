# Wind Power Forecasting

A modular and scalable pipeline for forecasting wind power generation using historical turbine data and numerical weather predictions (NWP). The project applies machine learning and statistical modeling techniques to improve grid reliability, optimize energy scheduling, and support renewable integration.


## Objectives

- Predict short- and medium-term wind power output (15 min to 48 hours ahead)
- Leverage NWP data and turbine operational data for improved accuracy
- Compare multiple forecasting methods: statistical, ML, and deep learning
- Provide reproducible code, configurable experiments, and visual insights


## Project Structure

```
wind-power-forecast/
├── README.md
├── requirements.txt
├── data/
│   ├── raw/               # Unprocessed data
│   ├── processed/         # Cleaned and feature-enhanced data
│   └── external/          # NWP or external datasets
├── notebooks/             # Jupyter Notebooks for EDA, modeling
├── src/
│   ├── preprocessing/     # Data loading, cleaning
│   ├── features/          # Feature engineering logic
│   ├── models/            # Model training, forecasting
│   ├── visualization/     # Plotting functions
│   └── utils/             # Configs, metrics, helpers
├── models/                # Trained model artifacts
├── config/                # YAML configuration files
├── reports/               # Visual and textual outputs
└── tests/                 # Unit tests

````

---

## Getting Started

### Prerequisites

- Python 3.12+
- pip or conda

### Installation

```bash
git clone https://github.com/your-username/wind-power-forecast.git
cd wind-power-forecast
pip install -r requirements.txt
````

## How to Use

1. **Configure the pipeline**
   Edit `config/config.yaml` to set paths and parameters.

2. **Run preprocessing**

```bash
python src/data/preprocess.py
```

3. **Train model**

```bash
python src/models/train_model.py
```

4. **Generate forecasts**

```bash
python src/models/forecast.py
```

5. **Visualize results**

```bash
python src/visualization/plot_forecasts.py
```

## Models Included

* Linear Regression
* Random Forest
* XGBoost
* LSTM (optional deep learning module)

## Evaluation Metrics

* MAE (Mean Absolute Error)
* RMSE (Root Mean Squared Error)
* NMAE, NRMSE (normalized metrics)
* Skill Score vs. baseline (persistence)

## Example Datasets

> You can use open datasets such as:

* [Open Power System Data (OPSD)](https://data.open-power-system-data.org/)
* [Global Wind Atlas](https://globalwindatlas.info/)
* ERA5 Reanalysis (via Copernicus Climate Data Store)

## Testing

Run all tests using:

```bash
pytest tests/
```

## References

* Giebel et al. (2011), *The State-Of-The-Art in Short-Term Prediction of Wind Power*
* Pinson (2013), *Wind energy: Forecasting challenges for its operational management*
* Open Energy Forecasting datasets and libraries

## Future Work

* Add probabilistic and ensemble forecasts
* Real-time inference and online learning
* Web-based dashboard or API for forecast delivery

## License

This project is licensed under the Apache-2.0 License.
