````markdown
# 🏎️ F1 Grand Prix Prediction Model

A Formula 1 race prediction project built with **Python, FastF1, Pandas, NumPy, and Scikit-learn**.

The project collects historical Formula 1 race and qualifying data, engineers driver and team performance features, trains a machine-learning model, and uses the model to estimate the finishing order for a target Grand Prix.

---

## 📌 Project Overview

This project uses historical Formula 1 data from FastF1 to build a machine-learning model capable of predicting race finishing positions.

The model considers factors such as:

- Starting/grid position
- Driver's recent form
- Team's recent form
- Driver's average finish at a circuit
- Driver's DNF rate
- Driver's championship points
- Constructor/team championship points

The model is trained using historical race results and then used to generate a predicted finishing order for a selected Grand Prix.

---

## 🛠️ Technologies Used

- **Python**
- **FastF1** — Formula 1 data collection
- **Pandas** — Data manipulation
- **NumPy** — Numerical operations
- **Scikit-learn** — Machine learning
- **Gradient Boosting Regressor** — Prediction model
- **Google Colab** — Development environment
- **GitHub** — Version control and project storage

---

## 📊 Data Collection

Formula 1 race and qualifying data is collected using the FastF1 library.

The project retrieves:

- Race results
- Qualifying results
- Grid positions
- Driver names/abbreviations
- Teams
- Finishing positions
- Race status
- Championship points

The collected data is saved locally as:

```text
race_dataset.csv
````

FastF1 caching is also enabled to reduce repeated downloads:

```text
f1_cache/
```

---

## 🧠 Feature Engineering

The model uses historical information to create predictive features.

### Features

| Feature                     | Description                                           |
| --------------------------- | ----------------------------------------------------- |
| `grid_position`             | Driver's starting position                            |
| `driver_form_last5`         | Driver's average finishing position over recent races |
| `team_form_last5`           | Team's recent finishing performance                   |
| `driver_circuit_avg_finish` | Driver's historical average finish at the circuit     |
| `driver_dnf_rate`           | Driver's recent DNF rate                              |
| `season_points_so_far`      | Driver's points accumulated during the season         |
| `constructor_points_so_far` | Constructor/team points accumulated during the season |

The feature engineering process is designed to use information from races that occurred **before the race being predicted**, helping reduce future-data leakage.

---

## 🤖 Machine Learning Model

The project uses a:

```python
GradientBoostingRegressor
```

from Scikit-learn.

The model is configured with:

```python
n_estimators=300
max_depth=3
learning_rate=0.05
subsample=0.8
random_state=42
```

The target variable is:

```text
finish_position
```

The model therefore treats race finishing position as a regression problem.

---

## 🧪 Training and Evaluation

Instead of randomly splitting the data, the project uses a **chronological train/test split**.

Approximately:

* **85%** of the data → training
* **15%** of the data → testing

This approach is used because Formula 1 results are time-dependent, and randomly mixing older and newer races could introduce information from the future into the training process.

The model is evaluated using:

```text
Mean Absolute Error (MAE)
```

The MAE represents the average number of finishing positions by which the predictions differ from the actual results.

---

## 🏁 Making a Race Prediction

After the dataset has been built and the model trained, a target race can be selected.

Example:

```python
year = 2026
event_name = "Azerbaijan Grand Prix"

predicted_order = predict_next_race(
    model,
    df,
    year,
    event_name
)

predicted_order[
    ["driver", "team", "predicted_position"]
]
```

The resulting DataFrame contains the predicted order of the drivers.

Example output structure:

```text
driver    team          predicted_position
VER       Red Bull      ...
LEC       Ferrari       ...
ALO       Aston Martin  ...
```

---

## ⚠️ Grid Position

Actual grid position is not known until qualifying has taken place.

When making a prediction before qualifying, the project uses the driver's **average grid position from their most recent three races** as a substitute.

After qualifying, the model can be run again using the actual grid positions to produce an updated prediction.

---

## 🚀 Running the Project

### 1. Install FastF1

```python
!pip install fastf1
```

### 2. Build the dataset

```python
df = build_dataset()
```

This downloads the configured historical seasons and creates:

```text
race_dataset.csv
```

### 3. Train the model

```python
model, df = train_model(df)
```

This performs feature engineering, trains the Gradient Boosting model, evaluates it, and displays feature importance.

### 4. Predict a race

```python
year = 2026
event_name = "Azerbaijan Grand Prix"

predicted_order = predict_next_race(
    model,
    df,
    year,
    event_name
)

predicted_order[
    ["driver", "team", "predicted_position"]
]
```

---

## 📁 Project Structure

```text
F1-GrandPrix-Prediction-model/
│
├── Azerbaijan_Grand_Prix_Prediction.ipynb
├── race_dataset.csv
├── f1_cache/
└── README.md
```

> `race_dataset.csv` and `f1_cache/` may be generated when the notebook is executed.

---

## 📈 Feature Importance

After training, the model calculates the relative importance of the input features:

```python
importances = pd.Series(
    model.feature_importances_,
    index=MODEL_FEATURES
)

print(
    importances
    .sort_values(ascending=False)
    .to_string()
)
```

This helps explore which historical factors contributed most to the model's predictions.

---

## ⚠️ Limitations

This project is intended as a machine-learning experiment and should not be treated as an authoritative prediction of Formula 1 race results.

Important limitations include:

* Historical data does not guarantee future performance.
* Race incidents such as crashes and mechanical failures are difficult to predict.
* Weather conditions can significantly affect race outcomes.
* Driver and team performance can change between seasons.
* Pre-qualifying predictions do not have the actual starting grid.
* The current training configuration uses historical seasons rather than a continuously updated dataset.
* Predictions are based on the features available to the model and therefore cannot capture every factor influencing a race.

---

## 🔮 Future Improvements

Potential improvements include:

* Add more historical seasons.
* Incorporate qualifying performance.
* Add weather data.
* Include tire strategy information.
* Include practice-session performance.
* Add circuit-specific characteristics.
* Include driver/team changes during a season.
* Add race-day weather predictions.
* Compare multiple machine-learning algorithms.
* Automatically update the dataset after every Grand Prix.
* Create an interactive prediction dashboard.
* Deploy the model as a web application.

---

## 👨‍💻 Project

**F1 Grand Prix Prediction Model**

Built using Python and FastF1 with a Gradient Boosting machine-learning approach.

The project is developed in Google Colab and maintained on GitHub.

````

### One thing I recommend changing in your notebook

Your actual source code currently has:

```python
NEXT_RACE = {
    "year": 2023,
    "event_name": "Azerbaijan Grand Prix"
}
````

while your manual prediction cell uses:

```python
year = 2026
event_name = "Azerbaijan Grand Prix"
```

So if your goal is specifically **predicting the 2026 Azerbaijan Grand Prix**, I'd change the `NEXT_RACE` configuration to 2026 as well, rather than having two different target years. The current source explicitly labels 2023 as a historical demonstration race. 

You can create a file called **`README.md`** in your GitHub repository and paste the README above directly into it.
