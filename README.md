# Patent Examiner Network Analysis: Impact on Application Processing Efficiency
![McGill](https://img.shields.io/badge/McGill-ORGB672-red.svg)


## Table of Contents
- [Project Overview](#project-overview)
- [Research Questions](#research-questions)
- [Data Description](#data-description)
- [Methods](#methods)
- [Key Findings & Business Insights](#key-findings--business-insights)
- [Repository Structure](#repository-structure)
- [Contributors](#Contributors)
- [Citation](#citation)

## Project Overview

### Background & Motivation
This project analyzes how social networks among patent examiners at the United States Patent and Trademark Office (USPTO) influence application processing efficiency. Patent examination backlogs can create significant delays in innovation journeys, with potential economic impacts. By understanding the social dynamics that influence processing behaviors, we can identify strategies to improve efficiency throughout the organization.

### Research Questions
Our analysis investigates four primary research questions:

1. What organizational and social factors are associated with patent application processing times?
2. What role does network structure play in making examiners faster?
3. How do processing times vary by examiner traits, technology center, and case outcome?
4. Does exposure to multiple fast peers accelerate slower examiners' performance?

### High-Level Summary of Findings
Key findings indicate that examiners need exposure to at least three fast peers to adopt faster processing behaviors, and that an examiner's network position is significantly more influential than demographic factors in determining processing efficiency. Community-level norms and boundary-spanning individuals play a crucial role in facilitating the adoption of more efficient processing methods across the organization.

## Data Description

### Source of Examiner-Level Data
The dataset was derived from the USPTO Patent Examination Research Dataset created by Graham et al. (2015). The processed data was provided by Prof. Galperin, containing multiple years of examiner activity and relational information.

### Key Variables
- **Examiner demographics**: Gender, race, tenure at USPTO
- **Organizational structure**: Technology Centers/Work Groups (1600, 1700, 2100, 2400)
- **Application outcomes**: Status (issued, abandoned, pending)
- **Processing metrics**: Time to decision, backlog size
- **Social network**: Advice network connections between examiners

### Cleaning Steps
The data preparation involved several key steps:
1. Converting raw feather files to parquet format for more efficient processing
2. Standardizing date formats and calculating processing time metrics
3. Identifying and handling missing values in demographic data
4. Constructing network edges based on examiner interactions
5. Creating a consistent dataset merging both examiner attributes and network connections

## Methods

### Descriptive Statistics & EDA
We performed extensive exploratory data analysis to understand:
- Distribution of processing times across different technology centers
- Demographic breakdown of examiners
- Relationship between examiner attributes and processing efficiency
- Basic network metrics like degree centrality and clustering

### Network Construction & Complex Contagion Simulation Models
We implemented three progressive contagion models with increasing complexity:

- **Model I: Fractional Contagion Baseline**
  - Simple threshold models testing different k-values (number of exposures)
  - Basic adoption mechanism without temporal components

- **Model II: Longitudinal Exposure Causal Analysis**
  - Time-based adoption patterns
  - Accounting for repeated exposures over different time periods
  - Testing for causality in adoption behaviors

- **Model III: Time-Weighted Complex Contagion with Network Features**
  - Incorporating decay functions for exposure effects
  - Weighting influence by network position
  - Multi-feature model combining demographic and network attributes

### Regression & Network-Feature Analysis
We employed statistical models to quantify the relationships between:
- Network centrality measures and processing efficiency
- Demographic factors and processing times
- Community structure and adoption rates
- Combined effects of multiple variables on processing outcomes

## Key Findings & Business Insights

### Complex Contagion Threshold (k=3)
Our simulations revealed a clear complex contagion dynamic among examiners. The k=3 threshold model outperformed simpler alternatives, indicating that examiners require exposure to at least 3 distinct fast peers before adopting faster processing behaviors. This finding challenges simple diffusion models and suggests targeted interventions focusing on multiple exposures.

### Importance of Boundary Spanners & Community Norms
Examiners who bridge between different network communities are crucial for facilitating the adoption of faster processing methods across organizational boundaries. These boundary spanners serve as conduits for best practices and can accelerate organization-wide improvements in efficiency.

Community-level norms strongly drive individual behavior, with fast processing rates spreading within connected groups. Targeting interventions at the community level rather than at individuals can create more sustainable efficiency improvements.

### Strategic Intervention Recommendations
Based on our findings, we propose four strategic initiatives:

1. **Three-Mentor Program**: Connect slow examiners with multiple fast peers (minimum 3) across different work areas to leverage complex contagion dynamics
2. **Bridge-Spanner Recognition Program**: Identify and incentivize natural boundary-spanning examiners who facilitate knowledge transfer between organizational units
3. **Cluster Performance Dashboard**: Implement monitoring of community-level adoption metrics to track norm changes within and across examiner clusters
4. **Cross-Cluster Rotation Programs**: Establish structured rotations to transfer productive norms across organizational boundaries, specifically targeting high-performing clusters as sources

## Repository Structure

```
USTPO_Patent_Approval_Network_Analytics/
├── README.md                         ← Original project documentation
├── README-V2.md                      ← This enhanced documentation file
├── Data/                             ← Raw and cleaned datasets
│   ├── Uncleaned/                    ← Original USPTO data files
│   │   ├── app_data_starter_coded_202502.feather  ← Raw examiner data
│   │   └── edges_sample.csv          ← Raw network connections
│   ├── 00_edges_cleaned(Approach_1).csv   ← Processed network connections (first approach)
│   ├── 00_starterdata_cleaned(Approach_1).csv  ← Processed examiner data (first approach)
│   ├── 01_cleaned_edges_sample.csv   ← Further refined network connections
│   ├── 02_ONA_final_cleaned_dataset.csv  ← Final consolidated dataset
│   └── 03_ONA_final_cleaned_sample.csv   ← Sample of final dataset for quick testing
├── Code/                             ← Analysis scripts and notebooks
│   ├── 01_Data_Cleaning_(Approach_1).ipynb  ← Initial data cleaning approach
│   ├── 02_Data_Cleaning_(Final_Approach).ipynb  ← Refined data cleaning methodology
│   ├── 03_NetworkCentrality_Demographics.ipynb  ← Exploratory analysis and network visualization
│   ├── 04_Demographics_ProcessingTime.ipynb     ← Demographic analysis of examiners
│   ├── 05_Demograhic_Network_Analysis.ipynb  ← Combined demographic and network analysis
│   ├── 06_Complex_Contagion_Simulation.ipynb  ← Implementation of contagion models
│   └── network_graph.graphml         ← Exported network structure for visualization
└── USPTO Network Analytics Data Dictionary.pdf  ← Data variable definitions and descriptions
```


Required packages include:
- pandas
- numpy
- networkx
- matplotlib
- seaborn
- pyarrow
- jupyter
- scikit-learn
- statsmodels


## Contributors
- Maggie Huang 
- Ayda Elzohbi 
- Felix Veaux 
- Helia Mahmood Zadeh


## Citation

When using this dataset or analysis in academic work, please cite the original USPTO dataset:

Graham, S. J., Marco, A. C., & Miller, R. (2015). The USPTO patent examination research dataset: A window on the process of patent examination. *Journal of Economics & Management Strategy*, 24(1), 969-993. https://doi.org/10.2139/ssrn.2632731 

