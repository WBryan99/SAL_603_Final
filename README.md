# SAL_603_Final
Final Project: 
Player Efficiency Rating (PER) is the NBA's most widely cited all-in-one player contribution metric, developed by ESPN's John Hollinger. It summarizes a player's per-minute statistical performance into a single number, with league average always calibrated to **15.0**.

This project analyzes **50 NBA players** from the **2023-24 season** to determine which traditional box score statistics most strongly predict PER, whether those predictors differ by position group, and whether a regression model can reliably estimate PER from basic stats alone.

All data cleaning, transformation, and analysis was performed entirely in Python. No Excel was used at any point.

---

## ❓ Research Questions

| # | Question |
|---|----------|
| **RQ1** | Which traditional box score statistics most strongly correlate with PER? |
| **RQ2** | Do PER predictors differ across Guards, Forwards, and Centers? |
| **RQ3** | Can a multiple linear regression model reliably predict PER from basic box score stats? |

---

## 📊 Dataset

- **Source:** [Basketball-Reference.com](https://www.basketball-reference.com/leagues/NBA_2024_per_game.html)
- **Season:** 2023-24 NBA Season
- **Filter:** Players with ≥ 20 games played
- **Sample size:** 50 players

### Variables

| Variable | Type | Description |
|----------|------|-------------|
| `Player` | string | Player name |
| `Position` | string | PG / SG / SF / PF / C |
| `Pos_Group` | string | Guard / Forward / Center *(derived)* |
| `PTS` | float | Points per game |
| `REB` | float | Rebounds per game |
| `AST` | float | Assists per game |
| `STL` | float | Steals per game |
| `BLK` | float | Blocks per game |
| `TOV` | float | Turnovers per game |
| `FG_PCT` | float | Field goal percentage |
| `FT_PCT` | float | Free throw percentage |
| `PER` | float | Player Efficiency Rating *(dependent variable)* |
| `Net_Contrib` | float | PTS+REB+AST+STL+BLK−TOV *(derived)* |

---

## 📈 Visualizations

### Visualization 1 — Correlation Heatmap
Shows pairwise correlations between all box score statistics and PER. Points Per Game (r = 0.94) emerges as the dominant predictor.

![Correlation Heatmap](viz1_correlation_heatmap.png)

---

### Visualization 2 — PER by Position Group
Left: violin plot of PER distributions by Guard, Forward, and Center. Right: scatter plot of Points vs PER colored by position.

![Position Analysis](viz2_position_analysis.png)

---

### Visualization 3 — Regression Model Results
Left: standardized regression coefficients showing each stat's impact on PER. Right: actual vs predicted PER for all 50 players.

![Regression Results](viz3_regression_results.png)

---

### Visualization 4 — Top 15 Players by PER
Horizontal bar chart ranking the top 15 players by PER with per-game stats annotated, color-coded by position group.

![Top 15 Players](viz4_top15_players.png)

---

## 🏆 Key Findings

### RQ1 — Which stats drive PER?

| Statistic | Correlation with PER | Interpretation |
|-----------|---------------------|----------------|
| PTS | **r = 0.94** | Strongest predictor by far |
| TOV | r = 0.93 | Reflects high usage / ball-handling volume |
| AST | r = 0.74 | Playmaking adds significant value |
| STL | r = 0.69 | Defensive impact matters |
| REB | r = 0.47 | Moderate positive effect |
| FG_PCT | r = 0.13 | Weak alone — efficiency requires volume |

> **Scoring volume is king.** FG% alone is nearly useless as a predictor — it only matters in combination with high scoring volume.

---

### RQ2 — Does position matter?

| Position Group | Mean PER | Median PER | Std Dev |
|----------------|----------|------------|---------|
| Center | **21.5** | 20.2 | 7.40 |
| Guard | 19.8 | 21.0 | 6.03 |
| Forward | 16.7 | 15.8 | 6.36 |

> Centers average the highest PER due to interior shooting efficiency and rebounding. Guards show the most variance — from elite playmakers to bench role players.

---

### RQ3 — Can we predict PER?

| Metric | Value |
|--------|-------|
| R² Score | **0.954** |
| RMSE | **1.19 PER points** |
| Variance explained | **95.4%** |
| Train/Test Split | 70 / 30 |

**Top regression coefficients (standardized):**

| Rank | Statistic | Coefficient |
|------|-----------|-------------|
| 1 | PTS | +3.10 |
| 2 | TOV | +1.93 |
| 3 | REB | +1.02 |
| 4 | AST | +0.89 |
| 5 | BLK | +0.79 |

> A linear regression model using 8 basic box score stats explains **95.4% of the variance in PER** — confirming that traditional counting stats are nearly sufficient to reconstruct the metric entirely.

---

## 📁 Project Structure

```
nba-per-analysis/
│
├── NBA_PER_Analysis.py          # Main analysis script (run this)
├── NBA_2023_24_Stats.csv        # Dataset (50 players, 13 columns)
├── README.md                    # This file
│
├── viz1_correlation_heatmap.png # Correlation matrix heatmap
├── viz2_position_analysis.png   # PER by position + scatter
├── viz3_regression_results.png  # Regression coefficients + actual vs predicted
└── viz4_top15_players.png       # Top 15 players ranked by PER
```

---

## ▶️ How to Run

**1. Clone the repository**
```bash
git clone https://github.com/yourusername/nba-per-analysis.git
cd nba-per-analysis
```

**2. Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

**3. Run the analysis**
```bash
python NBA_PER_Analysis.py
```

The script will print all model results to the console and automatically save all 4 visualizations as `.png` files in the same directory.

**Optional — use your own data:**

Download the real 2023-24 per-game stats CSV from [Basketball-Reference](https://www.basketball-reference.com/leagues/NBA_2024_per_game.html), then replace the data loading section in `NBA_PER_Analysis.py`:

```python
# Replace the data dictionary with:
df = pd.read_csv('your_basketball_reference_export.csv')
```

---

## 📦 Dependencies

| Package | Version | Purpose |
|---------|---------|---------|
| `pandas` | 2.0+ | Data loading and transformation |
| `numpy` | 1.24+ | Numerical operations |
| `matplotlib` | 3.7+ | Visualization |
| `seaborn` | 0.12+ | Statistical plots |
| `scikit-learn` | 1.3+ | Regression model, scaling, evaluation |

Install all at once:
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
```

---

## 📂 Data Source

Statistics sourced from **Basketball-Reference.com**:
- [2023-24 NBA Per Game Stats](https://www.basketball-reference.com/leagues/NBA_2024_per_game.html)
- [2023-24 NBA Advanced Stats](https://www.basketball-reference.com/leagues/NBA_2024_advanced.html)

PER (Player Efficiency Rating) formula originally developed by **John Hollinger**. Reference: *Pro Basketball Forecast* (Brassey's Sports, 2002).

---

## 📌 Practical Takeaway

> *The single most impactful change a player can make to raise their PER is reducing turnovers while maintaining scoring volume. Front offices can reliably estimate a player's PER from traditional box score stats alone — no tracking data required.*

---

*SAL 603 — Sport Analytics | 2023-24 NBA Season Analysis*
