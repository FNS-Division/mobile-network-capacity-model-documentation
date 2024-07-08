## Detailed Method Descriptions  
  
## Introduction  
  
The `Capacity` class ... :
  
## Functionalities and Calculations  
  
The `Capacity` class ... :
  
### 1. Resource Blocks Requirement Calculation (`poiddatareq`)   
  
The `poiddatareq` method is designed to calculate the number of resource blocks (RBs) necessary to meet a specific download throughput target at a certain distance from a cell site. This method is integral to network capacity analysis as it helps determine if a cell site can provide the required service level at varying distances. The method proceeds as follows:  
  
- It first checks whether the provided distance exceeds the maximum coverage radius of the cell site. If it does, the method concludes that the download throughput target cannot be met at that distance, and an infinite number of RBs are theoretically required.  
- If the distance is within the acceptable range, the method searches for the closest higher distance value in the preloaded `bwdistance_km` dataset to identify the corresponding achievable downlink bitrate from the `bwdlachievbr` dataset for the given bandwidth.  
- The method then calculates the required number of RBs by dividing the download throughput target (converted to kbps) by the achievable bitrate per RB (accounting for the average number of RBs available for PDSCH).  
- The calculated number of required RBs is stored in the `rbdlthtarg_result` attribute for later reference.  
  
This method is vital for assessing the coverage and capacity limitations of a cell site and is instrumental in network planning and optimization efforts.  
  
### 2. Bitrate Per Resource Block Calculation (`brrbpopcd`)  
  
The `brrbpopcd` method calculates the bitrate available per resource block at a specified population center distance. This is a key performance indicator that reflects how the network's capacity is distributed spatially. The method involves the following steps:  
  
- Utilizing two preloaded datasets, `bwdistance_km` and `bwdlachievbr`, which contain information on distance samples for different bandwidths and their corresponding achievable downlink bitrates, the method identifies the closest distance value that exceeds the given population center distance.  
- It retrieves the achievable bitrate associated with that distance for the specified bandwidth.  
- The method then divides the retrieved achievable bitrate by the average number of resource blocks available for PDSCH to determine the bitrate per resource block at the population center distance.  
- The result of this calculation is stored in the `brrbpopcd_result` attribute for subsequent use.  
  
This method is crucial for network performance analysis as it helps to gauge the efficiency of resource block usage in relation to the distance from the cell site, directly impacting the user experience.  
  
### 3. Average User Bitrate in Non-Busy Hour Calculation (`avubrnonbh`)   
  
The `avubrnonbh` method computes the average bitrate experienced by a user during non-busy hours, providing an estimate of network capacity when it is not heavily loaded. The calculation is based on user data consumption patterns and considers the following parameters:  
  
- The average user data traffic volume per month (`udatavmonth`) expressed in gigabytes.  
- The percentage of network usage that occurs during non-busy hours (`nonbhu`).  
  
The method carries out a sequence of operations to transform the monthly data volume into an hourly rate, adjusting for the percentage of usage during non-busy hours, and converting the final figure into kilobits per second. The formula takes into account the average number of days in a month, the number of non-busy hours per day, and the conversion factors between gigabytes and kilobits. The calculated average user bitrate for non-busy hours is then stored in the `avubrnonbh_result` attribute.  
  
This metric is of significant value for network operators to ensure that their networks are equipped to handle user demands during off-peak times, which is essential for maintaining a high quality of service.  

## Conclusion  
  
The `Capacity` class ...  