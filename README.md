# NBA-efficiency-vs-Volume
Data driven analysis of NBA scoring efficiency vs volume
# Efficiency vs Volume: What Actually Wins Games?

## Overview

This replication package contains all code and documentation needed to reproduce the analysis examining whether scoring efficiency or scoring volume matters more for team success in the NBA. The analysis uses 360 NBA players from the 2023-24 season and applies statistical analysis, regression modelling, and data visualization to answer this fundamental basketball question.

The code runs in approximately 5-10 minutes on a standard desktop machine. The analysis produces 7 visualizations, statistical test results, player classifications into archetypes, and all supporting tables and figures referenced in the blog post and manuscript.

To replicate the analysis, install the required Python packages listed below, download the NBA data using the provided code, and run the Jupyter notebook cells in sequence.

---

## Data Availability and Provenance Statements

This analysis uses data from the official NBA Statistics API. The data are publicly available and no restricted access data are used.

### Statement About Rights

☐ I certify that the author(s) of the manuscript have legitimate access to and permission to use the data used in this manuscript.

The NBA Stats API provides publicly available data. No special permissions are required to access or use this data for research purposes.

### License for Data

The data are sourced from the NBA Official Stats API, which provides data in the public domain. The data are available without license restrictions for educational and research purposes.

### Summary of Availability

☐ All data are publicly available.

The NBA Stats API provides comprehensive player statistics for every game in the 2023-24 regular season. Data are accessed dynamically using the nba_api Python library and require an active internet connection during initial download.

### Details on Data Source

**NBA Player Statistics (2023-24 Regular Season)**

Source: NBA Official Stats API (nba_api Python library)
URL: https://github.com/swar/nba_api
Access: Publicly available, no authentication required
Format: JSON (converted to pandas DataFrame)
Sample Size: 360 players with minimum 500 minutes played (filtered from 572 total players)

The analysis uses the LeagueDashPlayerStats endpoint, which provides comprehensive statistics including:
- Points, rebounds, assists, steals, blocks
- Field goals made/attempted, 3-pointers, free throws
- Plus/Minus, minutes played, usage statistics
- True Shooting percentage calculated from raw stats

Data can be re-downloaded by running Cell 2 of the Jupyter notebook. A CSV export of the processed data is provided for reference.

Datafile: nba_player_stats_2023-24.csv (provided in data/ folder)

---

## Dataset List

The analysis uses a single dataset derived from the NBA Stats API. After downloading via the API, the data is cleaned, features are engineered, and the final analysis dataset contains 360 players with the following variables:

**Volume Metrics**
- PPG: Points Per Game
- Scoring_Volume: Field Goal Attempts
- Usage_Rate: Possessions consumed per game
- Assist_Volume: Assists per game

**Efficiency Metrics**
- TS_Pct: True Shooting % (accounts for all shot types)
- FG_Pct: Field Goal %
- Efficiency_Rating: Points generated per possession
- FT_Pct: Free Throw %

**Outcome Metric**
- Win_Contribution: Plus/Minus (team impact)

**Classification Variables**
- Player_Archetype: Classification into Elite, Balanced, or Efficient Role Player
- Height_Inches: Player height (derived from position averages)
- Height_Category: Binned height categories

All variables are documented with full descriptions in the Jupyter notebook (Cell 3: Data Cleaning & Feature Engineering).

---

## Computational Requirements

### Software Requirements

Python 3.8 or higher

Required packages:
- nba-api==1.11.4 (for accessing NBA Statistics API)
- pandas==2.0.0+ (data manipulation and analysis)
- numpy==1.24.0+ (numerical computing)
- matplotlib==3.7.0+ (visualization)
- seaborn==0.12.0+ (statistical visualization)
- scipy==1.11.0+ (statistical tests)
- jupyter==1.0.0+ (notebook environment)

Installation:
```bash
pip install nba-api pandas numpy matplotlib seaborn scipy jupyter
```

Or use the provided requirements file:
```bash
pip install -r requirements.txt
```

The replication package does not contain automatic setup scripts, but all dependencies are listed in requirements.txt for easy installation using pip.

### Controlled Randomness

The analysis does not use random number generators or pseudorandom number seeds. All results are deterministic and reproducible. The archetypes are classified using fixed thresholds (volume_score > 60, efficiency_score > 60) on normalized metrics.

### Memory, Runtime, Storage Requirements

**Summary**

Approximate time needed to reproduce the analyses on a standard desktop machine:

☐ <10 minutes
☐ 10-60 minutes (✓ ACTUAL: 5-10 minutes)
☐ 1-2 hours
☐ 2-8 hours
☐ 8-24 hours
☐ 1-3 days
☐ 3-14 days
☐ > 14 days

Approximate storage space needed:

☐ < 25 MBytes (✓ ACTUAL: ~10-20 MB with generated visualizations)
☐ 25 MB - 250 MB
☐ 250 MB - 2 GB
☐ 2 GB - 25 GB
☐ 25 GB - 250 GB
☐ > 250 GB
☐ Not feasible to run on a desktop machine

**Details**

The code was last run on a 4-core Intel-based laptop with 16GB RAM and 256GB SSD storage running Python 3.13. Execution time varies slightly depending on API response times (typically 30 seconds to 2 minutes for data download, 1-3 minutes for analysis and visualization generation).

The initial data download via the NBA API may take 1-2 minutes depending on internet connection speed. Subsequent runs using cached data are faster. All analysis, statistical tests, and visualization generation complete within 5 minutes on standard hardware.

---

## Description of Programs/Code

