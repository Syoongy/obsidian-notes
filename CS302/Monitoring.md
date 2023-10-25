# Why do we need it?
Identify the cause of crashes. Figure out what potential bottlenecks are.
# Outages - Traditional Siloed Approach
![[wk11_monitoring_01.png]]
## Culture of Causality
A Disciplined approach to solving problems using production _telemetry_ to understand contributing factors
- Microsoft Ops Framework study - Organisations with the highest service levels rebooted their servers twenty times less frequently; five times fewer "blue screens of death"
- Best-performing organisations were better at diagnosing and fixing service incidents
# Telemetry
The automated process of collecting/transmitting measurements and data from remote points to monitoring systems
![[wk11_telemetry_01.png]]
Telemetry is essentially taking in information from all sources to use
## In software Systems
### Key Steps
1) Instrument software systems
2) Collect metrics from them
3) Monitor them through alerts and visualisations
### Etsy
By 2011, tracking > 200k production metrics at every layer of their application stack; monitored in _Graphite_ during deployments
## Challenges in implementing
- Number of components to analyse
- Maintenance
- Quantity of metrics
- Avoiding silos of information
### Silos of information
![[wk11_silos_01.png]]
## Centralised Infrastructure
Used to understand the system as a whole and paves the way to proactive alerting
- "The Art of Monitoring" describes a monitoring architecture used by Google, Amazon, etc...
	- Collect events/metrics about business logic, app, and environment layers
	- Centralise the handling of this data
	- Event router stores, visualises and alerts
## What kind of data can we collect?
- Work metrics - throughput, success, error, performance
- Resource metrics - utilisation, saturation, availability
- Events - Code Changes, alerts, Scaling events
- CI/CD pipeline - Build/Test length, pass/fail events
## Creating Production Telemetry
- Centralised telemetry infrastructure is only as good as its data
	- ensure apps are creating sufficient telemtry
- Dev and Ops create production telemetry as part of their work
- Every feature should be instrumented
	- "If it was important to enough to implement, it's important enough to monitor"
	- Logging libraries make it easier
- Members of the value stream will use telemetry in different ways
### Logging Levels
![[wk11_logging_01.png]]
### Enabling Fast Feedback
![[wk11_feedback_01.png]]
## Scientific Method
- What evidence do we have that a problem is occurring?
- What are the relevant event/changes that could have contributed?
- Which hypotheses can we formulate to confirm the cause and effect?
- How can we prove the hypothesis is correct and issue a fix?
### Self-Service Metrics
- Telemetry must be easy to access so that we can achieve
	- Fast, visible, sufficiently centralised
	- "Shared view of reality"
- "Information radiators"
	- Nothing to hide from visitors
	- Nothing to hide from itself
- Centralised servers
	- e.g. Graphite, Prometheus
	- No privileged access required
### Analysing Data - Time Series
- Events and metrics are often stored as time series data
	- data points indexed in time order
- Can be used to perform statistical operations
- E.g. Segmentation faults
	- Treat as individual events
	- Analyse occurences over time to find outliers/variances
	- notify if rate increases
### Means and Standard Deviations
- Simplest statistical technique
- e.g. Notify if queries are slower than average
- Could lead to false positives
### Non-Gaussian Data
Many telemetry data sets for not have normal distributions
![[wk11_telemetry_data_01.png]]
# Netflix
![[wk11_netflix_01.png]]
# Prometheus
Centralised telemetry software that records real-time metrics in a time series database. It is based on an HTTP pull model (Configure services to publish metrics and Prometheus to find the endpoints).
- Flexible alert and query systems
- Deployed with Grafana to visualise data in dashboards
## With Kubernetes Cluster
![[wk11_prometheus_01.png]]
## PromQL
Query language that lets users select and aggregate time series data in real-time
- Expression data types - instant, range vector; Scalar
	- http_requests_total
	- http_requests_total{status!~"4.."}
	- rate(http_requests_total[5m])[30m:]
## Alerting Rules
Used to specify conditions (alert states) in the monitored system that you wish to be notified about. Can be configured to periodically share information about alert states with "Alertmanager", which dispatches notifications
![[wk11_prometheus_02.png]]
## Custom Metrics
![[wk11_prometheus_03.png]]