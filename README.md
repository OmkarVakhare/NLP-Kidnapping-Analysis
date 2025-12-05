# NLP Kidnapping Statistics Analysis

## Project Overview
This project performs Natural Language Processing (NLP) analysis on Indian kidnapping and abduction statistics from 2016-2022, focusing on recovery rates across different demographics (gender and age groups).

## Dataset Description

### 1. Raw Dataset
**File**: `Child Victims - Recovery of Kidnapped and Abducted Persons Gender Age Group-wise.csv`
- **Source**: Official government statistics on child kidnapping cases in India
- **Time Period**: 2016-2022 (7 years)
- **Records**: 80 rows
- **Dimensions**: 12 columns
- **Coverage**: Gender (Male, Female, Total) × Age Groups (Below 6, 6-12, 12-16, 16-18 years)

### 2. Processed Dataset
**File**: `childvictimscleanwithtext.csv`
- **Records**: 72 rows (filtered to remove incomplete data)
- **Dimensions**: 20 columns (original + engineered features)
- **New Features**:
  - Text narratives generated from structured data
  - Recovery and unrecovered rates
  - Cleaned text for NLP analysis
  - Text length metrics

## Analysis Components

### 1. Data Cleaning & Preprocessing
- Column renaming for easier access
- Handling missing values
- Data type conversions
- Filtering incomplete records (Transgender category removed due to missing data)
- Data validation checks

### 2. Feature Engineering
- **Recovery Rate**: Proportion of kidnapped persons recovered (alive or dead)
- **Unrecovered Rate**: Proportion of kidnapped persons still unrecovered
- **Case Text**: Natural language descriptions generated from structured data
- **Text Cleaning**: Removing stopwords, punctuation, and preparing for NLP

### 3. Exploratory Data Analysis (EDA)
- Summary statistics by gender and age group
- Temporal trends (2016-2022)
- Recovery rate comparisons

### 4. Visualizations
- **Bar Charts**: Average recovery rates by gender and age group
- **Line Plots**: Recovery rate trends over time
- **Distribution Analysis**: Understanding data patterns

### 5. NLP Analysis
- Text generation from structured data
- Text preprocessing and cleaning
- TF-IDF vectorization
- Word frequency analysis
- Text length statistics

## Key Findings

- **Average Recovery Rate**: 52.15% (2016-2022)
- **Gender Differences**: Female children show different recovery patterns compared to male children
- **Age Group Impact**: Recovery rates vary significantly across age groups
- **Trend Analysis**: Year-over-year changes in kidnapping and recovery statistics

## Technologies Used

- **Python 3.x**
- **Pandas**: Data manipulation and analysis
- **NumPy**: Numerical computations
- **Matplotlib & Seaborn**: Data visualization
- **Re (Regex)**: Text processing
- **Jupyter Notebook**: Interactive development environment

## Project Structure

```
NLP-Kidnapping-Analysis/
│
├── NLP_New.ipynb                          # Main analysis notebook
├── README.md                               # Project documentation (this file)
└── DATA_DICTIONARY.md                      # Column definitions and descriptions
```

## How to Use

### Prerequisites
```bash
pip install pandas numpy matplotlib seaborn jupyter
```

### Running the Analysis

1. Clone the repository:
```bash
git clone https://github.com/OmkarVakhare/NLP-Kidnapping-Analysis.git
cd NLP-Kidnapping-Analysis
```

2. Launch Jupyter Notebook:
```bash
jupyter notebook NLP_New.ipynb
```

3. Run all cells to reproduce the analysis

## Data Sources

- Official Indian government statistics on child kidnapping and abduction cases
- Time period: Calendar Year (Jan-Dec) 2016-2022
- Aggregated at national level (India)

## Future Work

- [ ] Sentiment analysis on case descriptions
- [ ] Predictive modeling for recovery likelihood
- [ ] Geographic analysis (state-wise breakdown)
- [ ] Time series forecasting
- [ ] Advanced NLP techniques (word embeddings, topic modeling)
- [ ] Interactive dashboard development

## Author

**Omkar Vakhare**
- Location: Pune, MH
- GitHub: [@OmkarVakhare](https://github.com/OmkarVakhare)
- Email: ovakhare@gmail.com

## License

This project is available for educational and research purposes.

## Acknowledgments

- Data source: Indian government statistics portal
- Analysis conducted as part of data science portfolio development

---

*Last Updated: December 5, 2025*