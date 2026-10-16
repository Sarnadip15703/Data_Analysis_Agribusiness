# Agribusiness Data Analytics: 5-Week Virtual Internship Project

A five-week analytics project completed as a **Junior Data Analyst (Agribusiness) virtual internship with Yuva Intern**. It follows the full path from finding public agribusiness data, through cleaning, exploration, statistical testing and modelling, to a business report with strategic recommendations.

The main data source is India's district-level **Crop-Wise Area, Production and Yield (APY)** dataset (about 455,000 records, 1997 to 2023). A second, small farm-level dataset (50 farms) was used for statistical modelling.

## Headline findings

- **Aggregates mislead; segmented numbers work.** Pooled over all crops, mean yield is 69.6 t/ha but the median is 1.07, and the area-production correlation is 0.04. Within a single crop the correlation is 0.85 to 0.94. Analyses must be done per crop (and per state).
- **Data quality matters.** 5,009 records (1.1%) had unreported production recorded as zero yield. A naive outlier rule flagged 14.6% of records; per-crop rules flagged 3.21%.
- **Wheat productivity rose 43.2%** between 1997 and 2022 (1.90 to 2.73 t/ha, flagged records excluded).
- **The 2014-15 wheat shock was large and broad.** National production fell about 18.0 million tonnes (17.5%) with area almost unchanged. Uttar Pradesh accounts for about 64% of the net loss (74 of its 75 districts fell), and all major rabi crops in the state fell. External reports describe unseasonal rain and hail in March 2015, but the dataset has no weather variables, so the cause is a hypothesis, not a result.
- **Farm inputs did not predict yield in the 50-farm dataset.** Eight statistical tests were non-significant and a regression model scored worse than guessing the average on unseen farms (cross-validated R-squared of -0.137). This reflects a small, incomplete dataset, not proof that inputs do not matter.

## Project structure

| Week | Focus | Report | Notebook |
|---|---|---|---|
| 1 | Data landscape, sources, KPI framework | `Week1_Agribusiness_Data_Landscape.docx` | (research and planning) |
| 2 | Data cleaning and preparation | `Week2_Data_Cleaning_Agribusiness.docx` | `Week2_Data_Cleaning.ipynb` |
| 3 | Exploratory analysis and visualisation | `Week3_EDA_Agribusiness.docx` | `Week3_EDA.ipynb` |
| 4 | Statistical analysis and predictive modelling | `Week4_Statistical_Analysis_Agribusiness.docx` | `Week4_Statistical_Modeling.ipynb` |
| 5 | Business insights and strategic recommendations | `Week5_Business_Report_Agribusiness.docx` | `Week5_Supporting_Calculations.ipynb` |

```
.
├── README.md
├── reports/          # the five weekly reports (.docx)
├── notebooks/        # Jupyter notebooks, run in order Week 2 to Week 5
└── data/             # not committed; see "Data" below
```

## Data

Raw data files are **not included** in this repository. Download them from the sources below and place them in `data/`.

| Dataset | Source | Notes |
|---|---|---|
| Crop-Wise Area, Production and Yield (APY) | [India Data Portal](https://indiadataportal.com/p/area-production-yield-apy/r/moafw-area_production_yield-dt-sn-qzf) (Ministry of Agriculture and Farmers Welfare) | Open Data Commons Attribution License. File: `crop-wise-area-production-yield.csv` |
| Agriculture and Farming Dataset | [Kaggle](https://www.kaggle.com/datasets/bhadramohit/agriculture-and-farming-dataset) | 50 farms. Provenance is not documented and it may be simulated; check the licence on the dataset page. File: `agriculture_dataset.csv` |

Three further sources were identified in Week 1 but not analysed: FAOSTAT trade data, World Bank commodity price indices, and World Bank agriculture indicators. As a result, the findings concern yield and production, not prices or trade.

## How to run

1. Download the two datasets above into `data/`.
2. Install the requirements (the notebooks use `groupby(...).apply(..., include_groups=False)`, which needs **pandas 2.2 or newer**):
   ```bash
   pip install pandas numpy matplotlib scipy statsmodels scikit-learn jupyter
   ```
3. Open the notebooks in order. `Week2_Data_Cleaning.ipynb` cleans the APY data and saves `cleaned_apy_data.csv`, which the Week 3 and Week 5 notebooks load. The Week 4 notebook uses the Kaggle file.
4. File paths in the notebooks are relative to the notebook's own folder; adjust them if you store the data elsewhere.

## What each notebook reproduces

| Notebook | Main content |
|---|---|
| Week 2 | Missing-value, duplicate and outlier checks; per-crop IQR outlier flagging; `crop_failure` flag; export of the cleaned dataset |
| Week 3 | Summary statistics, per-crop distributions, correlation analysis, Wheat trend, Sugarcane low-yield investigation |
| Week 4 | Pearson correlations, one-way ANOVA with Levene's test, OLS regression, train/test and 5-fold cross-validation, VIF and residual checks |
| Week 5 | Flag totals, the 2014-15 wheat shock by state and district, other rabi crops, crop-mix test, Sugarcane shares by state, recovery after the shock |

## Method highlights

- **Diagnose before cleaning:** each data problem was inspected before it was fixed.
- **Flag, do not delete, when an extreme value may be real** (droughts, floods and bumper harvests are genuine events).
- **Segment before trusting an aggregate:** results were recomputed per crop and per state whenever a pooled number looked odd.
- **Validate on unseen data:** models were judged with repeated splits and cross-validation against a "guess the average" baseline, and unfavourable results are reported.

## Limitations

- Only two of the five Week 1 sources were analysed; there is no price, trade or supply-chain analysis.
- No weather variables: the explanation for the 2014-15 shock rests on external reports and the pattern in the data.
- District-level reported data cannot show differences between individual farms.
- The 50-farm dataset has little statistical power, and its origin is unknown.
- Findings are associations in observational data and do not establish cause.

## Note on revisions between weeks

The Week 3 report describes the 2014-15 wheat dip as concentrated in Uttar Pradesh and says the all-crop yield rise is "most likely" a crop-mix effect. Deeper checks done for Week 5 refined both points: the dip was broad across the northern wheat belt with Uttar Pradesh the largest contributor (about 64% of the net loss), and crop mix explains about 44% of the all-crop rise. **The Week 5 report and notebook contain the refined numbers.**

## Skills demonstrated

Python (pandas, NumPy, SciPy, statsmodels, scikit-learn, matplotlib) · data cleaning and validation · exploratory data analysis · hypothesis testing (correlation, ANOVA) · regression and model validation · translating analysis into business recommendations · technical report writing.

## Possible next steps

Join district weather data to test the weather hypothesis directly; analyse price and trade data for market-competitiveness insights; build per-crop trend and shock models with time-aware validation; verify the Sugarcane low-yield clusters against irrigation and unit conventions; collect a larger farm-level dataset with weather and soil variables.
