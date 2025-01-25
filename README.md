# Humanitarian Flood Vulnerability Index (HFVI): Weight calculation and Case Study Application & Analysis

This repository contains all the materials, data, and scripts required to reproduce the Humanitarian Flood Vulnerability Index (HFVI), supporting the publication "Developing a Spatially Explicit Humanitarian Flood Vulnerability Index for Refugee Camps using Fuzzy Multi-Criteria Decision Analysis" and contains the files for the Analytical Hierarchy Process (AHP), Fuzzy Analytical Hierarchy Process (FAHP), and the Humanitarian Fuzzy Vulnerability Index (HFVI) applied to the a refugee camp using synthetic data. 

## Overview
This repository contains three main scripts, each performing a specific part of the workflow:

1. **AHP Analysis**: Calculates the AHP weights based on expert questionnaire responses.
2. **FAHP Analysis**: Calculates the Fuzzy AHP weights using the outputs from the AHP analysis using fuzzy logic.
3. **HFVI Calculation**: Combines individual indicator layers using the HFVI equation, followed by sensitivity and uncertainty analysis.

## Repository Structure

hfvi_project/
|
├── README.md              			# Project description and instructions
├── data/                  			# Input data
│   ├── ahp/...   					    # Analytical Hierarchy Process calculations
│   ├── shp/   					        # Geospatial shapefiles
│   	├── global/..					    # Global datasets
│   	├── local/..					    # Local datasets (synthetic data)
|
├── scripts/               			# Scripts for analysis
│   ├── AHP_analysis.Rmd   		  # Analytical Hierarchy Process calculations
│   ├── FAHP_analysis.Rmd  		  # Fuzzy Analytical Hierarchy Process calculations
│   ├── HFVI_calculation.Rmd  	# HFVI computation and spatial analysis
│   ├──.Rproj                 	# RStudio project file
|
├── outputs/               			# Analysis results and outputs
│   ├── oat/						        # Files stored from the OAT-FAHP approach
│   ├── figures/           			# Visualizations (plots, maps, etc.)
│   ├── results/...           	# Final results and tables
├── documentation/         			# Supporting documents
│   └── methodology.pdf    			# Methodological overview


## Data 
### Input Data
#### data/shp: Geospatial data in Shapefile format (Spatial geometries of features) used for the indicators raster calculation.

**Global Data**: The extracts of the global datasets used for the fictional case study example are provided in the data folder for a fictional camp in Rwanda. All data extracts are downloaded in January 2025. The extract is clipped to the extent of the refugee camp under study in the HFVI_calculation.Rmd to fit the extent of the camp.

When applying the HFVI to a different camp, the global data can be openly extracted from the following sources:

- Google Buildings: Google Research. (2021). Open Buildings dataset v2 (Release 2021) [Data set]. Available at: https://sites.research.google/open-buildings/#dataformat

- Roads OSM Data: OpenStreetMap contributors. (2025). Rwanda [Data set]. Geofabrik. https://download.geofabrik.de/africa/rwanda.html

- Global Land Cover Data (30-m spatial resolution): Potapov, P., Hansen, M.C., Pickens, A., Hernandez-Serna, A., Tyukavina, A., Turubanova, S., Zalles, V., Li, X., Khan, A., Stolle, F. and Harris, N., 2022. Global Land Cover and Land Use Change (GLCLU) Dataset v2 [Data set]. University of Maryland. Available at: https://glad.earthengine.app/view/glcluc-2000-2020.

**Local Data**: Synthetically generated local data

The local data used for the original study cannot be published due to sensitivity restrictions. To demonstrate the workflow and performance of the HFVI, synthetic data was generated for a fictive refugee camp in Rwanda. This synthetic data is randomly generated and was constructed in ArcGIS Pro, with hand-drawn features stored as shapefiles. These shapefiles are provided in the data folder. 

For implementing the HFVI in real-world cases, local data should be collected through official camp maps and participatory workshops. Official camp information is often provided by organizations like the UNHCR. Real-world local data should be stored as shapefiles in a format analogous to the pseudo data provided in this repository.

#### data/ahp

AHP_results.xlsx: This dataset contains the results of Analytic Hierarchy Process (AHP) questionnaires conducted to calculate indicator weights across various vulnerability dimensions. The data is structured as Pairwise Comparison Matrices (PCMs), with comparisons derived from expert evaluations. These weights are used in the calculation of the HFVI.

Sheets:
- SOC: PCMs for social vulnerability indicators.
- PHY: PCMs for physical vulnerability indicators.
- Domain: PCMs for high-level aggregated domains (social vs. physical).

