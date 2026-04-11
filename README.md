# A/B Testing: Facebook Ads vs. Google AdWords 

A data-driven comparison of two digital advertising platforms — **Facebook Ads** and **Google AdWords** — across a full calendar year (January–December 2019). The project applies statistical and machine learning techniques to determine which platform delivers superior conversion performance.

---

## Project Structure

```
A-B-TESTING/
├── main.ipynb               # Main analysis notebook
├── marketing_campaign.csv   # Dataset
└── README.md
```

---

## Dataset

**File:** `marketing_campaign.csv`  
**Rows:** 365 (one per day in 2019)  
**Columns:** 17

The dataset tracks daily performance metrics for two parallel ad campaigns:

| Column | Description |
|---|---|
| `Date` | Calendar date (2019-01-01 to 2019-12-31) |
| `Facebook Ad Campaign` | Monthly campaign label (e.g., FB_Jan19) |
| `Facebook Ad Views` | Number of ad impressions |
| `Facebook Ad Clicks` | Number of clicks on the ad |
| `Facebook Ad Conversions` | Number of resulting conversions |
| `Cost per Facebook Ad` | Daily spend on Facebook |
| `Facebook Click-Through Rate` | Clicks / Views |
| `Facebook Conversion Rate` | Conversions / Clicks |
| `Facebook Cost per Click` | Ad cost / Clicks |
| `AdWords Ad Campaign` | Monthly AdWords campaign label |
| `AdWords Ad Views` | Number of ad impressions |
| `AdWords Ad Clicks` | Number of clicks |
| `AdWords Ad Conversions` | Number of resulting conversions |
| `Cost per AdWords Ad` | Daily spend on AdWords |
| `AdWords Click-Through Rate` | Clicks / Views |
| `AdWords Conversion Rate` | Conversions / Clicks |
| `AdWords Cost per Click` | Ad cost / Clicks |

---

## Analysis Overview (`main.ipynb`)

### 1. Exploratory Data Analysis
- Loaded and inspected the dataset (shape, dtypes, descriptive statistics)
- Converted `Date` column to `datetime` format
- Key summary stats:
  - **Facebook** avg. conversions: **11.74 / day** | avg. clicks: **44.05 / day**
  - **AdWords** avg. conversions: **5.98 / day** | avg. clicks: **60.38 / day**

### 2. Campaign Performance Comparison
- Distribution plots for clicks and conversions (histograms with KDE)
- Conversion category breakdown (< 6, 6–10, 10–15, > 15 per day)
- Grouped bar chart comparing Facebook vs. AdWords across conversion categories
- Scatter plots showing clicks vs. conversions for each platform

### 3. Correlation Analysis
| Platform | Clicks ↔ Conversions Correlation |
|---|---|
| Facebook | **0.87** (strong positive) |
| AdWords | **0.45** (moderate positive) |

### 4. Hypothesis Testing (Two-Sample Welch's t-test)
- **H₀:** Mean daily conversions are equal across platforms
- **H₁:** Mean daily conversions differ between platforms
- **Result:** T-statistic = 32.88 | p-value ≈ 9.35 × 10⁻¹³⁴
- **Conclusion:** Reject H₀ — Facebook Ads produce significantly more conversions

### 5. Regression Analysis (Facebook Ads)
- Linear regression: Facebook Ad Clicks → Facebook Ad Conversions
- **R² Score:** 76.35%
- **MSE:** 2.02
- **Predictions:**
  - 50 clicks → ~13 conversions
  - 80 clicks → ~19.31 conversions

### 6. Facebook Campaign Temporal Analysis
- **Weekly conversions:** Identified peak/off-peak days of the week
- **Monthly conversions:** Tracked seasonal trends across 12 months
- **Monthly Cost Per Conversion (CPC):** Monitored spend efficiency over time

### 7. Cointegration Test (Cost vs. Conversions)
- **Score:** −14.76 | **p-value:** 2.13 × 10⁻²⁶
- **Conclusion:** Ad spend and conversions are cointegrated — increased spending consistently drives more conversions

---

## Key Findings

- **Facebook Ads significantly outperform AdWords** in daily conversions (~2× higher on average)
- The performance gap is statistically significant (p < 0.001) and not due to random variation
- Facebook shows a **much stronger relationship** between clicks and conversions (r = 0.87 vs. 0.45)
- Ad spend on Facebook has a **stable long-term relationship** with conversions, making it a reliable platform for scaling investment
- **Recommendation:** Prioritize Facebook Ads to maximize marketing ROI

---

## Tech Stack

| Library | Purpose |
|---|---|
| `pandas` | Data loading and manipulation |
| `numpy` | Numerical operations |
| `matplotlib` | Data visualization |
| `seaborn` | Statistical plots |
| `scipy.stats` | Hypothesis testing (t-test) |
| `sklearn` | Linear regression, R² / MSE evaluation |
| `statsmodels` | Seasonal decomposition, cointegration test |

---

## Getting Started

```bash
# Clone the repository
git clone <your-repo-url>
cd A-B-TESTING

# (Optional) Create and activate a virtual environment
python -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate

# Install dependencies
pip install pandas numpy matplotlib seaborn scipy scikit-learn statsmodels

# Launch the notebook
jupyter notebook main.ipynb
```

---

## License

This project is open-source and available under the [MIT License](LICENSE).
