# Aadhaar Biometric Data Analysis for Risk States
## UIDAI Data Hackathon 2026

---

## Project Overview

This project provides a comprehensive data analysis framework for examining biometric completion rates across Aadhaar enrollment in India's high-risk states. Developed for the **UIDAI Data Hackathon 2026**, it combines granular geographic analysis (state, district, pincode levels) with temporal trend analysis to identify critical bottlenecks in biometric data collection and enrollment completion processes.

The analysis targets seven high-risk states identified by UIDAI for their lower biometric completion rates:
- **Assam**
- **Dadra and Nagar Haveli and Daman and Diu**
- **Goa**
- **Ladakh**
- **Meghalaya**
- **Mizoram**
- **Sikkim**

---

## Project Objectives

1. **Identify Critical Bottlenecks**: Pinpoint specific pincodes and districts where biometric data collection is failing or severely underperforming
2. **Quantify Risk**: Develop composite risk scores that combine multiple failure modes (zero completion, low completion, persistent anomalies)
3. **Provide Actionable Insights**: Offer clear, data-driven recommendations for infrastructure and capacity-building interventions
4. **Enable Evidence-Based Decision Making**: Supply state and district officials with prioritized lists of areas requiring urgent attention
5. **Track Progress**: Establish baseline metrics for monitoring improvement over time

---

## Data Sources

### Input Datasets
The analysis uses three primary data sources from the UIDAI Aadhaar enrollment system:

1. **Biometric Data** (`api_data_aadhar_biometric/`)
   - Monthly aggregated biometric completion records
   - Split across 4 CSV files (0-500K, 500K-1M, 1M-1.5M, 1.5M-1.86M rows)
   - Contains age-stratified biometric completion counts by month, state, district, and pincode

2. **Demographic Data** (`api_data_aadhar_demographic/`)
   - Monthly aggregated demographic data completion records
   - Split across 4 CSV files (0-500K, 500K-1M, 1M-1.5M, 1.5M-2M, 2M-2.07M rows)
   - Contains age-stratified demographic completion counts

3. **Enrollment Data** (`api_data_aadhar_enrolment/`)
   - Monthly aggregated enrollment records
   - Split across 3 CSV files (0-500K, 500K-1M, 1M-1.006M rows)
   - Contains age-stratified enrollment counts by month, state, district, and pincode

### Data Characteristics
- **Geographic Granularity**: State → District → Pincode (5-digit postal code)
- **Temporal Coverage**: Monthly periods
- **Age Groups**: Two groups analyzed - 5-17 years and 18+ years
- **Focus in Analysis**: 18+ age group (biometric completion rate for adults)

---

## Analysis Methodology

### Data Processing Pipeline

```
Raw CSV Files
    ↓
Load & Concatenate
    ↓
Preprocess & Normalize
    ↓
Filter (Risk States Only)
    ↓
Aggregate (Month × State × District × Pincode)
    ↓
Merge & Calculate Rates
    ↓
Anomaly Detection
    ↓
Summarize (Pincode & District Levels)
    ↓
Risk Scoring
    ↓
Export & Visualize
```

### Key Metrics

#### 1. **Biometric Completion Rate**
```
bio_rate_18p = bio_18p / enroll_18p
```
- Represents the proportion of enrollments that have completed biometric data capture
- Ranges from 0 (no completion) to 100+ (more biometric records than enrollments, indicating data quality issues)

#### 2. **Anomaly Classification**
- **Low Anomaly**: Biometric rate < 5th percentile (below-average performance)
- **Zero Anomaly**: Biometric rate = 0 (complete data collection failure)

#### 3. **Composite Risk Score**
```
risk_score = 0.5 × zero_ratio + 0.3 × anomaly_ratio + 0.2 × (1 / (1 + avg_bio_rate))
```

**Components:**
- **Zero Ratio** (50% weight): `zero_months / total_months` - frequency of complete failures
- **Anomaly Ratio** (30% weight): `anomaly_months / total_months` - frequency of low-performance months
- **Rate Penalty** (20% weight): Inverse relationship with average completion rate - penalizes chronically low performers

