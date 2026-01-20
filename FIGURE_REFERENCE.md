# FIGURE REFERENCE: Complete List of Visualizations and Charts

A complete enumeration of all figures generated across the national-level and pincode-level analyses, with descriptions suitable for figure captions in research publications and reports.

---

## NATIONAL-LEVEL ANALYSIS FIGURES (Analysis.ipynb)

### **Figure 1: Distribution of Biometric Completion Rates (18+) - Histogram & KDE**
- **File**: `bio_rate_18p_distribution.png` (Panel 1 of 3-panel visualization)
- **Type**: Histogram with Kernel Density Estimate overlay
- **Description**: Frequency distribution of biometric completion rates for the 18+ age group across all state-month observations, with a smooth kernel density estimate (KDE) curve overlaid. The histogram shows the concentration of locations by completion rate, while the KDE reveals the underlying probability distribution shape.
- **X-axis**: Biometric completion rate (0-1 scale or higher)
- **Y-axis**: Frequency (count of observations)
- **Key Finding**: Right-skewed distribution with significant concentration at lower completion rates, indicating that most locations are below-average performers with a long tail of exceptional high performers.

---

### **Figure 2: Distribution of Biometric Completion Rates (18+) - Boxplot**
- **File**: `bio_rate_18p_distribution.png` (Panel 2 of 3-panel visualization)
- **Type**: Box-and-whisker plot
- **Description**: Statistical summary of biometric completion rates displaying quartiles, median, and outliers. Shows the interquartile range (IQR) containing the middle 50% of data, with whiskers extending to extreme values and individual outliers marked as points.
- **Key Finding**: Dense concentration of observations in lower quartiles with numerous high-value outliers, confirming substantial positive skewness and indicating that the median (50th percentile) is considerably lower than the mean.

---

### **Figure 3: Log-Transformed Distribution of Biometric Completion Rates (18+)**
- **File**: `bio_rate_18p_distribution.png` (Panel 3 of 3-panel visualization)
- **Type**: Histogram with KDE of log-transformed values
- **Description**: Distribution of biometric completion rates after logarithmic transformation using log₁ₚ(rate). This transformation is applied to reveal the underlying distribution shape and test for log-normality.
- **X-axis**: log(1 + biometric rate)
- **Y-axis**: Frequency
- **Key Finding**: The transformed distribution approaches normality and approximate bell-shape, indicating that the underlying biometric completion rates follow a log-normal distribution, where multiplicative relationships are more meaningful than additive ones.

---

### **Figure 4: State-wise Average Biometric Completion Rate (Log Scale)**
- **File**: `avg_biometric_completion_rate_18plus_log.png`
- **Type**: Horizontal bar chart with logarithmic x-axis
- **Description**: Ranking of all states and union territories by their average biometric completion rate (18+ age group) for the entire analysis period, sorted from lowest to highest performance. The logarithmic scale accommodates the two-order-of-magnitude range in state averages.
- **X-axis**: Biometric rate (log scale)
- **Y-axis**: State names
- **Key Finding**: Stark disparities in state-level performance, with some states averaging below 50-unit completion and others exceeding 500 units. Most states cluster in the lower half, indicating that low biometric completion is the national norm.

---

### **Figure 5: Monthly Biometric Completion Trend (18+)**
- **File**: `monthly_biometric_completion_18plus.png`
- **Type**: Line plot with markers
- **Description**: Monthly trend of average biometric completion rates for the 18+ age group, showing temporal evolution across the analysis period. Each point represents the mean completion rate across all states for that month.
- **X-axis**: Month (temporal sequence)
- **Y-axis**: Average biometric rate across all states
- **Key Finding**: Month-to-month volatility indicates that biometric completion rates are not static but respond to operational factors, policy changes, and external events. Trend direction (upward vs. downward) indicates whether system capacity is expanding or contracting.

---

