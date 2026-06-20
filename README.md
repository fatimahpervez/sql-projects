Evaluating a Manufacturing Process — SQL Statistical Process Control

## Project Overview
A SQL-based quality control analysis of a manufacturing process, using 
statistical process control (SPC) methods to flag products that fall 
outside acceptable control limits during production.

## Business Question
Is the manufacturing process operating within acceptable statistical 
control limits, or are certain operators/items producing defective 
output that needs investigation?

## Dataset
`manufacturing_parts` table containing:
| Column | Description |
|--------|-------------|
| `item_no` | The item number |
| `length` | The length of the item made |
| `width` | The width of the item made |
| `height` | The height of the item made |
| `operator` | The machine/operator that produced the item |

## Methodology
- Used a **window function of length 5** (rolling window including 
  the current row) to calculate a rolling average and rolling 
  standard deviation of product height, partitioned by operator
- Calculated **Upper Control Limit (UCL)** and **Lower Control Limit 
  (LCL)** using the statistical formula: 
  `average ± 3 × (standard deviation / √5)`
- Flagged each item with a boolean `alert` if its height fell outside 
  the calculated control limits
- Excluded incomplete rolling windows (fewer than 5 preceding rows) 
  to ensure statistical validity

## SQL Techniques Used
- Common Table Expressions (CTEs) with `WITH` clauses
- Window functions: `ROW_NUMBER()`, `AVG() OVER`, `STDDEV_SAMP() OVER`
- Rolling window frames: `ROWS BETWEEN 4 PRECEDING AND CURRENT ROW`
- Conditional flagging with `NOT BETWEEN`
- Partitioning by operator for per-operator control limits

## Tools
- **SQL** (PostgreSQL syntax)
- DataCamp's SQL workspace environment

## Key Skills Demonstrated
- Statistical process control (SPC) methodology
- Advanced SQL window functions
- Quality control / manufacturing analytics
- Translating a statistical formula into working SQL logic
- Data validation and edge case handling (incomplete windows)

## Result
A query returning `operator`, `row_number`, `height`, `avg_height`, 
`stddev_height`, `ucl`, `lcl` and a boolean `alert` flag for every 
item, ordered by `item_no` — enabling quick identification of items 
that fall outside statistical control limits.

## About Me
BSc Economics graduate from LUMS, Pakistan.
Building data analytics skills in Python, SQL, Tableau and Statistics.

🔗 [LinkedIn](https://linkedin.com/in/fatimapervez)