Format: Square matrices where rows and columns represent indicators or domains.
Columns: Each pairwise comparison (e.g., SOC1_SOC2, PHY1_PHY3) represents the relative importance of one indicator/domain to another.

### Output Data
Maps and results are stored in outputs/.

## Scripts and workflow 
### AHP Analysis: AHP_analysis.Rmd
This script runs the calculations for determining the AHP weights based on the responses from the expert questionnaires. It creates individual Pairwise Comparison Matrices (PCMs) and calculates both individual and aggregated priority weights. 
The script also identifies, quantifies, and adjusts inconsistencies in the data to provide adjusted priority weights with reduced inconsistencies.

- Processes expert questionnaire data.
- Calculates individual and aggregated priority weights.
- Identifies and adjusts inconsistencies.

### FAHP Analysis: FAHP_analysis.Rmd
This script calculates the Fuzzy AHP weights based on the PCMs generated in `AHP_analysis.Rmd`. It fuzzifies the inconsistency-corrected AHP PCMs and calculates individual and aggregated fuzzy weights. The final defuzzified value serves as the input for the HFVI calculation (`HFVI_calculation.Rmd`).

- Converts AHP pairwise comparison matrices into fuzzy PCMs.
- Computes fuzzy weights and defuzzifies them for HFVI calculation.

### HFVI Calculation: HFVI_calculation.Rmd
This script calculates the HFVI applied to a case study. It uses global and synthetic local data of a refugee camp setting (fictional refugee camp) as inputs to create individual indicator raster layers for subsequent 
spatial overlay using the HFVI equation with the FAHP weights obtained from `AHP_analysis.Rmd` and `FAHP_analysis.Rmd`. Further spatial analysis (spatial autocorrelation and indicator correlation matrix) is performed,  followed by sensitivity and uncertainty analysis using the FAHP-OAT Method (with fuzzy ranges from `FAHP_analysis.Rmd`). Finally, the script generates visualizations of the HFVI and uncertainty maps.

•	Reads processed indicator layers.
•	Performs spatial overlay using the HFVI equation with FAHP weights.
•	Conducts sensitivity and uncertainty analysis.
•	Visualizes HFVI and associated uncertainty maps.

This code can be adjusted for real world case studies by changing the input data for the individual indicator layers.

## Computational Environment 
•	Operating System: Windows 10 / macOS / Linux
•	Software Versions:
•	R version 4.2.1 (2022-06-23)
•	RStudio 2023.06+ (tested for Version 2023.09.1+494)

Key R packages: The following R packages and their versions were used in this project. The scripts automatically check and install the following R packages if not already installed. 

ahpsurvey : 0.4.1
arrow : 14.0.0.2
corrplot : 0.92
devtools : 2.4.5
dplyr : 1.1.4
fs : 1.5.2
fsr : 2.0.1.9000
FuzzyAHP : 0.9.5
ggpattern : 1.1.1
ggplot2 : 3.5.1
gridExtra : 2.3
here : 1.0.1
httr : 1.4.4
kableExtra : 1.3.4
knitr : 1.47
leaflet : 2.1.1
lubridate : 1.8.0
maptools : 1.1-4
mapview : 2.11.0
plotly : 4.10.0
RColorBrewer : 1.1-3
raster : 3.6-26
readr : 2.1.3
readxl : 1.4.1
rgdal : 1.5-32
sf : 1.0-15
spatialEco : 1.3-7
spatstat : 2.3-4
SpatMCDA : 0.0.1
stars : 0.5-5
stringr : 1.5.1
terra : 1.7-65
tidyverse : 1.3.2
tmap : 3.3-3
tmaptools : 3.1-1
XML : 3.99-0.11
xtable : 1.8-4
zoo : 1.8-12

## Reproducibility Instructions
1.	Clone this repository: git clone <repository_url>
2.	Open the R project file (.Rproj) in RStudio (recommended).
3.	Ensure the working directory is set to the repository root.
4.	Execute scripts in the following order: 
	- scripts/AHP_analysis.Rmd
	- scripts/FAHP_analysis.Rmd
	- scripts/HFVI_calculation.Rmd
5.	Outputs will be saved in the outputs/ directory.

## Computation Steps
Detailed steps for each analysis are documented in the R Markdown files.
Expected Execution Times:
- AHP Analysis: ~2 minutes.
- FAHP Analysis: ~1 minutes.
- HFVI Calculation: ~5 minutes (using the provided synthetic data)


## Credits
Kunz, Annika. (2024). "Developing a Spatially Explicit Humanitarian Flood Vulnerability Index for Refugee Camps using Fuzzy Multi-Criteria Decision Analysis". GitHub repository. https://github.com/akinnaznuk/HFVI
