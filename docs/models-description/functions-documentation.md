# Detailed Functions Documentation  
  
## Introduction  
  
The `Capacity` class is designed for analyzing and calculating mobile network capacity in a given area. It provides methods to analyze cell site coverage, population distribution, and network capacity based on various parameters such as bandwidth, spectrum allocation, and user data consumption.

## Functionalities and Calculations  
  
### Initializing the class (`init`)

To initialize the class, you need to provide the following parameters:

- **country_code** (`str`): ISO3 country code for the area of analysis.
- **data_dir** (`str`): Directory path for input data.
- **logs_dir** (`str`): Directory path for logs.
- **poi** (`PointOfInterestCollection`): Collection of points of interest.
- **cellsites** (`CellSiteCollection`): Collection of cell sites.
- **bw_L850** (`float`): Bandwidth in MHz for L700 to L900 spectrum.
- **bw_L1800** (`float`): Bandwidth in MHz for L1800 to L2100 spectrum.
- **bw_L2600** (`float`): Bandwidth in MHz for L2300 to L2600 spectrum.
- **cco** (`float`): Control channel overhead in percentage.
- **max_radius** (`int`): Maximum buffer radius for analysis.
- **min_radius** (`int`): Minimum buffer radius for analysis.
- **radius_step** (`int`): Step size for buffer radius increments.
- **angles_num** (`int`): Number of angles for analysis.
- **rotation_angle** (`float`): Rotation angle in degrees.
- **dlthtarg** (`float`): Download throughput target in Mbps.
- **nonbhu** (`float`): Connection usage in non-busy hours in percentage.
- **mbb_subscr** (`float`): Active mobile-broadband subscriptions per 100 people.

You also need to provide the following parameters, although these already come with default values:

- **use_secure_files** (`bool`, optional): Flag to use secure files for bandwidth data. Default is `False`.
- **sectors_per_site** (`int`, optional): Number of sectors per cell site. Default is `3`.
- **cellsite_search_radius** (`int`, optional): Cell site search radius in meters. Default is `35000`.
- **poi_antenna_height** (`int`, optional): Point of interest antenna height in meters. Default is `15`.
- **rb_num_multiplier** (`int`, optional): Resource block number multiplier. Default is `5`.
- **visibility** (`VisibilityPairCollection`, optional): Collection of visibility pairs. Default is `None`.
- **area** (`gpd.GeoDataFrame`, optional): Area of interest. Default is `None`.
- **dataset_year** (`int`, optional): Year of the dataset being used. Default is `2020`.
- **one_km_res** (`bool`, optional): Flag for using 1km resolution data. Default is `True`.
- **un_adjusted** (`bool`, optional): Flag for using UN-adjusted data. Default is `True`.
- **nbhours** (`int`, optional): Number of non-busy hours per day. Default is `10`.
- **oppopshare** (`int`, optional): Percentage of population using operator services. Default is `50`.
- **enable_logging** (`bool`, optional): Flag to enable logging. Default is `False`.
  
### Downlink Bitrate (`get_dl_bitrate`)

This method calculates the achievable downlink bitrate for given **distances**, considering multiple frequency bands (L850, L1800, L2600) and their respective bandwidths.

- The input is a list, numpy array, or pandas Series containing distances in meters.
- The output is a numpy array of downlink bitrates (in kbps) corresponding to each input distance.
- For each frequency band:
   - Uses lookup tables to find bitrates corresponding to input distances.
   - Handles out-of-range distances by assigning NaN values.
- Computes final bitrates as a weighted sum across all frequency bands.

### Resource Blocks Requirement Calculation (`poiddatareq`)   
  
The `poiddatareq` method is designed to calculate the number of resource blocks (RBs) necessary to meet a specific download throughput target at a certain distance from a cell site. This method is integral to network capacity analysis as it helps determine if a cell site can provide the required service level at varying distances. The method proceeds as follows:  
  
- It first checks whether the provided distance exceeds the maximum coverage radius of the cell site. If it does, the method concludes that the download throughput target cannot be met at that distance, and an infinite number of RBs are theoretically required.  
- If the distance is within the acceptable range, the method searches for the achievable downlink bitrate at a given distance using the `get_dl_bitrate` function.  
- The method then calculates the required number of RBs by dividing the download throughput target (converted to kbps) by the achievable bitrate per RB (accounting for the average number of RBs available for PDSCH).  
  
This method is vital for assessing the coverage and capacity limitations of a cell site and is instrumental in network planning and optimization efforts.  
  
### Bitrate Per Resource Block Calculation (`brrbpopcd`)  
  
The `brrbpopcd` method calculates the bitrate available per resource block at a specified population center distance. This is a key performance indicator that reflects how the network's capacity is distributed spatially. The method involves the following steps:  
  
