# Testing Microservices
## Traditional Way
![[week04_microservice_testing_01.png]]
![[week04_microservice_testing_02.png]]
![[week04_microservice_testing_03.png]]
- Return on investment is difficult to show
- Hard to "prove" the investment leads to fewer defects
- Smaller companies are less likely to have experienced "unmaintainable" systems
- Tests seen as slowing down delivery cycle
# Testing & Analysis Pyramid
![[week04_pyramid.png]]
We now want to use an example to showcase how this pyramid is used
![[week04_example_01.png]]
## Automated Code Analysis
### Static Analysis
Check properties of the source code without executing it
![[week04_static_analysis.png]]
#### Halting Problem
![[week04_halting_problem.png]]
### In Practice
- Enforces coding standards and minimises smelly code (e.g. flake8, pylint)
- Find resource leaks (Memleaks)
- Common security vulnerabilities (Pass user input to JS innerHTML method)
- Deep analyses might be expensive if done for every commit
### For Microservices
![[week04_code_analysis_microservice.png]]
## Unit Testing
- Whitebox tests written by developers
- Verify the smallest _"units"_ of code (methods, classes)
### FIRST Principles
Fast | Isolated | Repeatable | Self-Validating | Timely
### For Microservices
![[week04_unit_testing_microservices.png]]
## Integration Testing
Do separately modules work together as expected?
We will commonly see
- Inbound adapters
	- REST HTTP Client
	- Messaging Subscriber Code
- Outbound Adapters
	- HTTP Proxy
	- O/R mapping (e.g. SQLAlchemy)
	- Messaging Publisher code
### For Microservices
![[week04_integration_microservices.png]]
- Services often call external infrastructure (DBs) or other services
- Integration tests verify that they work together correctly
- External infrastructure - "test doubles" (in-memory db) or real database (staging db)
- Other Services - Use test stubs with canned answers (e.g. WireMock)
![[week04_integration_docker.png]]
## Component Testing
Tests a service in isolation as a black box (process is external to the service)
![[week04_component_testing.png]]
There are minimalist (health check) and full fledged acceptance tests (I/O behaviour)
### For Microservices
![[week04_component_testing_microservices.png]]