# Racial Bias in the COMPAS Risk Assessment Algorithm

An exploratory data analysis project investigating racial disparities in the COMPAS (Correctional Offender Management Profiling for Alternative Sanctions) recidivism risk scoring algorithm, using ProPublica's 2016 Broward County dataset.

---

## What is COMPAS?

COMPAS is a commercial algorithm used by judges and parole officers across the United States to assign defendants a **risk score from 1 to 10**, predicting the likelihood of reoffending. Higher scores can lead to denied bail, longer sentences, and rejected parole. In 2016, ProPublica investigated whether the algorithm was racially biased — this project replicates and extends that analysis.

---

## Key Findings

| Metric | African-American | Caucasian | Disparity |
|---|---|---|---|
| Average risk score | 5.28 | 3.64 | 45% higher |
| % flagged high risk (score ≥ 8) | 26.6% | 10.6% | **2.5× more likely** |
| False positive rate | 6.0% | 2.7% | **2.2× more likely** |

> **Main finding:** Black defendants are flagged as high risk at 2.5× the rate of white defendants, and this disparity persists even after controlling for criminal history.

---

## Project Structure

```
compas-bias-analysis/
│
├── compas_analysis.ipynb       # Main Jupyter notebook (all code + charts)
├── compas-scores-two-years.csv # Dataset (download instructions below)
├── charts/
│   ├── chart1_avg_score.png
│   ├── chart2_distribution.png
│   ├── chart3_highrisk.png
│   ├── chart4_priors.png
│   ├── chart5_heatmap.png
│   └── chart6_errors.png
└── README.md
```

---

## Dataset

**Source:** ProPublica COMPAS Analysis  
**Original records:** 7,214  
**After cleaning:** 5,278  
**Coverage:** Broward County, Florida — 2013 to 2014

Load directly in Python (no download needed):

```python
import pandas as pd

url = "https://raw.githubusercontent.com/propublica/compas-analysis/master/compas-scores-two-years.csv"
df = pd.read_csv(url)
```

---

## How to Run

**1. Clone the repository**
```bash
git clone https://github.com/your-username/compas-bias-analysis.git
cd compas-bias-analysis
```

**2. Install dependencies**
```bash
pip install pandas matplotlib seaborn jupyter
```

**3. Launch the notebook**
```bash
jupyter notebook compas_analysis.ipynb
```

**4. Run all cells in order**  
The notebook is structured in 6 steps — load, clean, EDA, visualize, interpret, conclude.

---

## Analysis Steps

### Step 1 — Load data
Load the CSV directly from GitHub using pandas.

### Step 2 — Clean data
- Filter to cases screened within ±30 days of arrest
- Remove unknown recidivism flags (`is_recid = -1`)
- Remove traffic offenses (`c_charge_degree = 'O'`)
- Keep African-American and Caucasian defendants only

### Step 3 — Exploratory Data Analysis
- Average risk score by race
- % flagged high risk by race
- False positive and false negative rates

### Step 4 — Visualizations
Six charts covering score distributions, high-risk labelling rates, disparity after controlling for priors, and algorithm error rates by race.

### Step 5 — Conclusions
Written findings with real-world implications and limitations.

---

## Charts

**Chart 1 — Average risk score by race**  
Direct bar comparison showing the 1.64-point average gap.

**Chart 2 — Score distribution**  
Histogram showing white defendants cluster at low scores while Black defendants spread across all levels.

**Chart 3 — % labelled high risk**  
The headline chart — 26.6% vs 10.6%, a 2.5× disparity.

**Chart 4 — Score by race and prior crimes**  
Controls for criminal history — the gap persists at every level of prior crimes.

**Chart 5 — Heatmap: race vs risk category**  
Shows exactly how defendants distribute across low, medium, and high risk tiers.

**Chart 6 — False positive vs false negative rates**  
Proves the algorithm makes systematically different errors for each race.

---

## Limitations

- Data covers only one county (Broward County, FL) and may not generalise nationally
- Analysis focuses on African-American vs Caucasian only — other groups excluded due to small sample sizes
- Correlation is shown, not causation — the exact mechanism of bias is not identified
- Variables like legal representation quality, socioeconomic status, and neighbourhood crime rates are absent from the dataset

---

## Tech Stack

- **Python 3.8+**
- **pandas** — data loading, cleaning, groupby analysis
- **matplotlib** — chart rendering and saving
- **seaborn** — heatmap and distribution plots
- **Jupyter Notebook** — interactive analysis environment

---

## References

- ProPublica (2016). *Machine Bias.* https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing
- ProPublica COMPAS dataset: https://github.com/propublica/compas-analysis

---

## License

MIT License — free to use, modify, and distribute with attribution.
