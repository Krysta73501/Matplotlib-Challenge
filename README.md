# Matplotlib-Challenge

Pymaceuticals Inc. conducts an analysis to explore the relationship between various drug regimens and their effects on tumor volume in mice. The primary focus is on understanding how the Capomulin regimen impacts tumor growth relative to other treatments, emphasizing the role of mouse weight in treatment efficacy.

# Dependencies
The project requires the following Python libraries:

matplotlib
pandas
numpy
scipy
python
Copy code
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as st

# Data
The analysis uses two main datasets:

Mouse_metadata.csv: Contains metadata about the mice used in the study.
Study_results.csv: Contains the study results, including tumor volumes and treatment regimens.
The data is merged into a single DataFrame for analysis.

# Usage
To run the analysis, execute the following steps in a Jupyter Notebook environment:

Load the data:

mouse_metadata_path = "data/Mouse_metadata.csv"
study_results_path = "data/Study_results.csv"

mouse_metadata = pd.read_csv(mouse_metadata_path)
study_results = pd.read_csv(study_results_path)

Merge the data:

merged_data = pd.merge(study_results, mouse_metadata, how="left", on="Mouse ID")
Check for duplicates and clean the data:

duplicate_mice = merged_data[merged_data.duplicated(subset=['Mouse ID', 'Timepoint'], keep=False)]
clean_df = merged_data.drop_duplicates(subset='Mouse ID')
Generate summary statistics:

summary_stats = merged_data.groupby('Drug Regimen')['Tumor Volume (mm3)'].agg(['mean', 'median', 'var', 'std', sem])
Analyze specific drug regimens and visualize the data:

max_timepoint = merged_data.groupby('Mouse ID')['Timepoint'].max().reset_index()
merged_df = pd.merge(max_timepoint, merged_data, on=['Mouse ID', 'Timepoint'])

# Features
Data cleaning to ensure unique mouse entries.
Summary statistics generation for tumor volumes.
Analysis of specific drug regimens.
Visualization of tumor volume distributions and relationships.

# Contributors
Krysta Sharp

# Acknowledgements
Portions of the code were generated with the assistance of ChatGPT by OpenAI to assist with correction of coding errors.
