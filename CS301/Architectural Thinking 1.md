# How is Architecture defined?
>"The fundamental organisation of a system embodied in its components, their relationships to each other and to the environment and the principles guiding its design and evolution."

-IEEE Std. 1471 definition

![[week01_ieee_42010.png]]

# Architecture Requirements
- ## Functional Requirements
	E.g. "1 click checkout", "Search for all classes student is allowed to take"
- ## Quality Attributes
	E.g. "Serve 100 users", "99.5% availability"
	![[week01_quality_attributes.png]]
- ## Constraints
	E.g. "Must be built on WebSphere technology", "Have to be at least three-tiered"

# ISO 25010 Quality Attributes
- Specific concern about system behaviour (non-functional requirements)
- Typically addressed by one or more views per quality attribute
![[week01_iso_25010.png]]

# Architectural Significant Requirements
1. During design, you will not be able to prototype or validate all features
2. An architecturally significant requiement is any requirement that strongly influences our choice or structures for the architecture.
	a. Influential Functional Requirements - Features that require special attention in the architecture. (used 80% of the time and require end to end architecture components)
	b. Quality Attributes - Externally visible properties that characterise how the system operates in a specific context (ISO25010)
	c. Constraints - Unchangeable design decisions, usually given, sometimes chosen
	d. Other Influencers - Time, knowledge, experience, skills, etc...

# View Diagrams
We will be using 2 main diagrams. Namely network and sequence diagrams. They will be used for communication and analysis.

## Sequence Diagram
![[week01_sequence_diagram_1.png]]