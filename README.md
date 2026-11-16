# Who cancels a hotel booking?

Scientific Data Visualization project by Marta Brzezińska and Łukasz Madej.

An interpretable CatBoost analysis of 36,285 hotel bookings. We study how **lead time** and **special requests** relate to cancellation, and how the two interact.

## Research hypotheses

| | Hypothesis | Method |
|---|---|---|
| H1 | Longer lead time is associated with a higher probability of cancellation | Partial dependence plot (PDP) vs observed rates |
| H2 | More special requests are associated with a lower probability of cancellation, after accounting for other features | Model-based what-if scenarios, SHAP |
| H3 | The relationship between special requests and cancellation varies with lead time | Interaction plots, Friedman's H |

All results are descriptive associations, not causal effects. Rows inside groups of identical bookings are not independent, so we do not report formal tests.

## Repository structure

```
.
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   └── booking.csv          # not committed, see "Data" below
├── notebooks/
│   └── hotel_cancel_analysis.ipynb
```

## Data

Put `booking.csv` in `data/` (or next to the notebook and adjust the path in the first code cell).
Source: (https://www.kaggle.com/datasets/youssefaboelwafa/hotel-booking-cancellation-prediction/data)
## How to run

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/hotel_cancel_analysis.ipynb
```

Set `DEDUP = True` in the first code cell to rerun everything without exact duplicate rows (sensitivity analysis). Run all cells after changing it.

## Method summary

- 60/20/20 train / validation / test split, stratified by outcome and grouped by identical rows, so no copy of a booking appears on both sides.
- CatBoost on 13 booking features, logistic regression as baseline.
- Interpretation: PDP, what-if scenarios, interaction plots, Friedman's H, SHAP.

## Authors

Marta Brzezińska, Łukasz Madej