### **Figure 6: Pincode-Level Biometric Anomalies Scatter Plot**
- **File**: `zero_bio_rate_anomalies.png`
- **Type**: Scatter plot with state color-coding
- **Description**: Visualization of all state-month combinations with anomalously low or zero biometric completion rates. Each point represents one anomalous record, with temporal position showing when anomalies occurred and vertical position showing severity.
- **X-axis**: Month
- **Y-axis**: Biometric rate (18+)
- **Colors**: Different colors for each state
- **Key Finding**: Anomalies are not uniformly distributed across time or geography. Some states show concentrated anomaly problems; temporal clustering indicates system-wide disruptions.

---

### **Figure 7: Time Series with Anomalies Highlighted by State (Chunk 1)**
- **File**: `bio_rate_18p_states_1_to_10.png` (and subsequent chunk files)
- **Type**: Line plot with scatter overlay
- **Description**: Temporal trends in biometric completion rates for approximately 10 states per visualization, with anomalies highlighted in red. Lines show monthly progression for each state; red points highlight months with critically low or zero completion.
- **X-axis**: Month (temporal sequence)
- **Y-axis**: Biometric rate (log scale)
- **Colors**: Different line colors for different states; red points for anomalies
- **Key Finding**: Patterns vary by state—some show stable low performance with frequent anomalies (systemic failures), others show volatility (operational disruptions), and some show improvement trends (capacity expansion).

---

### **Figure 8: Log-Transformed Distribution of Biometric Rates (Direct Transformation)**
- **File**: `bio_rate_18p_log_transformed_histogram.png`
- **Type**: Histogram with KDE of logarithmically-transformed values
- **Description**: Distribution resulting from direct logarithmic transformation of all biometric rates using log₁ₚ(x), then visualized as a histogram. This approach emphasizes the shape of the transformed data.
- **X-axis**: log(1 + biometric rate)
- **Y-axis**: Frequency
- **Key Finding**: Confirms log-normal behavior of the underlying data, with transformed distribution approaching normality. This validates the use of multiplicative relationships for interpreting biometric completion variations.

---

### **Figure 9: Distribution with Logarithmic Binning (Non-transformed)**
- **File**: `bio_rate_18p_log_binning_histogram.png`
- **Type**: Histogram with logarithmically-spaced bins
- **Description**: Distribution of biometric completion rates using logarithmically-spaced bins (not transforming the data itself, but adjusting bin sizes logarithmically). The x-axis is then set to logarithmic scale. This approach preserves original units while accommodating wide value ranges.
- **X-axis**: Biometric rate (log scale)
- **Y-axis**: Frequency (linear scale)
- **Key Finding**: Maintains interpretability in original units while revealing structure across the full numerical range from near-zero to extremely high completion rates. Clearly shows the dominant concentration at lower rates.

---

