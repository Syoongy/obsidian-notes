# Strangler Fig Pattern
**Strangler vines** – "they seed in the upper branches of a fig tree, and gradually work their way down until they root in the soil. Over time, they _strangle and kill the tree_ that was their host."
This is the metaphor used for rewriting a large, important system.
We want to create a new system around the "edges" of the old.
## Gradually Decomposing a Monolith
We can use this pattern to gradually decompose a monolith into microservices.
Essentially, we build a new service that replaces _some_ functionality of the monolith
![[week07_monolith_decomposition.png]]
We then decouple the system into _layers of services_
### Service-Oriented Architecture (SOA) Layers
![[week07_soa_01.png]]
#### But what if a service requires a major update?
We now want a non-backwards compatible change to the API
### Versioned APIs
We can implement versioned APIs! (e.g. /v1/games and /v2/games).
This also applies the strangler fig pattern (New and old APIs co-exist).
This allows us to modify the service without impacting its clients and the system becomes more loosely coupled.
![[week07_api_versioning_01.png]]
However... there is still lots of coupling
![[week07_coupling_01.png]]
# API Gateways
## Pattern
![[week07_api_gateway_pattern.png]]
This allows for one standard api for all our clients to query from. It acts as a single point of access for external clients.
Essentially, it is a specific type of reverse proxy implementation
![[week07_api_gateway_02.png]]
### Composition
![[week07_api_gateway_composition.png]]
### Protocol Translation
![[week07_api_gateway_protocol_translation.png]]
### Edge Functions
- A request-processing function implemented at the "edge" of an application
- Examples include:
	- Authentication - Verifying client identity
	- Rate limiting - capping requests per second from clients
	- Caching - cache responses to commmon requests
	- Metrics/logging - for billing and/or usage analysis
- Can be implemented in the backend services or in the API gateway
![[week07_edge_auth_01.png]]
At the API Gateway level
![[week07_edge_logging.png]]
Logging can be done at all 3 layers
![[week07_edge_caching_01.png]]
Probably at the API gateway to benefit the most users and provide the fastest result
## Strangler Pattern
![[week07_strangler_api_gateway.png]]
![[week07_api_gateway_pros_cons.png]]
## Implementations
### Backends for Frontends (BFF) Pattern
![[week07_bff_pattern_01.png]]
![[week07_bff_pattern_02.png]]
#### Amazon API Gateway
A set of REST resources supported by HTTP methods.
Configure the API gateway to  route each method-resource pair to a backend service.
![[week07_aws_api_gateway.png]]
#### Kong
An open-source package that is installed and managed by yourself (Docker).
This includes built-in support for many key edge functions
![[weeko7_kong.png]]
#### Self-Developed
- This is a feasible option
- Key _design problems_ to solve:
	- Mechanism for defining routing rules (minimise coding)
	- Correctly implementing HTTP proxying, including handling headers
- Build on top of existing web frameworks (e.g. nginx, Netflix Zuul, Spring Cloud Gateway)
#### Graph-based API tech
- Key challenges in API design:
	- A simple retrieval might need data from multiple services
	- Different clients may need slightly different data
- These frameworks give clients control over the data returned
- Facebook/Meta's GraphQL standard
	- Models server-side data as "graph" of objects that can be queried
	- ![[week07_graphql.png]]
- Netflix's Falcor
	- Models server-side data as virtual JSON object graph
