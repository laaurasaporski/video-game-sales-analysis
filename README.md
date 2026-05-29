# 🎮 Video Game Sales Analysis — Market Trends & Platform Strategy

Exploratory data analysis and hypothesis testing on global video game sales (1980–2016), identifying top platforms, genres, and regional preferences to support data-driven market decisions.

---

## 📌 Overview

This project analyzes historical video game sales data to uncover market trends, platform lifecycles, genre performance, and regional purchasing behavior. The analysis focuses on the 2006–2016 period as the most relevant window for forecasting future sales.

**Key business questions:**
- Which platforms and genres drive the most revenue?
- How do sales patterns differ across North America, Europe, and Japan?
- Do user and critic scores significantly differ between platforms and genres?

---

## 📊 Dataset

| Feature | Description |
|---|---|
| `name` | Game title |
| `platform` | Gaming platform (PS3, X360, Wii, etc.) |
| `year_of_release` | Release year |
| `genre` | Game genre |
| `na_sales` | North America sales (millions) |
| `eu_sales` | Europe sales (millions) |
| `jp_sales` | Japan sales (millions) |
| `other_sales` | Other regions sales (millions) |
| `critic_score` | Metacritic critic score (0–100) |
| `user_score` | User score (0–10) |
| `rating` | ESRB rating (E, T, M, etc.) |

- **Raw records:** 16,715
- **Analysis period:** 2006–2016 (10,333 games — 61.8% of dataset)

---

## 🔧 Methodology

### Data Preprocessing
- Standardized column names to snake_case
- Converted `user_score` from object to float (`'tbd'` → NaN via `pd.to_numeric`)
- Converted `year_of_release` to numeric
- Dropped rows with missing `year_of_release`, `rating`, `critic_score`, and `user_score`
- Engineered `total_sales` = sum of all regional sales columns

### Analysis Period Selection
- Focused on 2006–2016: captures the PS3/X360/Wii generation through PS4/XOne launch
- Avoids outdated sales patterns from earlier decades

### Hypothesis Testing
- **Test 1:** Xbox One vs PC user scores — independent t-test (two-tailed), α = 0.05
- **Test 2:** Action vs Sports user scores — independent t-test (two-tailed), α = 0.05

---

## 📈 Results

**Top Platforms by Total Sales (2006–2016)**

| Platform | Total Sales (M) | Peak Year | Status in 2016 |
|---|---|---|---|
| PS3 | 939.7 | 2011 | Declining |
| X360 | 971.4 | 2010 | Declining |
| Wii | 907.5 | 2009 | Virtually dead |
| DS | 806.1 | 2008 | Dead |
| **PS4** | **314.1** | 2015 | **Growing** ✅ |

**Top Genres by Revenue (2006–2016)**

| Genre | Total Sales (M) | Avg Sales/Game (M) |
|---|---|---|
| Action | 1,116.7 | 0.47 |
| Sports | 793.9 | 0.63 |
| Shooter | 717.0 | **0.97** |
| Role-Playing | 522.4 | 0.52 |

**Regional Preferences**

| Region | Top Platform | Top Genre |
|---|---|---|
| North America | X360 (588.8M) | Action |
| Europe | PS3 (327.2M) | Action |
| Japan | DS (141.5M) | Role-Playing |

**Hypothesis Tests**

| Test | H₀ | p-value | Result |
|---|---|---|---|
| Xbox One vs PC user scores | Scores are equal | 0.0144 | ✅ Rejected |
| Action vs Sports user scores | Scores are equal | < 0.0001 | ✅ Rejected |

---

## 🛠️ Tech Stack

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Wrangling-lightgrey)
![SciPy](https://img.shields.io/badge/SciPy-Statistics-blue)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-teal)

---

## 📁 Project Structure

```
video-game-sales-analysis/
│
├── notebook.ipynb       # Full analysis and hypothesis testing
├── README.md
└── .gitignore
```

---

## 🚀 How to Run

```bash
# Clone the repository
git clone https://github.com/laaurasaporski/video-game-sales-analysis.git

# Install dependencies
pip install pandas numpy scipy matplotlib seaborn

# Open the notebook
jupyter notebook notebook.ipynb
```

---

## 💡 Key Insights

- **PS4 is the only growing platform** in 2016 — strong candidate for future investment
- **Shooter games have the highest revenue per title** (0.97M avg) despite ranking 3rd in total sales
- **Japan is a unique market** — Role-Playing dominates over Action/Sports, and mature-rated (M) games underperform vs. other regions
- **Mature-rated games sell 1.59x more per title in NA and 1.91x more in EU** than E-rated games
- **PC users rate games significantly higher** than Xbox One users (avg +0.31 points, p = 0.014)
- **Action games are rated significantly higher** than Sports games (avg +0.46 points, p < 0.0001)