### **Figure 10: Correlation Matrix of Key Metrics (18+)**
- **File**: `correlation_matrix_18plus.png`
- **Type**: Heatmap with correlation coefficients
- **Description**: Correlation matrix showing pairwise relationships among three key variables for the 18+ age group: enrollment count, demographic completion rate, and biometric completion rate.
- **Cells**: Correlation coefficients with color gradient (dark blue = high positive correlation; light blue = low correlation)
- **Key Finding**: Moderate to strong correlation between demographic and biometric rates (they scale together); weak to moderate correlation between enrollment volume and completion rates (higher enrollments don't automatically mean higher completion).

---

### **Figure 11: High-Risk States Ranked by Biometric Completion Rate**
- **File**: `high_risk_states_biometric_completion_18plus.png`
- **Type**: Horizontal bar chart with threshold line
- **Description**: Bar chart showing all states with average biometric completion rates below the risk threshold (200 units), sorted from worst to best performance. A dashed vertical line marks the 200-unit threshold.
- **X-axis**: Average biometric completion rate
- **Y-axis**: State names (sorted from worst to best)
- **Key Finding**: Multiple states fall significantly below the risk threshold, with distances from threshold indicating severity and resource requirements for intervention.

---

## PINCODE-LEVEL ANALYSIS FIGURES (Pincode_Analysis.ipynb)

### **Figure 12: State-Level Pincode Distribution - Zero Capture Ratio (Dual Panel)**
- **File**: `{state}_pincode_histograms.png` (Left Panel) - Generated for each of 7 high-risk states
- **Type**: Histogram showing distribution of zero-capture ratios across pincodes
- **Description**: Distribution of the proportion of months (0-1 scale) where each pincode experienced complete biometric collection failure (zero ratio). Shows how many pincodes fall into each zero-ratio category.
- **X-axis**: Zero ratio (0 to 1, representing 0% to 100% of months with zero collection)
- **Y-axis**: Number of pincodes with that zero-ratio
- **Key Finding**: States vary dramatically—some show distributions heavily skewed toward 0 (most pincodes collect biometric data consistently), others skewed toward 1 (persistent system failures). Distribution shape indicates state-level infrastructure adequacy.

---

### **Figure 13: State-Level Pincode Distribution - Non-Zero Rates (Dual Panel)**
- **File**: `{state}_pincode_histograms.png` (Right Panel) - Generated for each of 7 high-risk states
- **Type**: Histogram with log-scaled x-axis
- **Description**: Distribution of average biometric completion rates (for months when biometric collection occurred) across pincodes within each state, displayed on logarithmic scale.
- **X-axis**: Average biometric rate (log scale)
- **Y-axis**: Number of pincodes with that average rate
- **Key Finding**: Wide spread indicates high variation in implementation capacity across pincodes. Sharp peak at lower values indicates most pincodes struggle with completion even when collection occurs. Tail length shows if exceptional performers exist.

---

### **Figure 14: Pincode-Level Biometric Rate Distribution with KDE (Single State)**
- **File**: `{state}_pincode_distribution.png` - Generated for each of 7 high-risk states
- **Type**: Histogram with kernel density estimate overlay
- **Description**: Distribution of average biometric completion rates across all pincodes within a single high-risk state, with KDE curve revealing the underlying probability distribution.
- **X-axis**: Average biometric rate (18+)
- **Y-axis**: Count of pincodes
- **Key Finding**: Distribution shape (unimodal vs. bimodal, symmetric vs. skewed) reveals whether pincodes have consistent performance or distinct categories (e.g., functioning vs. non-functioning). Wide spread indicates heterogeneous capacity.

---

### **Figure 15: Pincode-Level Biometric Anomalies Time Series (Log Scale)**
- **File**: `pincode_anomalies_timeseries.png`
- **Type**: Scatter plot with state color-coding
- **Description**: Temporal and spatial distribution of all pincode-month anomalies across the seven high-risk states, with logarithmic y-axis to reveal both near-zero and moderately-low anomalies simultaneously.
- **X-axis**: Month (temporal progression)
- **Y-axis**: Biometric rate (log scale), showing severity of each anomaly
- **Colors**: Different colors for each of the 7 high-risk states
- **Key Finding**: Reveals temporal clustering (certain periods with many anomalies), geographic concentration (some states appear more frequently), and persistence patterns (horizontal bands indicate recurring failures in specific pincodes).

---

## DATA TABLES (Exported as CSV, Displayed in Notebooks)

### **Table 1: Critical Pincodes Summary (Top 20 displayed)**
- **File**: `critical_pincodes.csv`
- **Type**: Tabular data (DataFrame)
- **Description**: Ranked list of pincodes with anomalies, sorted by composite risk score in descending order. Shows top 20 critical pincodes across all states.
- **Columns**: 
  - state: State name
  - pincode: 6-digit postal code
  - avg_bio_rate: Mean biometric completion rate across months
  - anomaly_count: Months with critically low performance
  - zero_count: Months with zero collection
  - months_observed: Total months analyzed
  - zero_ratio: Proportion of months with zero collection
  - anomaly_ratio: Proportion of months with anomalies
  - risk_score: Composite risk score (50% zero ratio + 30% anomaly ratio + 20% low avg rate)
- **Key Finding**: Identifies highest-priority pincodes requiring urgent intervention, sorted by severity of combined failure modes.

---

### **Table 2: Critical Districts Summary (Top 20 displayed)**
- **File**: `critical_districts.csv`
- **Type**: Tabular data (DataFrame)
- **Description**: District-level summary of biometric completion performance, filtered to show only districts with anomalies, sorted by zero_ratio and anomaly_ratio.
- **Columns**:
  - state: State name
  - district: District name
  - avg_bio_rate: Mean biometric rate across pincodes and months
  - anomaly_months: Count of month-observations with critically low rates
  - zero_months: Count of month-observations with zero collection
  - total_months: Total number of observations
  - zero_ratio: Proportion with zero collection
  - anomaly_ratio: Proportion with anomalies
- **Key Finding**: Shows whether problems are localized to specific pincodes or systemic at district level, enabling appropriate intervention scale (pincode vs. district vs. state).

---

## SUPPLEMENTARY DATA EXPORTS

### **Export 1: Complete Pincode-Level Monthly Data**
- **File**: `risk_states_pincode_level_data.csv`
- **Description**: Comprehensive dataset of all month-state-district-pincode combinations with full metrics, suitable for independent verification and custom analysis.

### **Export 2: Anomalous Records Only**
- **File**: `risk_states_pincode_anomalies.csv`
- **Description**: Filtered dataset containing only anomalous pincode-month observations for focused investigation of failures.

### **Export 3: Pincode-Level Aggregated Metrics**
- **File**: `risk_states_pincode_summary.csv`
- **Description**: Aggregated metrics at pincode level across all months, containing average rates, anomaly counts, and risk scores for all pincodes in high-risk states.

---

## FIGURE USAGE GUIDELINES

### How to Reference Figures in Text

**Format for results narrative**:
- "As Figure 1 shows, the biometric completion rate distribution is highly right-skewed..."
- "Figure 4 reveals stark disparities in state-level performance, ranging from..."
- "The temporal analysis (Figure 5) indicates that monthly variation is substantial..."
- "Critical pincodes identified in Figure 12-14 are concentrated in..."

### Grouping Figures by Analysis Theme

**Distribution Analysis**:
- Figures 1-3: National-level distribution characteristics
- Figures 12-14: Pincode-level distributions by state

**Geographic Disparities**:
- Figure 4: State-level ranking
- Figures 12-13: Pincode variation within states
- Tables 1-2: Critical locations identified

**Temporal Patterns**:
- Figure 5: National monthly trends
- Figure 6-7: Anomaly timing and state patterns
- Figure 15: Pincode-level temporal anomalies

**Correlations and Relationships**:
- Figure 10: Metric correlations
- Figure 11: State categorization by threshold

---

## SUMMARY: TOTAL FIGURE COUNT

| Analysis Level | Figure Count | Description |
|---|---|---|
| National-Level Distribution | 3 | Histogram, Boxplot, Log-transformed (Fig 1-3) |
| National-Level Geographic | 2 | State ranking, Threshold categorization (Fig 4, 11) |
| National-Level Temporal | 3 | Monthly trend, Anomalies scatter, Time series (Fig 5-7) |
| National-Level Alternative Visualization | 2 | Log-transformation methods (Fig 8-9) |
| National-Level Relationships | 1 | Correlation heatmap (Fig 10) |
| **National-Level Subtotal** | **11 Figures** | |
| Pincode-Level State Comparisons | 7 × 2 | Dual histograms per state (Fig 12-13) |
| Pincode-Level Distributions | 7 | KDE distributions per state (Fig 14) |
| Pincode-Level Temporal | 1 | Anomalies time series (Fig 15) |
| **Pincode-Level Subtotal** | **22 Figures** | |
| **Data Tables** | **2 Tables** | Critical pincodes and districts |
| **Data Exports** | **3 CSV Files** | Full datasets for verification |
| **GRAND TOTAL** | **38+ Visual Elements** | 11 National + 22 Pincode + 2 Tables + 3 Exports |

---

## ARCHIVING AND REPRODUCTION

All figures are saved in the following formats:
- **PNG files**: High-resolution (300 DPI) for publication
- **CSV data**: For reproducibility and independent verification
- **Notebook cells**: Original analysis code documented in Jupyter notebooks

Figure filenames are descriptive and correspond to analysis sections, enabling easy location and organization.