**Interpretation:**
- Score range: 0 (best) to ~1.0 (worst)
- Higher scores indicate greater operational challenges
- Provides single, comparable metric across all pincodes and districts

---

## Project Structure

```
UDAI/
├── README.md                              # This file
├── analysis.ipynb                         # State-level analysis (demographic & biometric rates)
├── pincode_analysis.ipynb                 # Pincode-level detailed analysis (HIGH-RISK STATES)
├── api_data_aadhar_biometric/             # Raw biometric data (4 CSV files)
├── api_data_aadhar_demographic/           # Raw demographic data (4 CSV files)
├── api_data_aadhar_enrolment/             # Raw enrollment data (3 CSV files)
├── outputs_analysis/                      # State-level analysis outputs
│   ├── *.png                              # Visualization graphs
│   └── *.csv                              # Aggregated statistics
└── risk_state_pincode_analysis/           # Pincode-level analysis outputs
    ├── risk_states_pincode_level_data.csv         # Complete month-level data
    ├── risk_states_pincode_anomalies.csv         # Filtered anomaly records only
    ├── risk_states_pincode_summary.csv           # Aggregated pincode metrics
    ├── critical_pincodes.csv                     # Top pincodes by risk score
    ├── critical_districts.csv                    # Top districts by anomaly burden
    ├── {state}_pincode_histograms.png           # Zero ratio & non-zero distribution
    ├── {state}_pincode_distribution.png         # KDE distribution curves
    └── pincode_anomalies_timeseries.png         # Temporal anomaly patterns
```

---

## Getting Started

### Prerequisites
```python
# Required Python libraries
pandas >= 1.3.0
numpy >= 1.20.0
matplotlib >= 3.3.0
seaborn >= 0.11.0
scipy >= 1.7.0
jupyter >= 1.0.0
```

### Installation

1. **Clone/Download the project**
```bash
# Navigate to your project directory where UDAI files are located
cd /path/to/your/UDAI/project
```

2. **Install dependencies**
```bash
pip install pandas numpy matplotlib seaborn scipy jupyter
```

3. **Prepare data structure**
   - Ensure CSV files are placed in respective directories:
     - `api_data_aadhar_biometric/` - biometric CSV files
     - `api_data_aadhar_demographic/` - demographic CSV files
     - `api_data_aadhar_enrolment/` - enrollment CSV files

### Running the Analysis

#### Option 1: Complete Pincode-Level Analysis (Recommended for High-Risk States)
```bash
jupyter notebook pincode_analysis.ipynb
```
This notebook:
- Analyzes only the 7 high-risk states
- Provides pincode-level granularity
- Identifies critical pincodes and districts requiring intervention
- Generates 5-10 outputs per state

**Execution Time**: ~5-15 minutes (depending on system)
**Output Files**: Generated in `risk_state_pincode_analysis/` directory

#### Option 2: State-Level Analysis (Broader Overview)
```bash
jupyter notebook analysis.ipynb
```
This notebook:
- Analyzes all states and union territories
- Provides state and district-level analysis
- Shows national-level trends and patterns
- Generates comparative visualizations

**Execution Time**: ~10-30 minutes

### Quick Start (Run Full Analysis)

```python
# In Jupyter/VS Code
# Run all cells in pincode_analysis.ipynb sequentially
# Outputs will be saved automatically to risk_state_pincode_analysis/
```

---

## Output Files Explanation

### Data Export Files (CSV)

#### 1. `risk_states_pincode_level_data.csv`
**Complete dataset at month-state-pincode granularity**
- Rows: ~50,000-100,000+ (depending on data volume)
- Columns: All intermediate calculations
- Use case: Deep-dive analysis, custom filtering, data validation

Key columns:
- `month`: Period (as Period type)
- `state`, `district`, `pincode`: Geographic identifiers
- `bio_rate_18p`: Calculated biometric completion rate
- `low_anomaly`, `zero_anomaly`: Boolean flags for anomalies

