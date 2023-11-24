
# What is DevOps?
Is it a role, or a culture? (or both?)
![[week02_role_culture.png]]
Possibly, if everyone else also buys into the "culture" aspect of DevOps. This however could also create a new silo of just the DevOps which could be harmful.
## DevOps Engineers
Is it just a buzzword? Not many people know what it actually means. The role itself can vary and more often than not may lean to one side of dev or ops more.
### As a role
A DevOps engineer is an IT generalist:
- Some knowledge on DevOps workflows
- Managing of DevOps toolchains
- Automation expert
- Inter-personal skill to work across silos
Some organisations hire DevOps evangelists to implement process/cultural improvements

![[week02_cultural_movement.png]]
Although DevOps roles are often characterised in terms of tool, DevOps is a cultural movement
### Site Reliability Engineering
Originated from google with a goal of creating scalable and highly reliable software systems through applying aspects of SE to infrastructure/ops problems.
This however should be considered as a specific implementation ("how") of DevOps ("what").
![[week02_devops_sre_diff.png]]
![[week02_sre_practices.png]]
![[week02_sre_practices_2.png]]

To summarise, DevOps is a culture and mindset which can also be a role

# DevOps Skillset Roadmap
![[week02_skillset_roadmap.png]]
## Development (Git)
### Developer Workflows
Understand the organisation's developer workflow. We want to figure out how the applications are configured and tested along with their git workflow
![[week02_workflow_1.png]]
- Loose coupling ensures a reduction of "blockers" between different services. This improves flow through independence.
- Standardisations of testing frameworks, code standards and peer reviews ensure code readability to all engineers
- Shared source codes promote learning of concepts or techniques across projects or services
### Developer anti-patterns
- #### Developer Culture
	- Design by committee/Group think (Not the best idea but just go along to remove the blocker)
	- Cargo culting (Following FotM)
- #### Coding
	- God objects (In object-oriented programming, a god object is an object that references a large number of distinct types, has too many unrelated or uncategorised methods, or some combination of both)
	- Overengineering (Not everything needs to be a microservice)
	- Spaghetti code (Hacks to get things working etc)
	- Copypasta (ChatGPT)
- #### Tools
	- Law of the hammer (Using same tools for every problem)
	- Bleeding edge (Using the latest and greatest)
	- Vendor lock-in (Don't use onl)
### Git Branching
![[week02_git_branching.png]]
#### Branching Strategy
![[week02_branching_strategy.png]]

In 2015's State of DevOps Report, trunk-based development lead to higher throughput, better stability and less burnout

## Development OS
- Automate as much as possible
- Learn shell scripting
- Basics of security, load blancing, HTTP, networking
- Collaborate not replace the experts (sysadmins, network engineer, security engineers)
## Development Docker
#### Containerisation
Packages your application with just the OS libraries and dependencies required to run. This ensures a consistency on any infrastructure via OS-level virtualisation
## Development CI/CD
This is the heart and soul of DevOps. DevOps engineers design fully automated pipelines of CI/CD "jobs"
![[week02_ci_cd.png]]
### Andon Cord Pull
Comes from car production factories. A cord is pulled to alert the whole factory and everything stops to deal with the situation (swarming).
This is akin to part of the pipeline failing. We want to notify the whole team and get the issue fixed. This also enables the whole team to learn and make it less likely to happen again.
## Development IaaS
Agiility provided by cloud computing complements DevOps.  You can spin up servers, VMs, storage, backups and networks.
## Development Container Orchestration
- Docker and Docker Compose might suffice for local testing
- Distributed multi-container apps in production are complex and can consist of 100s or 1000s of containers
- Container orchestrators (K8, AWS ECS) help automate their deployment, management, networking, scaling, and repair
## Development Monitoring
Real time monitoring tools are required to find problems in production. Prometheus + Grafana
## Development Infrastructure as Code
Defines virtualised infrastructure in machine-readable files. This makes it easier to replicate environments. (E.g. Ansible and Terraform)
# Architecture for DevOps
## Microservices
- Logically represents a business capability
- Black box with a well developed interface (REST)
- Independently developed and deployed
![[week02_microservices.png]]