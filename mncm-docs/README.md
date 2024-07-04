## Repository structure

```sh
mobile-network-capacity-model
├── README.md
├── app.py
├── data
│   ├── input_data
│   │   ├── ESP-1697916284-6wv8-cellsite.csv
│   │   ├── ESP-1708423221-tgah-visibility.csv
│   │   ├── MobileBB_Traffic_per_Subscr_per_Month.csv
│   │   ├── active-mobile-broadband-subscriptions_1711147050645.csv
│   │   ├── area.gpkg
│   │   ├── bwdistance_km.csv
│   │   ├── bwdlachievbr_kbps.csv
│   │   ├── bwrsrp_dbm.csv
│   │   ├── bwulachievbr_kbps.csv
│   │   ├── mobile-broadband-internet-traffic-within-the-country_1711147118571.csv
│   │   └── population.tif
│   └── output_data
│       ├── MobileBB_Traffic_per_Subscr_per_Month.csv
│       └── network_capacity.csv
├── environment.yml
├── logs
│   └── app_timestamp.log
├── mobile_capacity
│   ├── capacity.py
│   └── spatial.py
├── notebooks
│   └── analyses.ipynb
└── tests
    ├── confest.py
    └── unit
        └── test_class.py
```

## Summary of methods

![capacity_checker](documentation/capacity_checker.drawio.png)

## Installation Steps

1. **Clone the Repository:**
    Clone the repository to your local machine using the following command:

   ```bash
   git clone git@ssh.dev.azure.com:v3/ITUINT/ConnectivityToolkit/mobile-network-capacity-model
   ```

2. **Navigate to the directory:**
    ```bash
    cd mobile-network-capacity-model
    ```

3. **Create a virtual environment with the required dependencies via [conda](https://www.anaconda.com/download):**<br><br>
   ```bash
   conda install -n base conda-libmamba-solver
   conda env create --file environment.yml --solver libmamba
   conda activate mobilecapacityenv
    ```

4. **Run analysis in notebooks**<br><br>
Run the analysis in `notebooks/app.ipynb`

5. **Deploy streamlit app locally**<br><br>
   ```bash
   conda activate mobilecapacityenv
   streamlit run app.py
    ```
Use keyborad shortcut `Ctrl+C` to terminate the local deployment.
