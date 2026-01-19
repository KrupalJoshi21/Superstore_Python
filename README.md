# 📊 Superstore Sales Analysis - SQL + Python Integration

**Author:** Krupal Joshi | **Role:** Data Analyst | **Date:** December 2025

---

## 📌 Project Overview

This project demonstrates **full-stack data analysis** combining SQL for data extraction and transformation with Python for advanced analysis and visualization. The workflow showcases professional data pipeline development: query → extract → transform → analyze → visualize → present insights.

**Business Problem:** How can we build a scalable, reproducible data pipeline that extracts actionable insights from complex transactional databases?

**Technical Problem:** How can SQL and Python work together efficiently for enterprise-grade data analysis?

---

## 🎯 Project Architecture

```
Raw Database (SQL Server/SQLite)
    ↓
Data Extraction (SQL Queries)
    ↓
Data Cleaning & Transformation (Python/Pandas)
    ↓
Analysis & Aggregation (Python/NumPy)
    ↓
Visualization & Insights (Matplotlib/Seaborn)
    ↓
Business Recommendations
```

---

## 📂 File Structure

```
04-SuperstoreSalesAnalysis-SQLPython/
├── README.md (this file)
├── notebooks/
│   ├── 01_sql_data_extraction.ipynb
│   ├── 02_data_pipeline.ipynb
│   ├── 03_advanced_analysis.ipynb
│   └── 04_insights_reporting.ipynb
├── sql_queries/
│   ├── 01_data_quality_checks.sql
│   ├── 02_customer_segmentation.sql
│   ├── 03_profitability_analysis.sql
│   ├── 04_product_performance.sql
│   ├── 05_regional_analysis.sql
│   └── 06_temporal_trends.sql
├── data/
│   ├── raw_exports/ (CSV from SQL queries)
│   └── processed_data/ (cleaned by Python)
├── outputs/
│   ├── visualizations/
│   ├── reports/
│   └── dashboards/
└── documentation/
    └── pipeline_documentation.md
```

---

## 🔧 Technical Skills Demonstrated

### SQL Skills
✅ **Data Quality & Validation**
- NULL detection and handling
- Duplicate identification using ROW_NUMBER()
- Data type validation and conversion
- Range and constraint checking

✅ **Complex Queries**
- Multi-table JOINs (INNER, LEFT, FULL)
- Window Functions (ROW_NUMBER, RANK, LAG, LEAD)
- Common Table Expressions (CTEs)
- Subqueries and nested aggregations
- Date/time functions and calculations

✅ **Business Logic Implementation**
- Customer segmentation (RFM scoring)
- Profitability calculations (Revenue - Cost)
- Sales trend analysis
- Cohort analysis
- Parametric query design

✅ **Query Optimization**
- Indexing strategies
- Query execution planning
- Query performance tuning
- Efficient joins and grouping

### Python Skills
✅ **Data Pipeline Development**
- Loading data from multiple sources
- Connecting to databases via SQLAlchemy
- Data validation and sanity checks
- Error handling and logging
- Reproducible data workflows

✅ **Data Transformation (Pandas)**
- DataFrame merging and joining
- Complex grouping and aggregations
- Feature engineering
- Data reshaping (melt, pivot)
- Missing value imputation

✅ **Statistical Analysis**
- Descriptive statistics
- Distribution analysis
- Correlation and covariance
- Statistical testing
- Outlier detection

✅ **Visualization (Matplotlib/Seaborn)**
- Multi-panel dashboards
- Time series analysis plots
- Distribution visualizations
- Relationship heatmaps
- Custom styling and formatting

✅ **Reproducibility**
- Configuration files
- Parametrized notebooks
- Documentation and comments
- Version control friendly code

---

## 🚀 SQL-Python Workflow

### Workflow Phase 1: SQL Data Extraction
**Objective:** Extract clean, aggregated data from database

```sql
-- SQL queries extract data pre-aggregated
-- This reduces data volume and processing time
-- Example: Aggregate 10M rows to 1K customer summaries
```