#### 2. `risk_states_pincode_anomalies.csv`
**Filtered dataset - only anomalous month-pincode combinations**
- Rows: ~1,000-5,000 (only records where anomalies exist)
- Columns: Same as complete dataset
- Use case: Focus on problem areas, identify patterns in failures

#### 3. `risk_states_pincode_summary.csv`
**Aggregated metrics at pincode level across all months**
- Rows: ~1,000-3,000 (unique pincodes per state)
- Columns: Aggregated statistics
- Use case: Pincode-level decision making, resource allocation

Key columns:
- `state`, `pincode`: Geographic identifiers
- `avg_bio_rate`: Mean completion rate (higher is better)
- `zero_count`: Number of months with zero collection
- `anomaly_count`: Number of months below 5th percentile
- `months_observed`: Total months in analysis
- `zero_ratio`: Proportion of months with zero collection
- `anomaly_ratio`: Proportion of months with low rates
- `risk_score`: Composite risk indicator (0=best, ~1=worst)

#### 4. `critical_pincodes.csv`
**Top 10 highest-risk pincodes per state (sorted by risk_score)**
- Rows: ~70 (10 per state × 7 states, less if some states have fewer pincodes)
- Columns: Same as pincode summary
- Use case: **PRIMARY TOOL FOR INTERVENTION PLANNING**

#### 5. `critical_districts.csv`
**Districts with anomalies, sorted by severity**
- Rows: ~30-50 (varies by state)
- Columns: District-level aggregated metrics
- Use case: District-level resource allocation, infrastructure planning

Key columns:
- `state`, `district`: Geographic identifiers
- `avg_bio_rate`: Mean district-level completion rate
- `zero_months`, `anomaly_months`: Count of problematic months
- `total_months`: Total observations
- `zero_ratio`, `anomaly_ratio`: Proportional metrics

---

## Visualization Outputs

### For Each Risk State (7 sets of visualizations)

#### 1. State Pincode Histograms (`{state}_pincode_histograms.png`)
**Two-panel visualization showing:**

**Left Panel - Zero Capture Ratio Distribution**
- Shows how many pincodes have zero collection in 0%, 10%, 20%... 100% of months
- Distribution near 0: Good (consistent data collection)
- Distribution near 1: Poor (frequent complete failures)

**Right Panel - Non-Zero Biometric Rate Distribution (Log Scale)**
- Shows completion rates for pincodes that have at least some data collection
- Helps identify operational capacity vs. infrastructure gaps
- Log scale reveals performance distribution across multiple orders of magnitude

**Use Case**: Assess whether problems are due to infrastructure (high zero ratio) or operational capacity (low non-zero rates)

#### 2. State Pincode Distribution (`{state}_pincode_distribution.png`)
**Single-panel histogram with KDE overlay**
- Shows count of pincodes at each completion rate level
- KDE curve reveals underlying distribution shape
- Single vs. multiple peaks indicate operational consistency
- Skewness shows whether most pincodes perform well or poorly

**Use Case**: Understand typical pincode performance and identify outlier groups

#### 3. Temporal Anomaly Pattern (`pincode_anomalies_timeseries.png`)
**Scatter plot with all anomalies across time and states**
- X-axis: Months (temporal trend)
- Y-axis: Bio rate severity (log scale, lower=worse)
- Colors: Different for each state
- Each point: One pincode-month combination with anomalies

**Use Case**: Identify whether problems are:
- Persistent (same pincodes repeatedly)
- Sporadic (different pincodes at different times)
- Systemic (all states affected simultaneously)
- State-specific (concentrated in one or few states)

---

## How to Use Results for Decision Making

### Step 1: Review Critical Pincodes Table
```
Open: risk_state_pincode_analysis/critical_pincodes.csv
Sort by: risk_score (descending)
```

**For each critical pincode, check:**
1. **Zero Ratio > 0.5**: Pincode has zero collection >50% of months
   - **Action**: Infrastructure audit, equipment provision, staffing review
   
