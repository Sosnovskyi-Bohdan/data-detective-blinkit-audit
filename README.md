# Project: The Data Detective - A Forensic Audit of a Retail Dataset
---
- **Project Overview**

This project is a case study in data forensics and quality auditing. Instead of performing a traditional business analysis, we take on the role of a "data detective" to investigate a publicly available retail dataset and determine its authenticity.

The initial goal was to analyze customer behavior and marketing effectiveness. However, preliminary checks revealed significant anomalies, shifting the project's focus to a critical examination of the data's integrity. This project demonstrates a crucial, often overlooked, step in the data analysis workflow: verifying that the data is a sound basis for any conclusion.

The dataset, found on Kaggle, came with a description suggesting advanced use cases such as:

*"Demand Forecasting, Price Optimization, Customer Behavior Analysis, Market Trends..."*

Our investigation will reveal the stark contrast between these suggested use cases and the reality of the data's quality.

- **Methodology & Tech Stack**
  
Our investigation was hypothesis-driven, moving from high-level checks to deep, conclusive tests.

Tech Stack: Python, Pandas, Matplotlib, Seaborn, Scikit-learn, Benfordslaw

Methodology:

1. Express Audit: Quick checks for data types, missing values, and uniqueness.

2. Deep Visual Audit: Analysis of data distributions using histograms and density plots.

3. Statistical & Mathematical Audit: Correlation analysis and testing against Benford's Law.

4. Logical Consistency Audit: Verifying data integrity across related tables.

5. Evidence Locker: Summary of Findings
  
Our forensic audit uncovered overwhelming evidence of synthetic data generation and a lack of internal consistency.

---

- **Finding 1:** The Data is Too Perfect (and Too Flawed)
  
  - Impossible Values: The ``delivery_time_minutes`` column contains negative values, which is physically impossible.
  
  - Suspiciously Clean: The dataset has almost no missing values, which is highly unusual for real-world data.
  
  - Low Uniqueness (The "Template" Evidence):
  
  - Feedback: Only ``25`` unique text strings for ``5,000`` feedback entries.
  
  - Delay Reasons: Only 1 unique reason for all delayed orders.
  
  - Products: A critical inconsistency where 268 ``product_ids`` map to only ``51`` ``product_names``.

- Finding 2: Unnatural Distributions
  - Uniform ("Box-like") Shapes: Key financial and logistical metrics (``avg_order_value``, ``distance_km``, ``spend``) exhibit near-perfect uniform distributions, a clear hallmark of simple random number generation, not natural business processes.
  - A real-world distribution of financial data is almost never flat.

- Finding 3: Lack of Logical Correlation
  - The correlation between logically connected marketing metrics is effectively zero (e.g., ``spend`` vs. ``revenue_generated`` is ``-0.01``). This proves that each column was generated independently without any underlying business logic.
  - In reality, spend and revenue should be positively correlated.

- Finding 4: Violation of Benford's Law
  - The distribution of the first digits in the order_total column significantly deviates from the expected Benford's Law curve (``P-value ≈ 0``). This is a strong indicator of non-organic, artificial data.
  - The black bars (our data) do not follow the red dots (Benford's Law).

- Finding 5: Critical Integrity Failure
  - The final audit revealed that ``99.98%`` of orders have a significant discrepancy between the stated ``order_total`` and the actual sum of its items. This is a fundamental violation of data integrity and proves the data was generated without cross-table validation.

---
- **Final Conclusion**
  
The dataset is a synthetically generated artifact with critical flaws in its design and is wholly unsuitable for the business analyses suggested in its description. Any attempt at forecasting, price optimization, or customer behavior analysis based on this data would yield meaningless and potentially misleading results.

This project underscores the importance of a "trust but verify" approach in data analysis. Before building complex models or deriving business insights, an analyst's primary responsibility is to audit the quality and integrity of the source data.

- **How to Replicate the Audit**
Clone the repository:

``git clone https://github.com/Sosnovskyi-Bohdan/data-detective-blinkit-audit.git``

Download the dataset from the [source on Kaggle](https://www.kaggle.com/datasets/akxiit/blinkit-sales-dataset "Blinkit Sales Dataset") and place the CSV files in the data/ directory.

Open and run the Jupyter Notebook located in the notebooks/ directory to see the full forensic analysis.