**Key Queries:**
1. **01_data_quality_checks.sql** - Validate source data
2. **02_customer_segmentation.sql** - Create customer RFM scores
3. **03_profitability_analysis.sql** - Calculate margins by dimension
4. **04_product_performance.sql** - Rank products by revenue/profit
5. **05_regional_analysis.sql** - Comparative regional metrics
6. **06_temporal_trends.sql** - Time-series data preparation

### Workflow Phase 2: Python Data Pipeline
**Objective:** Load SQL outputs, validate, transform, enrich

```python
# Load SQL outputs
df_customers = pd.read_csv('sql_outputs/customers.csv')
df_transactions = pd.read_csv('sql_outputs/transactions.csv')

# Validate data
assert df_customers.shape[0] > 0
assert df_transactions['amount'].dtype == 'float64'

# Transform and enrich
df_analysis = transform_pipeline(df_customers, df_transactions)

# Export for analysis
df_analysis.to_csv('processed_data/analysis_ready.csv')
```

### Workflow Phase 3: Analysis & Insights
**Objective:** Discover patterns, calculate metrics, generate findings

```python
# Pareto analysis
top_20 = df_customers.nlargest(int(len(df)*0.2), 'revenue')
print(f"Top 20% revenue: {top_20['revenue'].sum()}")

# Profitability trends
profit_by_region = df.groupby('region')['profit'].agg(['sum', 'mean', 'count'])

# Discount impact
df['margin'] = (df['profit'] / df['sales']).fillna(0)
discount_impact = df.groupby('discount_tier')['margin'].mean()
```

### Workflow Phase 4: Visualization & Reporting
**Objective:** Create publication-quality visuals and reports

```python
# Create 4-panel dashboard
fig, axes = plt.subplots(2, 2, figsize=(14, 10))

# Panel 1: Revenue trends
axes[0, 0].plot(df_time['date'], df_time['revenue'])

# Panel 2: Regional performance
df_region.plot(kind='bar', ax=axes[0, 1])

# Panel 3: Profit margin by category
axes[1, 0].barh(df_cat['category'], df_cat['margin'])

# Panel 4: Customer value distribution
axes[1, 1].hist(df['customer_value'], bins=50)

plt.tight_layout()
plt.savefig('outputs/dashboard.png', dpi=300)
```

---

## 📊 SQL Queries Explained

### Query 1: Data Quality Checks
```sql
-- Identifies data issues in source tables
-- Checks: NULLs, duplicates, ranges, type consistency
-- Output: Quality metrics and problem records
```

**Use Cases:**
- Validate data before analysis
- Document data quality issues
- Flag records requiring manual review

**Sample Output:**
```
Quality Report:
- Total records: 9,994
- NULL values: 23 (0.2%)
- Duplicates: 5
- Date range issues: 0
- Revenue range: $10 - $4,000 ✓
```

### Query 2: Customer Segmentation (RFM)
```sql
-- Segments customers using RFM (Recency, Frequency, Monetary)
-- Calculates:
--   Recency: Days since last purchase
--   Frequency: Number of transactions
--   Monetary: Total spending
-- Assigns quintile scores 1-5 for each metric
```

**Use Cases:**
- Identify VIP customers
- Find at-risk customers
- Segment for targeted marketing

**Sample Output:**
```
Customer_ID | Recency | Frequency | Monetary | RFM_Score
C001        | 2       | 5         | 5        | 555 (VIP)
C002        | 4       | 2         | 2        | 422 (At-Risk)
C003        | 1       | 4         | 4        | 144 (New High-Value)
```

### Query 3: Profitability Analysis
```sql
-- Calculates profit metrics by multiple dimensions
-- Breaks down: Total, by category, by region, by segment
-- Includes: Revenue, Cost, Profit, Margin %
```

**Use Cases:**
- Identify loss-leading products
- Compare profitability by region
- Find margin trends

**Sample Output:**
```
Category      | Revenue  | Profit  | Margin%
Technology    | $836,000 | $145,000| 17.3%
Furniture     | $742,000 | $18,000 | 2.4%
Office Supply | $719,000 | $122,000| 17.0%
LOSS LEADER:
Tables        | $207,000 | -$17,700| -8.6% ⚠️
```