The analysis is organized in a single Jupyter notebook with 16 cells structured as follows:

**Cell 1: Imports and Setup**
Loads all required libraries and configures visualization settings. Must be run first.

**Cell 2: Download NBA Data**
Downloads 2023-24 regular season player statistics from the official NBA Stats API. Includes error handling and progress messages. Data is saved to CSV for future reference.

**Cell 3: Data Cleaning and Feature Engineering**
Cleans raw data, creates derived metrics (efficiency ratings, usage rates, player archetypes), and prepares dataset for analysis. Filters for players with 500+ minutes played.

**Cell 4: Exploratory Data Analysis**
Generates descriptive statistics and data quality checks. Shows distribution of key metrics and player counts by archetype.

**Cell 5: Regression Analysis**
Builds three regression models to determine whether volume or efficiency better predicts team success (Plus/Minus). Compares R-squared values across models.

**Cell 6-11: Visualizations**
Creates 7 publication-ready charts:
- efficiency_vs_volume.png: Main scatter plot with quadrants
- regression_importance.png: Coefficient comparison
- volume_impact.png: PPG vs Plus/Minus relationship
- efficiency_impact.png: TS% vs Plus/Minus relationship
- player_archetypes.png: Archetype distribution and impact
- archetype_boxplots.png: Performance by archetype
- correlation_heatmap.png: Full correlation matrix

**Cell 12: Statistical Tests**
Runs t-tests comparing efficient vs inefficient scorers and high-volume vs low-volume scorers. Includes ANOVA testing archetype differences.

**Cell 13-15: Analysis and Summary**
Top performers analysis, detailed archetype breakdowns, and executive summary with key findings and takeaways.

### License for Code

The code is provided for educational and research purposes. No specific license restriction is imposed on the code itself. Users are welcome to adapt and modify the code for their own analysis.

---

## Instructions to Replicators

Follow these steps in order to replicate the analysis:

1. Install Python 3.8 or higher on your computer

2. Install required packages:
```bash
pip install -r requirements.txt
```

3. Open Jupyter Notebook:
```bash
jupyter notebook Efficiency_vs_Volume.ipynb
```

4. Run all cells in sequence from top to bottom. Jupyter will execute each cell when you press Shift+Enter or click the Run button.

Alternatively, from the Jupyter interface:
- Click Kernel menu
- Select "Restart & Run All"
- This will run all 16 cells in sequence automatically

5. Expected output:
- Console output: Correlation coefficients, statistical test results, summary statistics
- Generated files: 7 PNG visualizations saved to current directory
- Interactive plots: Displayed in the notebook

### Details

Cell 2 (Download NBA Data): Requires internet connection. Will take 1-2 minutes depending on API response times. Data is saved to CSV file for future runs.

Cell 3 (Data Cleaning): Filters raw data to 360 players with 500+ minutes played. Engages all feature engineering and archetype classification. No external files required.

Cells 4-5 (Analysis): Run without external dependencies. All data comes from Cell 3 output.

Cells 6-11 (Visualizations): Generate PNG files in the current directory. File names correspond to section names (e.g., efficiency_vs_volume.png, regression_importance.png).

Cells 12-15 (Tests and Summary): Generate console output only. No files created, but results displayed in notebook.

If running individual cells out of sequence may produce errors. Always run from Cell 1 in order, or use Restart & Run All option.

---

## List of Tables and Programs

The provided code reproduces:

☐ All numbers provided in text in the paper
☐ All tables and figures in the paper
☐ Selected tables and figures in the paper, as explained and justified below

**Specific outputs:**

All 7 visualizations:
- efficiency_vs_volume.png: Generated by visualization cell, shows volume-efficiency-outcome relationship
- regression_importance.png: Generated by regression analysis cell
- volume_impact.png: Generated by volume analysis cell
- efficiency_impact.png: Generated by efficiency analysis cell
- player_archetypes.png: Generated by archetype analysis cell
- archetype_boxplots.png: Generated by distribution analysis cell
- correlation_heatmap.png: Generated by correlation cell

All statistical test results:
- Correlation coefficients (Cell 5 output)
- Regression R-squared values and coefficients (Cell 6 output)
- T-test statistics and p-values (Cell 12 output)
- Archetype summary statistics (Cell 15 output)

All numbers in the blog post and this README are directly reproducible from the code. The blog post references specific correlation values (e.g., TS% 0.340 vs PPG 0.241), regression model fits (5.79%, 11.56%), and player statistics (Embiid 34.7 PPG, 64.4% TS) that are all computed and displayed in the notebook.

---

## References

Ruggles, Steven M., et al. 2018. "IPUMS Terra: Integrated Data on Population and Environment." Minnesota Population Center. https://github.com/swar/nba_api

NBA Official Statistics. 2024. "NBA Stats API." Accessed via https://stats.nba.com and https://github.com/swar/nba_api

Pandas Development Team. 2023. "pandas: powerful Python data analysis toolkit." https://pandas.pydata.org/

NumPy Developers. 2023. "NumPy: Numerical Computing for Python." https://numpy.org/

Matplotlib Development Team. 2023. "Matplotlib: Python plotting." https://matplotlib.org/

Seaborn Development Team. 2023. "Seaborn: Statistical Data Visualization." https://seaborn.pydata.org/

SciPy Contributors. 2023. "SciPy: Scientific Python." https://scipy.org/

Project Jupyter. 2023. "Jupyter Notebook." https://jupyter.org/

---

## Acknowledgements

This project uses the nba_api Python library maintained by the open-source community. The analysis methodology follows best practices for reproducible data science research.
