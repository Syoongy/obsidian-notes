# Software Process
![[week02_software_process.png]]
1. Process 1 needs it's code to execute
2. OS moves process 1's data intot he CPU registers
3. CPU works on process 1's data
4. Process 2 needs it's code to be executed
5. OS moves process 1's data back to the process table
6. OS moves process 2's data into the CPU registers
7. CPU works on process 2's data
e.g. `cat file1 file2 | grep stuff`

# Virtual Machines vs Containers vs Unikernels
![[week02_vm_container_unikernel.png]]
# Layered Architecture Style
This organises the structure into a stack of layers (group of components). Each layer further describes the key components within it. This ensures a logical separation of software components.

Each layer may be dependent on one or more layers below is but is independent of those above it. Layers can also be open or closed (can/cannot be bypassed)
![[week02_layered_architecture.png]]

# Multitenancy on the cloud
![[week02_multitenancy.png]]
How do we ensure the clients have the stacks that they need (Clients can have different needs and requirements)?
Different stacks are built to cater to any client. The image above showcases the different types of stacks.

# Distributed Systems and Integration
![[week02_distributed_systems_and_integration.png]]
# Client Server Architecture Style
![[week02_client_server_arch.png]]
Requires a client and a server. The internet represents the biggest client server architecture (Websites usually call APIs or just accessing of websites).

The server component provides one or more services through API or RPC and the client can then invoke these services (website calls for a list of movies).

This can be synchronous or asynchronous communication

Peer to Peer - Each component is both a client invoking a set of services on the server component and also providing the same set of services for other components to invoke

# Tiered Architecture Style
![[week02_tiered_arch.png]]
- Each tier consists of a set of components that are physically separated from other software components in other tiers
- These tiers offer a service to an ultimate consumer. Each tier acts as a server for its caller and client to the next tier in the architecture. Can be 2 or more tiers E.g. n-tiered
- Some tiers can be bypassed

# Network Zones and Proxy
![[week02_network_zones_and_proxy.png]]
- Demilitarised Zone (DMZ) separates a purely internal network from an external network
- Reverse proxy provides access to internal servers behind a firewall
- Forward proxy provides access to external servers for internal servers that are behind a firewall

# Network Diagram
![[week02_network_diagram_example_1.png]]
![[week02_network_diagram_summary_1.png]]
![[week02_network_diagram_example_2.png]]
This example may seem correct but is actually bad for availability. If the load balancer or DB fails, the service will be unable to function.

![[week02_network_diagram_example_3.png]]
Data can be synced on the end user's local environment from the data centre. This ensures availability of data even if the internet is down. This however, may result in inconsistent or incorrect data if the internet connection is loss.
# Air Gap
![[week02_airgap.png]]