### Query 4: Product Performance
```sql
-- Ranks products by revenue and profitability
-- Identifies top performers and underperformers
-- Calculates growth and trends
```

**Use Cases:**
- Inventory management (stock top items)
- Pricing optimization (fix loss leaders)
- Marketing focus (promote top sellers)

**Sample Output:**
```
Rank | Product     | Category | Revenue | Profit | Units | Margin
1    | Phone       | Tech     | $330K   | $45K   | 8,500 | 13.5%
2    | Chair       | Furn     | $328K   | $27K   | 22,000| 8.1%
...
N    | Table       | Furn     | $207K   | -$18K  | 850   | -8.6%
```

### Query 5: Regional Analysis
```sql
-- Comparative analysis across 4 US regions
-- Metrics: Revenue, Growth %, Profit, Margin
-- Identifies regional performance gaps
```

**Use Cases:**
- Identify high-performing regions
- Find improvement opportunities
- Resource allocation decisions

**Sample Output:**
```
Region  | Revenue | Growth% | Profit | Margin | Performance
West    | $725K   | 14.2%   | $108K  | 14.9%  | ⭐⭐⭐⭐⭐
East    | $679K   | 9.8%    | $91K   | 13.5%  | ⭐⭐⭐⭐
South   | $392K   | 3.2%    | $46K   | 11.9%  | ⭐⭐
Central | $501K   | 2.1%    | $39K   | 7.9%   | ⭐
```

### Query 6: Temporal Trends
```sql
-- Time-series data for trend analysis
-- Aggregations: Daily, Weekly, Monthly, Quarterly, Yearly
-- Includes: Revenue, Orders, Customer counts
```

**Use Cases:**
- Identify seasonal patterns
- Forecast future demand
- Detect anomalies

**Sample Output:**
```
Month   | Revenue | Orders | Customers | Trend
Jan-14  | $150K   | 850    | 200       |
Feb-14  | $145K   | 810    | 195       | ↓
...
Dec-14  | $210K   | 1,200  | 350       | ↑ (Q4 Peak!)
```

---

## 🎯 Key Findings from SQL+Python Pipeline

### Finding 1: Pareto Principle Confirmed
**SQL Query Used:** Customer RFM segmentation  
**Python Analysis:** Cumulative revenue distribution  
**Result:** Top 20% customers = $1.84M of $2.30M (80.4% of revenue)

**Business Impact:**
- Focus retention efforts on top 159 customers
- Implement VIP program with premium support
- Expected loyalty improvement: 5-10%

### Finding 2: Discount Profitability Trap
**SQL Query Used:** Profit calculation with discount breakdown  
**Python Analysis:** Correlation & regression analysis  
**Result:** Each 10% discount ≈ 2.5% margin reduction

**Quantified Impact:**
- Current avg discount: 16%
- Estimated margin loss: $50K annually
- **Recommendation:** Cap at 10%, save $30-50K

### Finding 3: Loss-Leading Products
**SQL Query Used:** Product profitability by category  
**Python Analysis:** Category and sub-category aggregation  
**Result:** Tables ($207K revenue but -$18K loss), Bookcases (-$3.5K loss)

**Business Impact:**
- Discontinue or reprice Tables
- Expected profit improvement: $20K+

### Finding 4: Regional Performance Gap
**SQL Query Used:** Regional revenue/profit breakdown  
**Python Analysis:** Statistical comparison, gap analysis  
**Result:** West region 85% higher profit than South

**Business Opportunity:**
- Apply West strategies to South/Central
- Expected growth: 20-30% in underperformers

### Finding 5: Seasonal Peak in Q4
**SQL Query Used:** Monthly/quarterly revenue trends  
**Python Analysis:** Time-series decomposition  
**Result:** Q4 revenue 35% above annual average

**Operational Impact:**
- Stock 3x inventory Oct-Nov
- Launch Q4 marketing in September
- Prepare logistics for surge

### Finding 6: Segment Profitability Variation
**SQL Query Used:** Segment-based profitability  
**Python Analysis:** Segment comparison  
**Result:** Home Office 14.2% margin > Consumer 12.3% margin

