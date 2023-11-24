- Software requirements rarely "frozen" before development
- Software is subject to (frequent) change
- Software and WIP are "invisible"
- Maintenance & technical debt are major challenges

# Waterfall
The main idea of this method is to break software development into linear, sequential phases
![[week_01_waterfall.png]]
# Agile Manifesto
![[week01_agile.png]]
![[week01_agile_principles.png]]
# Lean Software
- Translation of lean manufacturing principles (Toyota Production System) to software development
- The main focus is to eliminate waste during the project process
- This resulted in Kanban to visualise work in progress

Through Agile and Lean, we managed to shift away from the linearity of waterfall. However, teams still worked in their own silos. This results in a blame culture where different teams meet only their own KPIs.

# Deployment Hell
A typical scenario would have a large complex organisation, coupled monoliths, scarce integration testing and many approval processes

This is an example of what a deployment lead time of three months can look like
![[week01_deployment_hell.png]]

After merging all the changes, the monolith no longer builds
- Heroics and multiple investigations required
- Who broke it? How can it be fixed? Delays for the customer? \$\$s?

# So what is DevOps?
Practices that combine development and IT operations with a goal to shorten software delivery life cycle, providing continuous delivery with high quality software

## Solving a People Issue
- Takes into account everyone involved with software delivery (Devs, Ops, Security, QA, ...)
- Embrace a culture of collaboration, ownership and learning with purpose
- Developers no more important than other types of engineers
	- Empathy and understanding between teams
	- Without Ops, no value released to customer
	- Without Devs, no new features to meet changing business requirements

## Principles
### CALMS Framework - Jez Humble
- Culture - Collaborative and customer-centred
- Automation - Automated integration testing, deployment and infrastructure as code (CI/CD pipelines)
- Lean - Agile, scrappy lean teams (minimise WIP)
- Measurement - Measure data to celebrate "wins"
- Sharing - Devs and Ops should feel empowered to teach and learn from each other; empathise with their (conflicting!) incentives

### Three Ways - Gene Kim
- Idea: Devlops practices can be narrowed down into three principles
	1) Flow
		- Value stream from the business to customer. This can come in the order of Business -> Devs -> Ops -> Customer
		- Anything that increases this flow from left to right comes under this
		- Practices that improve the flow / remove blockages
		- E.g. smaller batches of work can result in a faster flow
		- To promote flow, we should make work visible
			- The technology value stream is invisible (Cannot easily see where flow is impeded and where work can easily be bounced around with incomplete info)
			- Take explicit steps to visualise how work is flowing (E.g. Kanban or Sprint Planning Boards)
		- Limit work in progress
			- Daily work can become dominated by "urgent requests"
				- Phone calls, emails, Slack, issue tickets
				- WIP gets stuck as WIP for longer - costly
				- Superstar engineers can become the bottleneck
			- These disruptions are less visible than in manufacturing
			- Use a ticketing system so that everyone knows how much work the individual has
			- Set a WIP limit for each individual
		- Reduce batch sized & handoffs
			- Handing off technology artefacts to the next team is "easy" but requires substantial communication to do properly and knowledge might be lost in the process
		- Continually identify & elevate constraints
			- Constrains - Environment creation, code deployment, test setup, overly tight architecture, "superstar engineers", ...
		- Eliminate waste in the value stream
			- "Waste" is any material/resource beyong what the customer requires and is willing to pay for
			- E.g. extra features, task switching, waiting, defects, manual work
	2) Feedback
		- Business -> Devs -> Ops -> Customer
		- This goes from right to left
		- Ensures that feedback goes back to the previous items as fast as possible
		- If anything goes wrong at the Ops level, the Devs should also be included
		- Working within complex systems
			- Especially important in complex systems
			- Systems that are more complex than the sum of their parts
			- System level behaviours that cannot be explained only in terms of components
			- Accept that failure is inherent and inevitable
		- See problems as they occur
			- Lack of fast feedback leads to poor outcomes
			- Waterfall - develop for a year, no feedback until testing/release
			- We want fast feedback whenever work is performed at all stages
		- Swarm & solve problems to build new knowledge
			- Swarm/mobilise whoever is needed to fix it
			- Deliberately goes against conventional wisdom
			- We want to do this to build a knowledge base and develop empathy for the product
		- Keep pushing quality closer to the source
			- Adding more inspection / approval steps can increase the likelihood of future failures (People unfamiliar with the project might be now part of the this process)
			- Find / fix problems in engineer's area of control in the value stream
				- Push quality / safety to where the work is performed
				- Use peer reviews and automated QA / security tests
		- Enable optimising for downstream work centres
			- In lean manufacturing, our most important customer is the next step "downstream"
				- Idea - Have empathy for their problems in order to better identify the issues that prevent fast and smooth flow
			- In the technology value stream - this means designing for operations
			- How? Prioritise testability, configurability, architecture (etc.) as highly as user features
	3) Continual Learning
		- ![[Pasted image 20230816175029.png]]
		- Organisational learning and a safety culture
			- Unexpected outcomes are possible when working within a complex system
			- Learn from mistakes rather than blame
		- Improvement of daily work
			- Technical Debt - Implied cost of additional rework caused by choosing an easy (limited) solution now instead of using a better approach that would take longer
			- Improve daily work by reserving time to pay down technical debt
			- Schedule "kaizen blitzes" (periods where engineers self-organise; fix any problems they want to)
		- Make local discoveries to global improvements
			- Make blameless post-mortems searchable
			- Shared source code repositories
			- Convert individual expertise into shared artefacts
		- Resilience patterns in daily work
			- Conventional wisdom - prepare a buffer for disruptions
			- Netflix wisdom - Continually introduce tension to elevate performance
				- E.g. Chaos Monkey - Randomly kills processes and compute servers in production
				- "Chaos engineering"
		- Leaders reinforce a learning culture
			- Conventional wisdom - leadership is making all the right decisions
			- DevOps wisdom - Leadership is creating conditions that allow the team to discover greatness in their daily work
			- Help your direct reports to see, solve, and learn from problems in their daily work
- Hypothesis: All DevOps behaviours and patterns can be derived from "The Three Ways"
- Many DevOps practices are related to or logical continuations of lean and/or agile practices

