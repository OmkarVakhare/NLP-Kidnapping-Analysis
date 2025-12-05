# Data Dictionary

Comprehensive documentation of all columns in the kidnapping statistics datasets.

---

## Raw Dataset Columns
**File**: `Child Victims - Recovery of Kidnapped and Abducted Persons Gender Age Group-wise.csv`

| Column Name | Data Type | Description | Example Values |
|-------------|-----------|-------------|----------------|
| **Country** | Object (String) | Country name | "India" |
| **Year** | Object (String) | Calendar year period | "Calendar Year Jan - Dec, 2022" |
| **Gender** | Object (String) | Gender category of victims | "Male", "Female", "Total" |
| **Age Group** | Object (String) | Age range of victims | "Below 6 Years", "6 Years to 12 Years", "12 Years to 16 Years", "16 Years to 18 Years" |
| **Unrecovered Victims Of Kidnapping And Abduction From Previous Years (UOM:Number, Scaling Factor:1)** | Integer | Number of unrecovered victims carried forward from previous year | 14180, 22217, 3077 |
| **Victims Kidnapped And Abducted During The Year (UOM:Number, Scaling Factor:1)** | Integer | New kidnapping cases reported during the year | 21451, 37429, 2807 |
| **All Kidnapped And Abducted (UOM:Number, Scaling Factor:1)** | Integer | Total kidnapped persons (previous unrecovered + new cases) | 35631, 59646, 5884 |
| **Victims Recovered Alive (UOM:Number, Scaling Factor:1)** | Integer | Number of victims recovered alive | 21351, 39033, 2656 |
| **Victims Recovered Dead (UOM:Number, Scaling Factor:1)** | Integer | Number of victims recovered dead | 152, 407, 21 |
| **Recovered Dead And Alive (UOM:Number, Scaling Factor:1)** | Integer | Total recovered victims (alive + dead) | 21503, 39440, 2677 |
| **Percentage Recovery (UOM:Percentage, Scaling Factor:1)** | Float | Recovery percentage | 60.3, 66.1, 45.5 |
| **Unrecovered Kidnapped And Abducted Persons (UOM:Number, Scaling Factor:1)** | Integer | Number of victims still unrecovered at year end | 14128, 20206, 3207 |

---

## Processed Dataset Columns
**File**: `childvictimscleanwithtext.csv`

### Original Columns (Renamed)

| Column Name | Data Type | Description | Example Values |
|-------------|-----------|-------------|----------------|
| **Country** | Object (String) | Country name | "India" |
| **Gender** | Object (String) | Gender category | "Male", "Female", "Total" |
| **Age Group** | Object (String) | Age range category | "12 Years to 16 Years", "Below 6 Years" |
| **unrecovered_prev_year** | Integer | Unrecovered victims from previous year | 14180, 3940 |
| **kidnapped_during_year** | Integer | New kidnapping cases in current year | 21451, 5814 |
| **all_kidnapped** | Integer | Total kidnapped (prev + current year) | 35631, 9754 |
| **recovered_alive** | Integer | Victims recovered alive | 21351, 5587 |
| **recovered_dead** | Integer | Victims recovered dead | 152, 81 |
| **recovered_total** | Integer | Total recovered (alive + dead) | 21503, 5668 |
| **pct_recovery** | Float | Official percentage recovery | 60.3, 58.1 |
| **unrecovered_total** | Integer | Total still unrecovered | 14128, 4086 |
| **year** | Integer | Calendar year (extracted from original) | 2022, 2021, 2020, 2019, 2018, 2017, 2016 |

### Engineered Features