**Growth Strategy:**
- Expand Home Office focus (better margins)
- Grow segment through targeted campaigns
- Expected margin improvement: 1-2%

---

## 📊 Key Metrics Dashboard

```
OVERALL PERFORMANCE
├─ Total Revenue:      $2,297,200
├─ Total Profit:       $286,397
├─ Profit Margin:      12.4%
└─ Year-over-Year:     +11.4%

CUSTOMER METRICS
├─ Total Customers:    793
├─ Repeat Rate:        23%
├─ Avg Customer Value: $2,896
└─ Top 20% Value:      $11,542

PROFITABILITY BY CATEGORY
├─ Technology:         17.4% margin ✓
├─ Office Supply:      17.0% margin ✓
├─ Furniture:          2.5% margin ⚠️
├─ Tables:             -8.6% margin ❌
└─ Bookcases:          -3.0% margin ❌

REGIONAL PERFORMANCE
├─ West:               14.9% margin ⭐
├─ East:               13.5% margin
├─ South:              11.9% margin
└─ Central:            7.9% margin ⚠️

DISCOUNT IMPACT
├─ Avg Discount:       16%
├─ No Discount Margin: 18%
├─ 20%+ Discount:      -5% margin ❌
└─ Annual Loss:        $50K+ ⚠️
```

---

## 🚀 How to Run the Pipeline

### Prerequisites
```bash
# Install required packages
pip install pandas numpy matplotlib seaborn sqlalchemy jupyter
```

### Step 1: Setup SQL Connection
```python
from sqlalchemy import create_engine

# SQLite (local)
engine = create_engine('sqlite:///superstore.db')

# SQL Server
engine = create_engine('mssql+pyodbc://server/database')
```

### Step 2: Run SQL Queries
```python
# Load SQL query
with open('sql_queries/01_data_quality_checks.sql', 'r') as f:
    query = f.read()

# Execute and get results
df_quality = pd.read_sql(query, engine)
print(df_quality)
```

### Step 3: Run Notebooks Sequentially
```bash
jupyter notebook notebooks/01_sql_data_extraction.ipynb
jupyter notebook notebooks/02_data_pipeline.ipynb
jupyter notebook notebooks/03_advanced_analysis.ipynb
jupyter notebook notebooks/04_insights_reporting.ipynb
```

### Step 4: Generate Reports
```python
# Reports auto-generate in outputs/
# Check:
# - outputs/visualizations/
# - outputs/reports/
# - outputs/dashboards/
```

---

## 📈 SQL-Python Integration Advantages

| Aspect | SQL Only | Python Only | SQL+Python | Winner |
|--------|----------|------------|-----------|--------|
| **Data Volume** | 1M rows | Struggles | Efficient | ✓ SQL+Python |
| **Aggregation** | Fast | Slow | Fast+Flexible | ✓ SQL+Python |
| **Visualization** | None | Excellent | Excellent | ✓ SQL+Python |
| **Reproducibility** | Good | Good | Excellent | ✓ SQL+Python |
| **Scalability** | Better | Limited | Better | ✓ SQL+Python |
| **Maintenance** | Version control | Files | Version control | ✓ SQL+Python |

---

## 💡 When to Use Each Technology

### Use SQL for:
✅ Large datasets (1M+ rows)
✅ Complex aggregations
✅ Data quality validation
✅ Recurring extractions
✅ Data warehouse queries
✅ Join operations

### Use Python for:
✅ Statistical analysis
✅ Complex transformations
✅ Machine learning
✅ Visualization
✅ Ad-hoc exploration
✅ Report generation

### Use SQL+Python for:
✅ Enterprise analytics
✅ Scalable pipelines
✅ Reproducible analysis
✅ Large + complex analysis
✅ Production workflows
✅ Data science projects

---

## 🎓 Interview Questions You Can Answer

**"Describe a time you integrated SQL and Python"**
→ Walk through this pipeline: Extract with SQL → Transform with Python → Analyze & Visualize

