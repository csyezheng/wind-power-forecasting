# Wind power forecasting

## Entire Wind Farm or Each Wind Turbine?

a farm-level aggregated forecast or individual turbine forecasts? Common Practice for Short-Term Forecasting (From 0:00 the next day to the next 72 hours, 15-minute time resolution)

## General process

### Data Collection

* **Historical Wind Power Data (SCADA)**: This is actual measured power output from the turbines/farm.
* **Meteorological Data (SCADA/Local Sensors)**: Real-time wind speed, wind direction, temperature, pressure, humidity collected at the wind farm site.
* **Numerical Weather Prediction (NWP) Data**: Forecasted meteorological variables (wind speed, direction, temperature, pressure, etc.) for the wind farm location from weather models. For longer horizons (like your 72-hour forecast), NWP becomes the most critical input.
* **Ancillary Data**: Turbine status (operational, curtailed, under maintenance), geographical information (terrain, obstacles), time-based features (hour of day, day of week, month, season, holidays).

### Data Preprocessing and Feature Engineering

#### Cleaning

Handling missing values, outliers.

#### Synchronization

Aligning different data sources by time.

#### Feature Creation

* **Lagged variables**: Past values of wind power, wind speed, etc., are highly predictive
* **Time-based features**: Encoding cyclic patterns (e.g., sine/cosine transformations for hour of day, day of year).
* **Derived features**: Wind components (u-wind, v-wind), wind speed at hub height (if only ground-level measurements are available).
* **NWP feature selection**: Choosing the most relevant NWP outputs for the specific wind farm.

### Model Selection and Training



## Ultra-short-term wind power forecast

forecasting power for the next 15 minutes to 4 hours, with a 15-minute time resolution

### Data Collection and Preprocessing

### Feature Selection

#### Essential Features (High Priority)

* Wind Speed

  Wind power is approximately proportional to the cube of wind speed. This will be your primary predictor.

* Historical Wind Power Output

  Past power values are excellent indicators of future power, especially for short horizons due to inertia in the system and autocorrelation.

* Wind Direction

  While wind speed is primary, wind direction can influence power output due to turbine yawing, wake effects from other turbines, and terrain effects.

#### Important, but Potentially Secondary (Consider based on data availability and quality)

* Temperature

  Can affect air density, which influences power output, although its effect is usually less pronounced than wind speed.

* Air Pressure

  Similar to temperature, affects air density.

* Turbine Status/Availability

  If individual turbine data is available, knowing if a turbine is operational or undergoing maintenance is crucial.

* Time-based Features

  * Hour of Day

    Wind patterns often exhibit diurnal cycles.

  * Day of Year/Month

    Seasonal variations in wind resources.

### Model Selection and Development

#### Gradient Boosting Machines (LightGBM/XGBoost)

#### LSTMs/GRUs

### Training and Validation

### Performance Evaluation

## Short-term forecasts

From 0:00 the next day to the next 72 hours, 15-minute time resolution

### Data Collection and Preprocessing

### Feature Selection

#### Essential Features (High Priority)

* Wind Speed

  Wind power is approximately proportional to the cube of wind speed. This will be your primary predictor.

* Historical Wind Power Output

  Past power values are excellent indicators of future power, especially for short horizons due to inertia in the system and autocorrelation.

* Wind Direction

  While wind speed is primary, wind direction can influence power output due to turbine yawing, wake effects from other turbines, and terrain effects.

#### Important, but Potentially Secondary (Consider based on data availability and quality)

* Temperature

  Can affect air density, which influences power output, although its effect is usually less pronounced than wind speed.

* Air Pressure

  Similar to temperature, affects air density.

* Turbine Status/Availability

  If individual turbine data is available, knowing if a turbine is operational or undergoing maintenance is crucial.

* Time-based Features

  * Hour of Day

    Wind patterns often exhibit diurnal cycles.

  * Day of Year/Month

    Seasonal variations in wind resources.

### Model Selection and Development

#### Gradient Boosting Machines (LightGBM/XGBoost)

Excellent starting point due to their performance and speed. Be meticulous with feature engineering.

**Input for GBM:**

- Lagged actual wind power values: Up to a certain point (e.g., 24-48 hours back) for capturing autocorrelation.
- Lagged NWP data: Past NWP values for the same forecast horizon can provide context.
- Future NWP data: This is essential for the 72-hour window. You'll use forecasted wind speed, direction, temperature, pressure, etc., for the target 15-minute intervals.
- Time-based features: Hour of day (sine/cosine transformations for periodicity), day of week, day of year, month, public holidays (if relevant to demand patterns, which can indirectly affect wind farm operation schedules).
- Interaction features: E.g., wind speed * wind direction components.

#### LSTMs/GRUs Networks

Highly capable of handling the temporal sequences inherent in this problem. These are often the go-to for such horizons with abundant data.

**Input for LSTMs/GRUs:**

- Historical sequence of wind power.
- Historical sequence of relevant meteorological features (wind speed, direction, temperature, etc.).
- **Future sequence of NWP data:** This is fed as "future known inputs" or "exogenous variables" to predict the output for the next 72 hours.

#### Hybrid/Ensemble

### Training and Validation

### Performance Evaluation