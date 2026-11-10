# Workforce Capacity Loss Prediction

Predicting which employees are likely to leave, so operations can plan cover **before** capacity drops.

**Stack:** Python (pandas, scikit-learn, XGBoost) · PostgreSQL (SQL) · SQLAlchemy · Power BI

---

## Business Question
Which teams are losing capacity fastest, what is driving it, and which employees should managers act on first?

## Approach
| Step | Tool | What was done |
|---|---|---|
| 1. Data cleaning | Python (pandas) | Cleaned a messy 1,544-row, 37-column HR dataset: fixed 77 mislabelled attrition records, dropped 5 zero-value columns, imputed missing hire dates, corrected data types, produced a data quality report |
| 2. Analysis | PostgreSQL (SQL) | Loaded clean data into PostgreSQL; analysed attrition by department, job role, job level, overtime, salary and tenure |
| 3. Risk model | Python (scikit-learn, XGBoost) | Compared 3 classifiers on 14 selected features (gender excluded); scored every employee Low / Medium / High risk |
| 4. Reporting | Power BI | Capacity loss dashboard |

## Key Findings
- Overall attrition: **20.6%** (318 of 1,544 employees)
- Employees working overtime leave at **34.3% vs 15.2%**, which is 2.2x higher
- Entry-level (Job Level 1) attrition: **30.4%**
- Sales (24.5%) and HR (24.1%) lose staff faster than R&D (18.9%)

## Model Comparison
| Model | Accuracy | Leavers Caught (Recall) | False Alarms |
|---|---|---|---|
| Logistic Regression | 65.7% | **60.9%** | 81 |
| Random Forest | 81.2% | 31.2% | 14 |
| XGBoost | 77.3% | 50.0% | 38 |

Recall was prioritised over accuracy: missing a leaver costs far more than a false alarm. Random Forest looks best on accuracy but misses ~69% of leavers.

## Business Impact
- **363** employees flagged high-risk
- Estimated replacement cost: **$38,425** per leaver (about 6 months' salary)
- Maximum exposure if none are retained: **$13.9M**

## Recommendations
1. Rebalance overtime in high-overtime teams, the strongest single driver
2. Focus retention effort on entry-level Sales staff
3. Re-score monthly and review high-risk employees with team leads to plan cover early

## Files
| File | Purpose |
|---|---|
| `People Analytics - Data Cleaning.ipynb` | Cleaning and data quality report |
| `People Analytics - EDA.ipynb` | SQL analysis via PostgreSQL |
| `People Analytics - ML Algorithms.ipynb` | Models, risk scoring, cost impact |
| `Capacity Loss Prediction.pbix` | Power BI dashboard |

## Data
IBM HR Analytics Employee Attrition dataset, with injected data quality issues to simulate real HR system exports.
