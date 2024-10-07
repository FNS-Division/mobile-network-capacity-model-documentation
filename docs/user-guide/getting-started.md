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

## Preparing your data

In order to conduct your analysis, you will need to provide the tool with the following geospatial data in CSV format:

- Points of interest locations
- Cell site locations

See the `input_data` section of this documentation page for more information.

It is also possible to provide data on the visibility status between each point of interest and cell site, but this is not a requirement as the checker automates these calculations in the background.

## Running your analysis

To conduct your analysis using the Mobile Network Capacity Model, follow these steps:

1. **Prepare Your Data**: 
   Place your input data files in the `data/input_data/<country-code>` directory. For example, for Spain, include your geospatial data in CSV format in sub-folder `data/input_data/ESP`. Use [ISO-3 three-letter codes](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-3) to identify your country. Ensure your data is in the correct format as specified in the technical documentation.

2. **Create a Jupyter Notebook to run your analysis**:
   Copy the notebook template from `notebooks/template.ipynb`, and insert the copy in the folder `notebooks`. For example, `notebooks/my_analysis.ipynb`.

3. **Configure Analysis Parameters**: 
   In your analysis notebook (for example, `notebooks/my_analysis.ipynb`) locate the configuration cells and adjust the parameters according to your specific analysis requirements.

4. **Execute the Analysis**:
   Run through the notebook cells sequentially. Each cell contains explanations and code for different stages of the analysis. During the analysis run, auxiliary files related to topography (Source: [NASA](https://portal.opentopography.org/raster?opentopoID=OTSRTM.082015.4326.1)) and population (Source: [Worldpop](https://www.worldpop.org/)) in the area covered by the points of interest and cell sites will automatically be downloaded into the `data/input_data/<country-code>` folder (in sub-folders called `srtm1` and `population`). You do not need to directly manipulate these files.

5. **Review Results**: 
   After execution, find your output data and visualizations in the `data/output_data/<country-code>` directory. The notebook will also display key results and graphs inline.

6. **Iterate if Necessary**: 
   Based on your initial results, you may want to adjust parameters or input data. Simply update the relevant sections and re-run the affected cells or the entire notebook.