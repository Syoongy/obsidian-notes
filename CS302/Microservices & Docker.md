# Microservices
## Monolith First
Most projects often start as a monolith. But why do we choose monoliths?
They are often simple to develop and test, have code all in one place, easy to monitor and very fast inter app communications
We have an example of a monolithic application under "Food To Go PTE"
![[week03_monolith_example_01.png]]
Over time, we run into an anti-pattern called "Big Ball of Mud" where we have spaghetti code building up along with duct taped solutions. This leads to longer repair times and potential bugs.
The application often also becomes too large for any one developer to understand while the integration loop also gradually increases along with the size of the app.
When an application outgrows its monolithic architecture, we often want to refactor it into microservices.
## Microservices Architecture
An assembly of loosely-coupled, fine-grained _services_.
A _service_ provides functionality over a network and
- Logically represents a business capability
- Is a "black box" with a well defined interface (e.g. REST)
- Independently developed (different languages) and deployed
- Exclusive access to its own data
![[week03_microservice_service.png]]
![[week03_microservices_example_02.png]]
### As a DevOps Enabler
![[week03_microservices_enabler.png]]
This enables CI/CD for a per service basis. This reduces time to deployment and complexity of any CI/CD pipeline.
- #### Deployability
	- shorter edit-build-test-run cycles; independent CI/CD
- #### Reliability
	-   a fault in a (loosely coupled) service does not cause the entire application to fail
- #### Scalability
	- services can be independently scaled, taking full advantage of the elasticity of the cloud
- #### Modifiability
	- services communicate via well-defined interfaces, so their underlying implementations can be refactored without affecting other services
- #### Management
	- services can be ‘owned’ by smaller teams, facilitating self-organisation and agile methodologies
### Decomposing a Monolith
We can decompose the FTGO example into microservices
![[week03_ftgo_decomposed.png]]
However, a large microservices application can also end up in a similar state if we have too many microservices
### Service Granularity
No consensus on what the size of a microservice should be. However, we typically map to business capabilities with some rough _rule of thumb_ (e.g. Jeff Bezos' *two pizza rule*).
Teams shouldn't be too big and complex e.g. > 20 people for 1 microservice.
However, services can also be too fine-grained and result in more network calls to each service.
#### Communication Patterns
![[week03_comm_patterns.png]]
##### Choreography
![[week03_pattern_choreography.png]]
This pattern essentially continually passes the message all the way without waiting for a reply until it hits the *Notifications* service. This pattern is loosely coupled with each service processing only what they need to.
##### Orchestration
![[week03_pattern_orchestration.png]]
The _Place an Order_ service is a _composite_ that _orchestrates_ communications between _atomic_ services.
### Atomic Services
Provides functionality related to on capability (e.g. CRUD operations for _Orders_). It is self-contained and does not depend on any other service. This is the simplest and most reusable type of service
![[week03_atomic_services_01.png]]
### REST
![[week03_rest_recap.png]]
### Drawbacks
Thet are _not a silver bullet_ and can make things worse with poor testing or development culture.
Incorrectly decomposing an application can result in a distributed monolith.
Distributed systems are also complex especially in terms of data consistency.
Deploying features that span multiple services can be tricky.
## Docker
This is to containerise a service to ensure it runs everywhere consistently
![[week03_docker_containerisation.png]]