**"How do you optimize data pipelines?"**
→ Pre-aggregate in SQL (10M → 100K rows) → Process quickly in Python

**"Tell me about your largest data project"**
→ 10K transactions, 6 SQL queries, discovered $50K savings opportunity

**"How do you ensure reproducibility?"**
→ SQL queries in version control + Jupyter notebooks + parameterized code

**"Describe your approach to data quality"**
→ SQL validation queries first → Python sanity checks → Flag issues before analysis

**"How would you architect a data pipeline for production?"**
→ Explain: SQL extraction → Python ETL → Database load → BI visualization

---

## 📚 Advanced SQL Concepts Demonstrated

| Concept | Query | Use Case |
|---------|-------|----------|
| **ROW_NUMBER()** | Customer Segmentation | Ranking, Top-N analysis |
| **RANK/DENSE_RANK** | Profitability | Product ranking |
| **LAG/LEAD** | Temporal Trends | Month-over-month growth |
| **CTE** | Regional Analysis | Readable subqueries |
| **Window Functions** | Customer Value | Percentile calculations |
| **Date Functions** | Trends | Cohort analysis |
| **JOIN Variations** | All queries | Multi-table analysis |
| **GROUP BY + HAVING** | Filters | Conditional aggregations |

---

## 📚 Advanced Python Concepts Demonstrated

| Concept | Use | Value |
|---------|-----|-------|
| **Pandas GroupBy** | Aggregation | Multi-level analysis |
| **DataFrame Merge** | Joining data | Integration |
| **Feature Engineering** | New metrics | Enhanced analysis |
| **Statistical Methods** | Validation | Hypothesis testing |
| **Visualization Stack** | Charts | Communication |
| **Error Handling** | Robustness | Production-ready |
| **Logging** | Debugging | Maintenance |
| **Documentation** | Clarity | Collaboration |

---

## 🔄 Extensibility

This pipeline can be extended for:

### Power BI Integration
```python
# Export processed data for Power BI
df_analysis.to_csv('powerbi_input.csv')
# Then import CSV into Power BI for dashboard
```

### Machine Learning
```python
from sklearn.preprocessing import StandardScaler
from sklearn.cluster import KMeans

# Use processed data for clustering
scaler = StandardScaler()
X_scaled = scaler.fit_transform(df_features)
clusters = KMeans(n_clusters=5).fit_predict(X_scaled)
```

### Automated Reporting
```python
# Monthly report generation
for month in date_range:
    df_month = filter_by_month(df, month)
    generate_report(df_month, output_path)
```

### Real-Time Dashboarding
```python
# Connect to live database
# Auto-refresh visualizations hourly/daily
# Alert on anomalies
```

---

## 📞 Troubleshooting

**Q: SQL query returns too much data (memory error)**
A: Use `LIMIT` clause in SQL or add aggregation before Python

**Q: Python merge creates too many rows (duplicate issue)**
A: Check join keys; use `.drop_duplicates()` or review SQL grouping

**Q: Visualizations not displaying in Jupyter**
A: Add `%matplotlib inline` at notebook start

**Q: SQL query takes too long**
A: Add indexes, use EXPLAIN PLAN, reduce result set size

---

## 📊 Files Included

### SQL Queries (6 files)
1. **01_data_quality_checks.sql** - Validation
2. **02_customer_segmentation.sql** - RFM analysis
3. **03_profitability_analysis.sql** - Margin breakdown
4. **04_product_performance.sql** - Ranking
5. **05_regional_analysis.sql** - Comparative
6. **06_temporal_trends.sql** - Time-series

### Python Notebooks (4 files)
1. **01_sql_data_extraction.ipynb** - Database connection & queries
2. **02_data_pipeline.ipynb** - ETL & validation
3. **03_advanced_analysis.ipynb** - Statistical analysis
4. **04_insights_reporting.ipynb** - Visualization & reports

### Outputs
- Visualizations (10+ charts)
- Analysis reports
- Dashboard files

---

**Ready to explore the data? Start with notebook 01! 🚀**

*This project showcases enterprise-grade data analysis combining SQL efficiency with Python flexibility.*

*Last Updated: December 2025*

 
