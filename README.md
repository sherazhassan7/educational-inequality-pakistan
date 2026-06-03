# Mapping and Predicting Educational Inequality in Pakistan: District-Level Evidence from ASER 2023

This repository contains the analysis code for a study of educational inequality between government and private schools across Pakistan, using data from the Annual Status of Education Report (ASER) 2023 survey. The analysis covers approximately 214,000 children across 150 districts and examines learning outcomes in arithmetic, Urdu reading, and English reading. All inferential estimates use cluster-robust (village-level) bootstrap confidence intervals to account for ASER's two-stage cluster sampling design.

## Research Questions

1. How large is the government-private school learning gap in arithmetic, Urdu, and English, and how does it vary by province, grade level, and gender?
2. What household and school characteristics predict the risk of a child dropping out before completing middle education?
3. Which districts show the widest and narrowest gaps, and do school operational metrics explain cross-district variation in the government-private gap?

## Key Findings

- The arithmetic gap between government and private school students is present from grade 1 and remains statistically robust at every national grade level; cluster-robust bootstrap confidence intervals exclude zero at every grade.
- Seventy-eight percent of observed dropouts occur in middle and secondary school (grades 6-10). School stage (middle or secondary) and education expenditure are the top predictors in the dropout risk model.
- Household electrification rate is the strongest district-level correlate of absolute government school arithmetic scores (r = 0.42).
- Mean pupil-teacher ratio in government schools (28.1) is approximately 60 percent higher than in private schools (17.6), after excluding recorded ratios above 100:1 as data errors. Medians follow the same direction (24.8 vs 15.9). Teacher attendance in government schools is approximately 7 percentage points lower than in private schools.
- Textbook availability in government Grade 2 classrooms averages 17.9 percent nationally; Punjab government schools average 35.7 percent, more than double the national figure.
- Twelve districts (11 in Punjab, 1 in KPK) show a statistically significant government school advantage over private schools under bootstrap testing. Six of these also exceed national government-school benchmarks on three or more operational resource metrics.

## Notebooks

| Notebook | Description |
|---|---|
| `01_gap_by_grade.ipynb` | Government-private arithmetic gap by grade and province; line charts and filtered views |
| `02_sample_size_check.ipynb` | Sample size audit and coverage heatmap across provinces and grades |
| `03_district_rankings.ipynb` | District-level gap rankings; top-30 widest and bottom-15 narrowest gaps |
| `04_socioeconomic_correlations.ipynb` | SES correlates of learning outcomes: electricity access, asset index, BISP/Ehsaas receipt |
| `05_competency_rates.ipynb` | Proficiency rates by school type: story reading, sentence reading, division, subtraction |
| `06_school_resources.ipynb` | School resource metrics by type and province: PTR, attendance rates, classroom resources |
| `07_dropout_model.ipynb` | Logistic regression and gradient boosting dropout risk model with provincial coefficients |
| `08_district_outlier_check.ipynb` | Data quality audit and outlier flagging at the district level |
| `09_grade_gap_bootstrap.ipynb` | Grade-by-grade arithmetic gap with cluster-robust bootstrap CIs; gender delta test |
| `10_dropout_robustness.ipynb` | Robustness checks for the dropout risk model across subsamples and specifications |
| `11_bisp_diagnosis.ipynb` | BISP/Ehsaas transfer coverage and its relationship to district learning outcomes |
| `12_distributional_views.ipynb` | Score distributions and within-school-type inequality by province |
| `13_punjab_verification.ipynb` | Bootstrap verification of government school advantage in 12 districts; resource metric check |
| `14_punjab_textbook_check.ipynb` | Punjab-specific textbook availability by district; comparison with national government benchmarks |
| `15_cluster_bootstrap.ipynb` | District-level cluster-robust bootstrap CIs; top-10 and bottom-15 gap tables |

## Data

The raw ASER 2023 data files are not redistributed in this repository (ITA licence). They must be obtained directly from ASER Pakistan: [aserpakistan.org](https://aserpakistan.org).

Once obtained, place the pre-processed CSV files in `Data:/` (the folder name includes a trailing colon, which is literal):

```
Data:/child_merged.csv
Data:/district_summary.csv
Data:/grade_level_gaps.csv
Data:/school_resources.csv
```

Notebooks 09 and 15 additionally load village codes from the raw ASER child-level Excel file. The default path is `../data/raw/ITAASER2023Child.xlsx`. Override it by setting the `ASER_CHILD_XLSX` environment variable before launching Jupyter:

```bash
export ASER_CHILD_XLSX=/path/to/ITAASER2023Child.xlsx
```

## Setup

Requires Python 3.9 or later.

```bash
git clone https://github.com/sherazhassan7/educational-inequality-pakistan.git
cd educational-inequality-pakistan
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook
```

## License

MIT License. See [LICENSE](LICENSE).
