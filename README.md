# USPTO Patent Examiner Network Analysis

## Project Overview

This project analyzes how social networks among patent examiners at the USPTO influence application processing efficiency. Through network analysis and complex contagion models, we investigate how processing behaviors spread among examiners across different technology centers. The research provides insights into the social dynamics that impact patent examination speed and offers practical recommendations for reducing application backlogs.

Key findings indicate that examiners need exposure to at least three fast peers to adopt faster processing behaviors, and that an examiner's network position is significantly more influential than demographic factors in determining processing efficiency.

## Research Questions

Our analysis investigates four primary research questions:

1. What organizational and social factors are associated with patent application processing times?
2. What role does network structure play in making examiners faster?
3. How do processing times vary by examiner traits, technology center, and case outcome?
4. Does exposure to multiple fast peers accelerate slower examiners' performance?

## Data Description

The dataset contains detailed information about USPTO patent examiners, including:

- **Examiner demographics**: Gender, race, tenure at USPTO
- **Organizational structure**: Technology Centers/Work Groups (1600, 1700, 2100, 2400)
- **Application outcomes**: Status (issued, abandoned, pending)
- **Processing metrics**: Time to decision, backlog size
- **Social network**: Advice network connections between examiners

The data was cleaned and provided by Prof. Galperin, containing multiple years of examiner activity and relational information.

## Methodology

Our approach combines exploratory data analysis with advanced network analysis techniques:

1. **Exploratory Analysis**: Examining distributions of demographic factors and processing times
2. **Network Construction**: Building advice networks from examiner interactions
3. **Complex Contagion Modeling**: Implementing three progressive models:
   - **Model I**: Fractional Contagion Baseline - Testing basic threshold models
   - **Model II**: Longitudinal Exposure Causal Analysis - Analyzing repeated exposures
   - **Model III**: Time-Weighted Complex Contagion with Network Features - Incorporating decay functions and network position

Model performance was evaluated using Jaccard similarity measures comparing predicted adoption patterns with actual behavioral changes.

## Project Structure

```
patent-examiner-network/
├── data/
│   ├── raw/                      # Original patent examiner data
│   ├── processed/                # Cleaned and transformed datasets
│   └── network/                  # Constructed examiner networks by time period
├── notebooks/
│   ├── 01_data_cleaning.ipynb    # Data preprocessing and cleaning
│   ├── 02_exploratory_analysis.ipynb  # EDA of demographics and processing times
│   ├── 03_network_construction.ipynb  # Building examiner advice networks
│   ├── 04_basic_network_analysis.ipynb  # Network metrics and visualizations
│   └── 05_contagion_simulations.ipynb  # Complex contagion modeling
├── src/
│   ├── data/
│   │   ├── preprocessing.py      # Functions for data cleaning
│   │   └── network_builder.py    # Functions to construct networks
│   ├── features/
│   │   ├── demographic_features.py  # Examiner attribute engineering
│   │   └── network_features.py   # Network metric calculations
│   ├── models/
│   │   ├── fractional_threshold.py  # Model I implementation
│   │   ├── causal_exposure.py    # Model II implementation
│   │   └── complex_contagion.py  # Model III implementation
│   └── visualization/
│       ├── demographic_viz.py    # Demographics visualization functions
│       ├── processing_time_viz.py # Processing time visualization functions
│       └── network_viz.py        # Network visualization utilities
├── reports/
│   ├── figures/                  # Generated visualizations
│   └── final_report.pdf          # Complete project report
├── requirements.txt              # Project dependencies
└── README.md                     # Project documentation
```

### Directory Descriptions

- **data/**: Contains all data files used in the project
  - **raw/**: Original, unmodified USPTO examiner data
  - **processed/**: Cleaned data ready for analysis
  - **network/**: Network data extracted from examiner relationships

- **notebooks/**: Jupyter notebooks for each step of the analysis pipeline
  - Sequential notebooks from data preparation to complex modeling

- **src/**: Modular Python code organized by functionality
  - **data/**: Data processing utilities
  - **features/**: Feature engineering for both demographic and network attributes
  - **models/**: Implementation of the three contagion models
  - **visualization/**: Visualization functions for different data types

- **reports/**: Analysis outputs and documentation
  - **figures/**: Generated visualizations and charts
  - **final_report.pdf**: Comprehensive analysis report

## Key Findings

Our analysis revealed several significant insights:

- **Complex contagion dynamics**: Examiners require exposure to at least 3 distinct fast peers before adopting faster processing behaviors (k=3 threshold model outperformed simpler alternatives)
- **Network position dominance**: An examiner's position in the advice network (especially boundary spanning roles) is more influential than demographic factors in predicting processing efficiency
- **Community-level effects**: Strong evidence that cluster-level norms drive individual behavior, with fast processing rates spreading within connected communities
- **Bridge importance**: Examiners who bridge between different network communities are crucial for facilitating the adoption of faster processing methods across organizational boundaries

## Business Recommendations

Based on our findings, we propose four strategic initiatives:

1. **Three-Mentor Program**: Connect slow examiners with multiple fast peers (minimum 3) across different work areas to leverage complex contagion dynamics
2. **Bridge-Spanner Recognition Program**: Identify and incentivize natural boundary-spanning examiners who facilitate knowledge transfer between organizational units
3. **Cluster Performance Dashboard**: Implement monitoring of community-level adoption metrics to track norm changes within and across examiner clusters
4. **Cross-Cluster Rotation Programs**: Establish structured rotations to transfer productive norms across organizational boundaries, specifically targeting high-performing clusters as sources

## Installation and Usage

To set up the project environment:

```bash
# Clone the repository
git clone https://github.com/username/patent-examiner-network.git
cd patent-examiner-network

# Create and activate virtual environment (optional)
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

To run the analysis pipeline:

```bash
# Run notebooks in sequence
jupyter notebook notebooks/01_data_cleaning.ipynb
```

For specific analyses:

```python
# Example: Run complex contagion simulation
from src.models.complex_contagion import simulate_contagion

# Load preprocessed network
import networkx as nx
G = nx.read_gpickle("data/network/examiner_network_2015.gpickle")

# Run simulation with k=3 threshold
results = simulate_contagion(G, threshold=3, decay_rate=0.2)
```

## Technologies Used

- **Python**: Primary programming language
- **NetworkX**: Graph creation and analysis
- **Pandas**: Data manipulation and cleaning
- **Scikit-learn**: Machine learning components
- **Matplotlib/Seaborn/Plotly**: Data visualization
- **Statsmodels**: Statistical analysis
- **Jupyter**: Interactive development and presentation

## Contributors

- Maggie Huang (261229497)
- Ayda Elzohbi (260899679)
- Felix Veaux (260973626)
- Helia Mahmood Zadeh (261224416)

## References

- Graham, S., Marco, A., & Miller, R. (2015). The USPTO patent examination research dataset: A window on the process of patent examination.
- Centola, D., & Macy, M. (2007). Complex contagions and the weakness of long ties. American Journal of Sociology, 113(3), 702-734.
- Uzzi, B., & Spiro, J. (2005). Collaboration and creativity: The small world problem. American Journal of Sociology, 111(2), 447-504.
- Burt, R. S. (2004). Structural holes and good ideas. American Journal of Sociology, 110(2), 349-399.
