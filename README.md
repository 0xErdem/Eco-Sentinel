Eco-Sentinel: Unsupervised Machine Learning for Harmful Algal Bloom (HAB) Detection
Project Overview
Eco-Sentinel is a data-driven environmental engineering project aimed at detecting Harmful Algal Blooms (HABs) and sensor anomalies in aquatic ecosystems. By combining water quality thermodynamics with unsupervised machine learning, this project identifies the true biological signatures of ecological crises without relying on pre-labeled data or rigid thresholds.

The Environmental Problem
Harmful Algal Blooms cause severe hypoxia and ecosystem degradation. Identifying them from raw multidimensional sensor data (Temperature, pH, Dissolved Oxygen, Secchi Depth) is challenging because:

The relationship between water parameters is highly non-linear.

High dissolved oxygen in cold water is a normal thermodynamic state, whereas in warm water, it indicates a biological crisis (supersaturation).

Field sensors frequently record erroneous data (e.g., impossible temperatures) that must be filtered out before analysis.

Methodology & Data Pipeline
1. Data Preprocessing
Handling Missing Values: Applied median imputation for critical columns (Dissolved Oxygen, pH) to maintain data integrity.

Noise Reduction: Removed administrative columns and redundant metrics to streamline the dataset.

2. Physics-Aware Feature Engineering
To prevent the AI from making statistical misinterpretations, domain-specific ecological formulas were injected:

DO Saturation Percentage: Calculated theoretical maximum dissolved oxygen capacity to isolate supersaturation events driven by algae.

Turbidity Index: Derived from Secchi Depth to mathematically represent biomass concentration.

Photosynthetic Index: A composite metric capturing simultaneous spikes in alkalinity and oxygen during intense algal activity.

3. Anomaly Detection (Isolation Forest)
Implemented an Isolation Forest to scan for extreme multi-dimensional outliers, separating severe ecological events from sensor hardware failures.

4. Ecosystem State Classification (K-Means Clustering)
The cleaned data was passed through a K-Means Clustering algorithm to define specific ecological states:

Cluster 2 (Normal Ecosystem): Low turbidity, stable pH, and baseline photosynthetic activity.

Cluster 1 (Physical Turbidity): High turbidity but normal photosynthesis (e.g., sediment run-off, not a bloom).

Cluster 0 (The HAB Signature): High turbidity (biomass) + extreme Photosynthetic Index. True algal bloom autonomously isolated.

Technologies Used
Language: Python

Data Science Libraries: Pandas, NumPy, Scikit-learn, Matplotlib, Seaborn

Algorithms: Isolation Forest (Anomaly Detection), K-Means (Clustering)

How to Run
Clone this repository: git clone https://github.com/OxErdem/Eco-Sentinel.git

Install the required dependencies: pip install pandas numpy scikit-learn matplotlib seaborn

Run wqa.ipynb via Jupyter Notebook or Google Colab to view the data pipeline and the final ecosystem clustering visualizations.
