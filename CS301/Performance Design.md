# Performance (ISO 25010)
(When performing its functions to meet requirements)
- ## Time Behaviour
	- Response and processing times and throughput rate of a product or system
- ## Resource Utilisation
	- Amounts and types of resources used by a product or system
- ## Capacity
	- Maximum limits
# Performance Design
## Load Balancing
![[week06_load_balancing.png]]
## Parallel Execution
![[week06_parallel_execution.png]]
## Data Partitioning
![[week06_data_partitioning.png]]
![[week06_data_partitioning_02.png]]
![[week06_data_partitioning_03.png]]
## Caching
![[week06_caching_01.png]]
### Cache Efficiency
![[week06_cache_efficiency.png]]
## Pre-fetch
![[week06_pre_fetch.png]]
## Flow Control
![[week06_flow_control.png]]
# Measuring Performance
![[week06_performance_measuring.png]]
# Multi-Region High Availability and DNS
![[week06_ha_dns.png]]
# Auto Scaling
## Typical Traffic loads
### Weekly
![[week06_weekly_traffic.png]]
### November
![[week06_nov_traffic.png]]
- Launches/terminates instances based on specified conditions
- Automatically registers new instances with load balancers when specified
- Can launch across Availability Zones
## How it works
![[week06_scaling_01.png]]
![[week06_scaling_02.png]]
## Choosing Minimum Capacity Size
![[week06_scaling_minimum.png]]

- How many users to support
- Use past records to gauge users (Highest and lowest values with some buffer)
- Number of clients they have
![[week06_scaling_ha.png]]
![[week06_scaling_maximum.png]]
## Steps
![[week06_scaling_steps_01.png]]
There is a time delay to set up and tear down servers
![[week06_scaling_steps_02.png]]
![[week06_scaling_steps_03.png]]
In the above scenario, we should note the warm-up period
![[week06_scaling_steps_04.png]]
![[week06_scaling_steps_05.png]]
![[week06_scaling_steps_06.png]]
![[week06_scaling_steps_07.png]]
![[week06_scaling_steps_08.png]]
- We should avoid auto scaling tthrashing
	- be cautious about scaling in; avoid aggressive instance termination
	- Scale out early, scale in slowly
- Se the min/max capacity carefully