2. **Anomaly Ratio > 0.5**: Pincode has low completion rates >50% of months
   - **Action**: Training programs, process optimization, supervision
   
3. **Avg Bio Rate < 50**: Average completion rate is very low
   - **Action**: Comprehensive operational review, leadership change, process redesign

### Step 2: Understand District-Level Challenges
```
Open: risk_state_pincode_analysis/critical_districts.csv
Sort by: zero_ratio (descending)
```

**District profile analysis:**
- **High zero_ratio, Low avg_bio_rate**: Lacks basic infrastructure
  - **Solution**: Capital investment, equipment, facilities
  
- **Low zero_ratio, Low avg_bio_rate**: Has infrastructure but poor execution
  - **Solution**: Training, process improvement, accountability
  
- **Both high**: Systemic failure across multiple dimensions
  - **Solution**: Comprehensive restructuring with both infrastructure and capacity building

### Step 3: Temporal Trend Analysis
```
Review: risk_state_pincode_analysis/pincode_anomalies_timeseries.png
```

**Pattern interpretation:**
- **Horizontal bands at bottom**: Specific pincodes with persistent failures
- **Scattered points**: Sporadic failures across different pincodes
- **Upward trend over time**: Improving conditions
- **Downward trend**: Worsening conditions
- **Color clustering**: Whether problems are state-specific or distributed

### Step 4: State-Level Comparisons
```
Review: risk_state_pincode_analysis/{state}_pincode_distribution.png
```

**Compare across states to understand:**
- Which states have most pincodes performing well
- Which states have widest variation in performance
- Which states have systemic (vs. isolated) problems

---

## Analysis Workflow in pincode_analysis.ipynb

The notebook is organized into 20 sequential sections:

| Section | Purpose | Input | Output |
|---------|---------|-------|--------|
| 1-5 | Setup, load, preprocess, filter | Raw CSV files | Cleaned dataframes |
| 6-8 | Aggregate data, calculate rates | Raw data | Month-pincode-level rates |
| 9-11 | Anomaly detection, risk scoring | Calculated rates | Risk scores |
| 12-13 | Summary statistics | Individual records | Aggregated metrics |
| 14-15 | Visualizations (histograms) | Pincode summary | State-level distribution graphs |
| 16-17 | Temporal analysis | Anomalies | Time-series scatter plot |
| 18 | Extract critical pincodes | Risk scores | Sorted table (top 10 per state) |
| 19 | Extract critical districts | District aggregates | Sorted districts with anomalies |
| 20 | Export all datasets | In-memory dataframes | CSV files for external analysis |

---

## Understanding Key Concepts

### Why These 7 States Are "High-Risk"?

The seven states/UTs in this analysis have been identified as priorities because:
1. **Lower biometric completion rates** compared to national average
2. **Geographic challenges**: Remote areas (Ladakh), island territories (D&D), northeastern states with connectivity issues
3. **Infrastructure gaps**: Limited biometric enrollment centers
4. **Population diversity**: Multiple languages, varying digital literacy
5. **Administrative challenges**: Coordination across state/UT boundaries

### Why Pincode-Level Granularity?

Pincode analysis enables:
- **Hyperlocal targeting**: Identify exact geographic coordinates for intervention
- **Resource optimization**: Focus support on specific 5-digit postal code areas
- **Root cause analysis**: Distinguish infrastructure vs. operational failures within a state
- **Scalable deployment**: Test solutions in small areas before state-wide rollout

### What Biometric Rate > 100 Means?

In some pincodes, `bio_rate_18p` may exceed 100, indicating:
- **Data quality issue**: More biometric records than enrollments
- **Possible causes**:
  - Duplicate biometric captures for same individual
  - Re-enrollment after initial enrollment in different period
  - Data logging errors
- **Action**: These pincodes warrant data audit and cleanup

### Interpretation of Risk Score Components

**Zero Ratio (50% weight)** - Most critical factor
- 0 = Zero collection in 0% of months (excellent)
- 1.0 = Zero collection in 100% of months (complete failure)
- Indicates infrastructure/baseline operational capacity

