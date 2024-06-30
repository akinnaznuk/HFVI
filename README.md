# Humanitarian Flood Vulnerability Index (HFVI): Weight calculation and Case Study Application & Analysis
This repository contains code and documentation of the master thesis:
"Developing a Spatially Explicit Humanitarian Flood Vulnerability Index for Refugee Camps using Fuzzy Multi-Criteria Decision Analysis"
and contains the files for the Analytical Hierarchy Process (AHP), Fuzzy Analytical Hierarchy Process (FAHP), 
and the Humanitarian Fuzzy Vulnerability Index (HFVI) applied to the Mahama Case Study.

## Overview
This repository contains three main scripts, each performing a specific part of the analysis:

1. **AHP Analysis**: Calculates the AHP weights based on expert questionnaire responses.
2. **FAHP Analysis**: Calculates the Fuzzy AHP weights using the outputs from the AHP analysis.
3. **HFVI Calculation**: Applies the HFVI to the Mahama Case Study using the outputs from the FAHP analyses.

## AHP Analysis: AHP.Rmd
This script runs the calculations for determining the AHP weights based on the responses from the expert questionnaires. 
It creates individual Pairwise Comparison Matrices (PCMs) and calculates both individual and aggregated priority weights. 
The script also identifies, quantifies, and adjusts inconsistencies in the data to provide adjusted priority weights with reduced inconsistencies.

## FAHP Analysis: FAHP.Rmd
This script calculates the Fuzzy AHP weights based on the PCMs generated in `AHP.Rmd`. 
It fuzzifies the inconsistency-corrected AHP PCMs and calculates individual and aggregated fuzzy weights. 
The final defuzzified value serves as the input for the HFVI calculation (`HFVI.Rmd`).

## HFVI Calculation: HFVI.Rmd
This script calculates the HFVI applied to the Mahama Case Study. 
It uses data from the Mahama Camp as inputs to create individual indicator raster layers for subsequent 
spatial overlay using the HFVI equation with the FAHP weights obtained from `AHP.Rmd` and `FAHP.Rmd`. 
Further spatial analysis (spatial autocorrelation and indicator correlation matrix) is performed, 
followed by sensitivity and uncertainty analysis using the FAHP-OAT Method (with fuzzy ranges from `FAHP.Rmd`). 
Finally, the script generates visualizations of the HFVI and uncertainty maps.

This code can be adjusted for other case studies by changing the input data for the individual indicator layers.

## Usage
To use the scripts in this repository, clone the repository:
   ```sh
   git clone https://github.com/akinnaznuk/HFVI.git

## Credits
Kunz, Annika. (2024). "Developing a Spatially Explicit Humanitarian Flood Vulnerability Index for Refugee Camps using Fuzzy Multi-Criteria Decision Analysis". GitHub repository. https://github.com/akinnaznuk/HFVI

   
