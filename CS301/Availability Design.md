Many services/websites/applications can fail
![[week05_availability_01.png]]
## Availability (ISO25010)
This describes the degree to which a system, product or component is operational and accessible when required for use.
![[week05_availability_02.png]]
# Considerations
- Process and Data Node (e.g. Windows, Tomcat, Web App, DB):
	- Redundant process and data nodes, Clustering (Node config, Failure Detection, Fail-over) and Replication
- Network Node (e.g. Firewall Router)
	- Redundant
- Network Segment (e.g. SMU network, M1, StarHub, Singtel)
	- Redundant links
- Location (e.g. Disaster Recovery Data Centre)
	- Redundant
# Brewer's Cap Theorem
We can only have at most two of these properties for any shared data system
![[week05_brewers_cap_01.png]]![[week05_brewers_cap_02.png]]
## Discussion
![[week05_brewers_discussion.png]]
We want both C and A as consistency of item stock is important and availability of the service is also important
![[week05_CAP_example_01.png]]
# Ideas
## Separation Of Concern
Enables loose coupling for the components that provide critical services
![[week05_separation_of_concern.png]]
## Fault Tolerance
Enables detection and correction of errors before they become effective
![[week05_fault_tolerance.png]]
## Availability in Series
Total Availability is always lower than the availability of any component in the series
![[week05_availability_series.png]]
## Availability in Parallel
Total Availability is higher than individual links
![[week05_availability_parallel.png]]
# Redundancy
![[week05_redundancy.png]]
# Clustering
This is required to coordinate among redundant components
## Configuration
- ### Active / Passive
	- Redundant instance on standby which is only online when the associated primary node fails
- ### Active / Active
	- Multiple homogeneous nodes participate in the computational workload and provides a logical view of a single machine. Requires decisions to decide which node handles which request. A client connected to one node will continue to access the same node in the same session unless failure is known as session affinity or sticky session.
![[week05_clustering.png]]
# Detect Failures
## Pinging (Inbound to server)
![[week05_detect_failure_pinging.png]]
## Heartbeats (Outbound from server)
![[week05_detect_failures_heartbeats.png]]
# Recover Service
How to direct traffic to the other machine
- Client Based
- Load Balancer (add new component)
- DNS with primary IP and secondary IPs
- Virtual IP
## Fail-over
### Client Based
On request fail (e.g. exception or timeout)
- Client retry
- Client contacts backup
![[week05_client_based_failover.png]]
#### Client
```//other code  
Try {  
server = new Server(serverIPs[i]);  
server.doWork;  
} catch (IOException e) {  
server = new Server(serverIPs[++i]);  
//try again  
}
```
### Load Balancer
On request fail
- Change list
- Load Balancer contacts backup
![[CS301/images/week05_load_balancer.png]]
### DNS
DNS can have more than 1 IP entry (Primary and Secondary IPs)
![[week05_dns_failover.png]]
If an error occurs on the primary IP, the secondary server can be pinged to retrieve an answer to the client
![[week05_dns_failover_02.png]]
# Virtual IPs
Useful as the IP can be bound to any one of several machines
![[week05_virtual_ip_01.png]]
Only one machine is assigned the virtual IP at a given time.
During normal times, the virtual IP is assigned to one of the database servers.
![[week05_virtual_ips_02.png]]
If the cluster manager discovers that db server 1 is down, failover to db server 2 occurs.
![[week05_virutal_ips_03.png]]
### Example Web System
What is wrong with this system?
![[week05_example_web_system.png]]
Inconsistency between server 1 and 2. Server 2 does not have a record of the items added from server 1
# Session State
Transient data maintained by a software program and removed when the session ends. (e.g. Shopping Cart, web session)
Systems typically need to _preserve_ state under certain failure modes. (e.g. Customer can keep his login/cart item) if one web server instance fails.
## Storage
- ### Client
	- Stored in "hidden fields" in html forms or cookies
	- Sent between browser and server in every communication
- ### In-memory Server Sessions
	- Stored in server memory
	- Each server replicates its session state to other servers
- ### Database or Cache
	- Stored in centralised table or cache
	- All servers access this table or cache for session state
# Server availability and state management example
![[week05_example_01.png]]
## Failover Case 1
![[week05_example_failover_01.png]]
## Failover Case 2
![[week05_example_failover_02.png]]
# AWS Elastic Load Balancer
![[week05_load_balancer 1.png]]
Provides:
- High availability
- Health Checks
-  Security Features
- TLS termination
- Layer 4 or layer 7 load balancing
## Sticky Policy Configuration
Routes each request independently to the application with the smallest load by default. _Session affinity_ is available that enables the load balancer to bind a user's session to a specific application instance
## Multi-Load Balancer Pattern
Assigns multiple load balancers with different settings for the types of devices that are accessing the web application
![[week05_multi_load_balancer.png]]
## HA with Load Balancing
This consists of an internet facing load balancer ,which is deployed in the public subnet and balances traffic to web servers in 2 availability zones, and an internal load balancer which distributes traffic to EC2 instances from clients with access to the VPC for the load balancer.
![[week05_HA_load_balancing.png]]
## Elastic IP Addresses Enable HA
![[week05_enable_ha.png]]
# Availability Across Regions
## Route 53
An authoritative DNS service that translates domain names to IP addresses and tracks health status of resources and take action when error occurs.
![[week05_route_53.png]]