**Anomaly Ratio (30% weight)** - Secondary factor
- 0 = Low rates in 0% of months (excellent implementation)
- 1.0 = Low rates in 100% of months (consistent underperformance)
- Indicates operational efficiency and execution quality

**Rate Penalty (20% weight)** - Tertiary factor
- Inversely related to average completion rate
- Captures "how low is low" for pincodes with some collection
- Distinguishes between "barely functioning" and "well-performing" pincodes

---

## Customization & Extension

### Modify Analysis Parameters

**Change risk threshold:**
```python
# In pincode_analysis.ipynb, Section 8
LOW_THRESHOLD = df["bio_rate_18p"].quantile(0.10)  # Change from 0.05 to 0.10
```

**Adjust risk score weights:**
```python
# In Section 10
pincode_summary["risk_score"] = (
    0.6 * pincode_summary["zero_ratio"] +      # Increase zero_ratio weight
    0.2 * pincode_summary["anomaly_ratio"] +   # Decrease anomaly_ratio weight
    0.2 * (1 / (1 + pincode_summary["avg_bio_rate"]))
)
```

**Filter for specific state:**
```python
state_data = critical_pincodes[critical_pincodes["state"] == "assam"]
```

**Add age group 5-17 analysis:**
```python
# Modify Section 7 to include:
df["demo_rate_5_17"] = df["demo_5_17"] / df["enroll_5_17"]
df["bio_rate_5_17"] = df["bio_5_17"] / df["enroll_5_17"]
# Then create separate summaries for 5-17 age group
```

---

## Contact & Support

**For UIDAI Data Hackathon 2026:**
- Review submission guidelines for final deliverables
- Ensure all outputs are properly documented
- Include visualization snapshots in presentation

**For Technical Issues:**
- Check notebook execution order (some sections depend on prior cell outputs)
- Verify CSV files are in correct directories
- Ensure sufficient RAM (analysis processes ~5-7 million records)

---

## License & Attribution

This analysis was developed for the **UIDAI Data Hackathon 2026**.

**Datasets Provided By**: Unique Identification Authority of India (UIDAI)

---

## Quick Reference Commands

```bash
# Run complete analysis
jupyter notebook pincode_analysis.ipynb

# View results
cd risk_state_pincode_analysis/
# Open critical_pincodes.csv in Excel/Pandas
# View PNG files for visualizations

# Extract specific state analysis
python -c "
import pandas as pd
df = pd.read_csv('risk_state_pincode_analysis/critical_pincodes.csv')
assam = df[df['state'] == 'assam']
print(assam.to_string())
"

# Find worst-performing pincodes
python -c "
import pandas as pd
df = pd.read_csv('risk_state_pincode_analysis/critical_pincodes.csv')
worst = df.nlargest(20, 'risk_score')
print(worst[['state', 'pincode', 'risk_score', 'avg_bio_rate']])
"
```

---

## Expected Results Summary

After running the complete analysis, you should have:

✅ **20 Analysis Outputs Per State** (140 total for 7 states):
- Pincode histograms (zero ratio + log-scale rates)
- Distribution curves with KDE
- Temporal anomaly patterns
- Critical pincode lists
- District-level summaries

✅ **5 Master CSV Files** (consolidated across all states):
- Complete pincode-level data (~50K+ records)
- Anomalies only (~1K-5K records)
- Pincode summary metrics
- Critical pincodes (top 10/state)
- Critical districts

✅ **Key Insights**:
- Identification of 70 highest-risk pincodes across 7 states
- Quantified risk scores for intervention prioritization
- Evidence of infrastructure vs. operational challenges
- Temporal trends showing improving or declining performance
- District-level strategic insights for resource allocation

---

**Last Updated**: January 2026  
**Project Version**: 1.0  
**Status**: Analysis Complete ✓

---

For detailed methodology and interpretation guidance, see the markdown cells within the notebooks for section-by-section explanations.
