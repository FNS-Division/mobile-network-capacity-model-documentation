## Prerequisites

Before you begin, ensure you have the following installed:
- Python 3.9
- Conda
- Jupyter Notebook or JupyterLab

You can verify the installations by running these commands:

```bash
python --version
conda --version
jupyter --version
```

If any of these commands fail or show an outdated version:
- Python: Download from [python.org](www.python.org)
- Conda: Follow the official [Conda installation guide](https://conda.io/projects/conda/en/latest/user-guide/getting-started.html)
- Jupyter: Install via Conda after setting up your environment.

```bash
conda install jupyter
```

## Installation steps

1. Clone the Repository:
    Clone the repository to your local machine using the following command:

```bash
git clone git@ssh.dev.azure.com:v3/ITUINT/ConnectivityToolkit/mobile-network-capacity-model
```

2. Navigate to the directory:
```bash
cd mobile-network-capacity-model
```

3. Create a virtual environment with the required dependencies via [conda](https://www.anaconda.com/download):
```bash
conda env create --file environment.yml
conda activate mobilecapacityenv
```

## Running your analysis

To conduct your analysis using the Mobile Network Capacity Model, follow these steps:

1. Prepare Your Data: 
   Place your input data files in the `data/input_data` directory. Ensure your data is in the correct format as specified in the technical documentation.

2. Configure Analysis Parameters: 
   Open the `notebooks/analyses.ipynb` notebook. Locate the configuration cell and adjust the parameters according to your specific analysis requirements.

3. Execute the Analysis:
   Run through the notebook cells sequentially. Each cell contains explanations and code for different stages of the analysis.

4. Review Results: 
   After execution, find your output data and visualizations in the `data/output_data` directory. The notebook will also display key results and graphs inline.

5. Iterate if Necessary: 
   Based on your initial results, you may want to adjust parameters or input data. Simply update the relevant sections and re-run the affected cells or the entire notebook.