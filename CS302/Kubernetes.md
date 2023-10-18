# Container Orchestration
We have containers and some CI/CD. How do we meet the demands of production?
- Microservices are designed to be independently scalable
	- Provisioning and deployment
	- Resource allocation
	- Scaling up/down containers
	- Auto healing containers
	- Load balancing
- ECS and Kubernetes are used to automate these tasks
# Kubernetes
## Declarative Model
Manifest files (YAML) are used to tell Kubernetes what we want
- Which images to use
- How many replicas
- Which ports to listen
- Auto scalling conditions
The aim is to achieve the _"desired state"_ that is declared while observing the _"observed state"_. If observed $\neq$ desired, Kubernetes will perform the tasks required to achieve the desired state.
![[week10_k8_01.png]]
## Cluster
![[week10_k8_02.png]]
## Pods
- Basic unit of deployment
- Consist of one or more containers that share an internal address and storage volume
- Disposable and replaceable ("ephemeral")
	- A container may crash - Easier to dispose and replace the Pod
	- The Node may go down - Create a replacement Pod on another
![[week10_k8_03.png]]
![[week10_k8_04.png]]
## Deployments
- Declarative updates for (replica sets) of Pods
	- Image to use
	- Port to listen on
	- Replica amount
- Described desired state in a YAML file
- Deployment Controller changes the actual state to the desired state at a controlled rate
![[week10_k8_05.png]]
![[week10_k8_06.png]]
## Services
- Proves a static network location that exposes some Deployment / Pods
	- A form of infrastructure-provided service discovery
- Abstract way to expose Pods over the network
- Service locations are stable even if the underlying Pods are restarted, removed, or scaled-up
	- Simple load-balancing, e.g. randomly choosing a Pod from the set
![[week10_k8_07.png]]
![[week10_k8_08.png]]
### Service Types
- ClusterIP
	- Expose the Service on a cluster-internal IP
	- Reachable only from within the cluster
- NodePort
	- Expose the Service on each Node's UP at a static port
	- Reachable outside the cluster using `http://<NodeIP>:<NodePort>``
- LoadBalancer
	- Exposes the Service externally using a cloud provider's load balancer (e.g. AWS)
## Ingress
This helps with the limitations in Kubernetes:
- NodePorts only work on high port numbers + requires knowledge of node names / IPs
- LoadBalancers need a 1-1 with cloud load balancers
- 25 internet facing microservices would need 25 cloud load balancers
- We fix this by exposing multiple Services through a single cloud load-balancer
- Creates a LoadBalancer on port 80 or 443, then uses host-based and path-based routing to send traffic to backend Services
![[week10_k8_09.png]]
### Controller
- In addition to an Ingress object, clusters require an _Ingress controller_ to implement it
- Some k8s clusters provides controllers (Google GKE)
- Otherwise, just install one (nginx Ingress, Kong Ingress)
### Path-based Routing
![[week10_k8_10.png]]
### Host-based Routing
![[week10_k8_11.png]]
## Auto-Healing
### Keeping Pods Alive
- Liveness probes are used to check the health of Pods
	- Ping /health endpoint every 10s
	- Restart Pod if unhealthy
- Ensures availability despite bugs / instability
### Zero-Downtime Rolling Updates
- Users expect applications to be always available and developers are expected to deploy multiple times a day
- Kubernetes incrementally updates Pods using a rolling update
	- i.e. Create a new Pod, wait for it to be ready then destroy an old one
	- By default, max no. of Pods that can be unavailable during an update is 25%
	- Maximum no. of extra Pods that can exist during an update is 25%
- Services only load-balance traffic to available Pods during updates
![[week10_k8_12.png]]
![[week10_k8_13.png]]
### Auto-Scaling
- Optimises resource usage/costs by scaling a cluster up and down in line with demand
- Uses a Deployment object to request CPU resources
- Use a "Horizontal Pod Autoscaler" object to declaratively specify
	- e.g. Average CPU utilisation of 50% across all pods
	- Min / Max no. of replicas that can be deployed to achieve target
- Automatically adjusts up/down according to demand
![[week10_k8_14.png]]
## Summary
Kubernetes is a powerful container orchestration system. It uses a declarative model which is specified by the developer. Master nodes are used to ensure the desired state is attained and maintained. Finally, new container images can be deployed in zero-downtime rollouts.
