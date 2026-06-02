SI 305 Problem Set 2 — Elevated Blood Lead Level (EBLL) Analysis in Michigan
An exploratory data analysis notebook examining childhood elevated blood lead level (EBLL) testing data across Michigan zip codes and counties, completed for SI 305: Introduction to Data Analysis (Winter 2026) at the University of Michigan School of Information.

Overview
This notebook analyzes a Michigan Department of Health dataset tracking blood lead testing results in children by zip code and year. The analysis covers data cleaning, suppression patterns, geographic aggregation, and multi-county trend analysis.

Dataset
Two external datasets are loaded directly from Google Drive:
DatasetDescriptionEBLL Testing DataZip-code-level reports of children tested and those with an EBLL, 2010–2024ZIP–County CrosswalkMaps Michigan zip codes to county names
Both are publicly accessible CSVs loaded via pd.read_csv() with direct Google Drive download URLs.

Notebook Structure
Part 1 — Characterizing the EBLL Data
1.1 Load and Characterize

Loads the raw EBLL dataset and inspects shape, null values, and data types
Dataset: 30,800 rows × 8 columns; 3 float64 columns

1.2 Clean the Data

Drops rows with null values in Number of Children Tested
Filters to a single Blood Lead Reference Value (3.5 µg/dL)
Strips asterisks from zip code strings and casts to float
Creates a boolean Suppressed column for suppressed percentage reports
Cleaned dataset: 12,961 rows; ~50.6% unsuppressed

1.3 Characterize Suppressed Reports

Calculates suppression rates aggregated by zip code and year
Key findings:

~54.1% of zip codes have more than half their reports suppressed
~21.7% of zip codes have fewer than 25% suppressed
2023 had the highest annual suppression rate (~53.2%)



1.4 Plot Suppressed Reports

Histogram of suppression rates by zip code
Line chart of suppression rates over time (2010–2024)
Suppression rates have trended upward from ~47% (2010) to ~51% (2024)


Part 2 — Comparing Across Michigan Counties
2.1 Load and Characterize ZIP–County Data

Loads a ZIP-to-county crosswalk and filters to Michigan
Drops STCOUNTYFP and CLASSFP columns
Result: 1,102 Michigan zip codes; 326 (~32.8%) span multiple counties

2.2 Merge the Datasets

Merges EBLL data with zip-county crosswalk on zip code
Merged dataset: 19,592 rows

2.3 Aggregate by County

Analyzes suppression rates and EBLL rates for Ingham, Washtenaw, and Wayne counties

County% Suppressed% Unsuppressed Reports w/ >5% EBLLIngham~38.9%~57.1%Washtenaw~55.5%~17.3%Wayne~17.9%~51.1%
2.4 Trends Over Time

Aggregates total children tested and total with EBLL by county and year
Plots percent positive over time for all three counties (2010–2024)
In 2024: Ingham ~5.6%, Washtenaw ~2.6%, Wayne ~5.9% positive rates
All three counties show an overall downward trend, though Washtenaw has seen a slight uptick since 2021


Key Libraries
pythonpandas
numpy
matplotlib

How to Run

Clone or download this repository
Open PS2.ipynb in Jupyter Notebook or JupyterLab
Run all cells top to bottom — datasets load automatically via URL


No local data files are required. An internet connection is needed to fetch the CSVs from Google Drive.


Notes

The Blood Lead Reference Value filter (== 3.5) is applied during cleaning to ensure comparability across years
Suppressed reports (where fewer than 5 children were tested in a zip code) are flagged with a boolean column rather than dropped, allowing them to be included or excluded depending on the analysis
One cell includes an attribution to Claude AI for a matplotlib range parameter suggestion