- Using `get_dl_bitrate`, the method identifies the closest distance value that exceeds the given population center distance.  
- It retrieves the achievable bitrate associated with that distance for the specified bandwidth.  
- The method then divides the retrieved achievable bitrate by the average number of resource blocks available for PDSCH to determine the bitrate per resource block at the population center distance.  
  
This method is crucial for network performance analysis as it helps to gauge the efficiency of resource block usage in relation to the distance from the cell site, directly impacting the user experience.  
  
### Average User Bitrate in Non-Busy Hour Calculation (`avubrnonbh`)   
  
The `avubrnonbh` method computes the average bitrate experienced by a user during non-busy hours, providing an estimate of network capacity when it is not heavily loaded. The calculation is based on user data consumption patterns and considers the following parameters:  
  
- The average user data traffic volume per month (`udatavmonth`) expressed in gigabytes.  
- The percentage of network usage that occurs during non-busy hours (`nonbhu`).  
  
The method carries out a sequence of operations to transform the monthly data volume into an hourly rate, adjusting for the percentage of usage during non-busy hours, and converting the final figure into kilobits per second. The formula takes into account the average number of days in a month, the number of non-busy hours per day, and the conversion factors between gigabytes and kilobits.
  
This metric is of significant value for network operators to ensure that their networks are equipped to handle user demands during off-peak times, which is essential for maintaining a high quality of service.

### User Population Bitrate Per Sector (`upopbr`)

This method calculates the total bitrate needed to serve a given population within a cell sector, taking into account the average user bitrate, mobile broadband subscription rate, and the operator's market share.

- Its inputs are the average user bitrate in non-busy hour in kbps (`avubrnonbh`) and the total population in the area served by the cell sector.
- Its output is the user Population Bitrate in kbps.

### User Population Resource Blocks Utilisation (`upoprbu`)

This method calculates the number of resource blocks utilized by the user population in a cell sector.

- Its inputs are the total bitrate required by the user population in kbps (`upopbr`) and the bitrate per resource block at population center distance in kbps (`brrbpopcd`).`
- Its output is the user population resource blocks utilisation in units.

### Cell Site Available Capacity Check (`cellavcap`)

This method calculates the available capacity at a cell site by subtracting the utilized resource blocks from the total available resource blocks.

- Its inputs are the number of resource blocks available for the Physical Downlink Shared Channel (`avrbpdsch `) and the number of resource blocks utilized by the user population (`upoprbu `).`
- The output is the The available capacity at the cell site.

### Sufficient Capacity Checker (`sufcapch`)

This method determines whether the available capacity at a cell site is sufficient to meet the required download throughput target.

- Its inputs are the available capacity at the cell site (`cellavcap`) and the Resource Blocks Download Throughput Target (`rbdlthtarg`).
- The output is a True/False flag indicating whether there is sufficient capacity (cellavcap > rbdlthtarg) or not (cellavcap <= rbdlthtarg).

### Capacity Checker (`capacity_checker`)

This method performs a comprehensive capacity check for a cell site, combining the auxiliary functions above.

- Its inputs are:
    - Distance to the Point of Interest (`d`)
    - Population center distance (`popcd`)
    - Monthly data usage per user (`udatavmonth`)
    - Population served by the cell site (`pop`)
- The method calculates several intermediate values:
    - Target data rate based on distance (`rbdlthtarg`)
    - Bitrate per resource block at population center (`brrpopcd`)
    - Average user bitrate in non-busy hours (`avubrnonbh`)
- It then uses these to compute the final outputs:
    - User population bitrate (`upopbr`)
    - User population resource block utilization (`upoprbu`)
    - Available cell capacity (`cellavcap`)
    - Capacity check result (`capcheck`)

### Capacity Checker Using Buffers Around Cell Sites (`calculate_buffer_areas`)

This method performs spatial analysis and capacity assessment for cell sites by creating buffer areas and calculating various metrics. For more information, please refer to the `Network Capacity Model` section of this documentation. The method doesn't take any inputs beyond the class attributes. It performs several key operations:

- Geodata preparation
    - Buffer and ring creation around cell sites
    - Visibility analysis (if needed)
    - Capacity calculations at different levels

- The method calculates several intermediate values:
    - Voronoi polygons for cell sites
    - Buffer areas and rings around cell sites
    - Visibility between POIs and cell sites
    - Population per ring
    - Resource block requirements for download throughput

- It then uses these to compute the final outputs:
    - User population bitrate per ring
    - User population resource block utilization
    - Available cell capacity
    - Capacity sufficiency check

- The output is a tuple containing:
    - A dictionary of GeoDataFrames:
        - 'buffers': Buffer areas around cell sites
        - 'rings': Ring areas around cell sites
    - A GeoDataFrame of POIs within cell site coverage areas, including capacity analysis results