| Column Name | Data Type | Description | Formula | Example Values |
|-------------|-----------|-------------|---------|----------------|
| **case_text** | Object (String) | Natural language description generated from data | Template: "In {year}, for {gender} children aged {age_group}, there were {all_kidnapped} kidnapped cases with a recovery percentage of {pct_recovery}." | "In 2022, for female children aged 12 years to 16 years, there were 35631 kidnapped cases with a recovery percentage of 60.3." |
| **recovery_rate** | Float | Calculated recovery rate (proportion) | `recovered_total / all_kidnapped` | 0.603491, 0.661235, 0.454963 |
| **unrecovered_rate** | Float | Calculated unrecovered rate (proportion) | `unrecovered_total / all_kidnapped` | 0.396509, 0.338765, 0.545037 |
| **check_all_kidnapped** | Integer | Validation: sum of unrecovered_prev_year + kidnapped_during_year | `unrecovered_prev_year + kidnapped_during_year` | Should match `all_kidnapped` |
| **check_recovered_total** | Integer | Validation: sum of recovered_alive + recovered_dead | `recovered_alive + recovered_dead` | Should match `recovered_total` |
| **check_pct** | Float | Validation: calculated percentage | `100 * (recovered_total / all_kidnapped)` | Should approximately match `pct_recovery` |
| **case_text_clean** | Object (String) | Cleaned text with stopwords removed | Lowercase, tokenized version of case_text | "female children aged years years kidnapped cas..." |
| **text_len** | Integer | Number of words in cleaned text | Word count of `case_text_clean` | 9, 8 |

---

## Data Quality Notes

### Filtering Applied
- **Transgender Category Removed**: Rows with Gender="Transgender" were removed due to:
  - All zero counts (no cases reported)
  - Missing `pct_recovery` values
  - After filtering: 72 rows (from original 80)

### Data Validation
- **check_all_kidnapped**: All 72 rows pass validation (True)
- **check_recovered_total**: All 72 rows pass validation (True)
- **check_pct**: 48 rows match exactly, 24 rows have minor rounding differences

### Missing Values
- Original dataset: 8 missing values in `Percentage Recovery` column (Transgender rows)
- Processed dataset: No missing values after filtering

---

## Statistical Summary

### Numeric Columns (Processed Dataset, n=72)

| Statistic | unrecovered_prev_year | kidnapped_during_year | all_kidnapped | recovered_total | recovery_rate |
|-----------|----------------------|----------------------|---------------|-----------------|---------------|
| **Mean** | 6,766 | 10,851 | 17,618 | 10,177 | 0.522 (52.2%) |
| **Std Dev** | 6,855 | 12,096 | 18,892 | 11,577 | 0.076 (7.6%) |
| **Min** | 649 | 412 | 1,092 | 420 | 0.361 (36.1%) |
| **25%** | 1,732 | 1,850 | 3,750 | 1,710 | 0.459 (45.9%) |
| **50%** | 3,843 | 5,086 | 9,136 | 4,635 | 0.519 (51.9%) |
| **75%** | 11,886 | 21,198 | 33,311 | 18,204 | 0.586 (58.6%) |
| **Max** | 26,248 | 43,206 | 69,454 | 44,908 | 0.661 (66.1%) |

---

## Categorical Columns

### Gender Distribution
- **Female**: 24 rows (33.3%)
- **Male**: 24 rows (33.3%)
- **Total**: 24 rows (33.3%)

### Age Group Distribution
- **12 Years to 16 Years**: 18 rows (25.0%)
- **16 Years to 18 Years**: 18 rows (25.0%)
- **6 Years to 12 Years**: 18 rows (25.0%)
- **Below 6 Years**: 18 rows (25.0%)

### Year Distribution
- Each year (2016-2022): Balanced representation
- **2022**: 12 rows
- **2021**: 12 rows
- **2020**: 12 rows
- **2019**: 12 rows
- **2018**: 12 rows
- **2017**: 12 rows
- **2016**: 12 rows

---

## Usage Notes

### For Analysis
1. Use **processed dataset** for most analyses (cleaner, more features)
2. Use **raw dataset** only if you need original column names or all categories
3. **recovery_rate** is more accurate than **pct_recovery** (some have >100% due to data entry issues)

### For NLP
- **case_text**: Use for initial text analysis
- **case_text_clean**: Use for word frequency, TF-IDF, and modeling
- **text_len**: Use for text complexity analysis

### For Visualization
- Filter by **Gender** for gender-specific analysis
- Group by **Age Group** for age-based comparisons
- Plot **year** on x-axis for temporal trends

---

*Last Updated: December 5, 2025*