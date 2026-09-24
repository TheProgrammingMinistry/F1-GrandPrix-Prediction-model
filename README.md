# F1-GrandPrix-Prediction-model
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
