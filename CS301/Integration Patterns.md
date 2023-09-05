# Interface Integration
This covers screen/web scraping with input data and data extraction. This can be used in both intranet and internet environments.
![[week04_interface_integration_01.png]]
Some examples are UiPath, IBM Host Access Transformation Server, BeautifulSoup, AWS Glue
# File Transfer
This is one of the most common integration methods and has batch mode for files greater than 100MB.
Format protocol, frequency, who transforms data and file server architecture must all be decided.
![[week04_file_transfer_01.png]]
Some examples are FTP, SFTP, IBM Managed File Transfer (MFT), AWS Transfer Family
# Database Integration
We first need to consider batch or Record/Transaction modes. SQL and NoSQL databases also need to be decided.
## SQL
- Relational schema
- Structured data
- ACID transactions
- Designed for vertical scaling
Oracle DB, MySQL, AWS RDS
## NoSQL
- Key-value, document, graph, etc...
- Unstructured Data
- Horizontal Scaling
- Eventual Consistency
MongoDB, AWS DynamoDB
## Replication
This operation can be synchronous or asynchronous. This can have one or two way replication and ensure that states on the replicating databases are in sync at start
![[week04_db_integration_replication_01.png]]
# Messaging
- Pub/Sub model based
- Record/Transaction data
- Synchronous or asynchronous communication
- Can be either centralised/decentralised
File format, selectivity, persistence, durability and exception handling need to be defined along with the application model and communication
![[week04_messaging_01.png]]
Examples include WebSphereMQ, MicrosoftMQ, RabbitMQ, AWS SQS/SNS/MQ
## Messaging Concepts
### Channels
Data is transmitted through a message channel which is a virtual pip that connects sender to receiver
![[week04_messaging_channels.png]]
#### Point to Point
Ensures only one receiver will receive a specific message
![[week04_messaging_ptp.png]]
#### Pub/Sub
Sends message to all subscribed receivers
![[week04_messaging_pubsub.png]]
#### Datatype
Ensures that all data of a specific type is sent to a channel of that type
![[week04_messaging_datatype_channel.png]]
#### Dead Letter Queue
A channel for undelivered messages
![[week04_messaging_dlq.png]]
#### Guaranteed Delivery
Messages are not lost even if the messaging system crashes (Save to disk)
![[week04_messaging_gd.png]]
#### Message Bus
A middleware between applications that enables them to work together through messaging
![[week04_messaging_bus.png]]
### Messages
Atomic packet of data that can be transmitted on a channel
#### Request Reply
Any message sent must receive a reply to confirm the message has been received
![[week04_messaging_reqreply.png]]
#### Return Address
Request message should have a return address to send the reply message to
![[week04_messaging_return_address.png]]
#### Correlation Identifier
A unique identifier to indicate which request message this reply is for
![[week04_messaging_identifier.png]]
### Routing
Sender will send a message to the message router and the application component will determine how to navigate the channel topology and direct the message to the final receiver or next router
#### Message Broker
Hub and spoke architectural style
![[week04_messaging_broker.png]]
#### Process Manager
Maintains the state of the sequence and determine the next processing step based on intermediate results
![[week04_messaging_manager.png]]
#### Content-based Router
Routes message based on content
![[week04_messaging_content_router_01.png]]
#### Splitter & Aggregator
![[week04_messaging_splitter_aggregator.png]]
### Transformation
Reconcile different data formats from various applications through a message translator
#### Canonical Data Model
Independent from any application and requires each application to produce and consume messages in a common format
![[week04_messaging_canonical_data_model.png]]
### Endpoints
A layer of code that knows how the application and messaging system works and bridges the two to work together. The bridge code is a set of coordinated message endpoints that enables the application to send and receive messages.
#### Polling Consumer
Makes a call to receive a message when it wants to
![[week04_messaging_polling.png]]
#### Event Driven
Handles messages as they are delivered onto the channel
![[week04_messaging_event_driven.png]]
#### Selective Consumer
Filters messages delivered to only accept those that match its criteria
![[week04_messaging_selective.png]]
#### Durable Subscriber
Save messages that are published if the messaging system goes down
![[week04_messaging_durable.png]]
# Application Programming Interfaces (API)
This is for Record/Transaction level data transfer and synchronous communication.
This requires a function with its input/output parameters and exception handling to be defined and exposed through SOAP or RESTFUL.
Examples include Java EJB, .NET remoting, SpringBoot, AWS Lambda
## SOAP Architecture
![[week04_api_soap.png]]
## REST
![[week04_api_rest.png]]
## Comparisons
![[week04_api_comparisons.png]]
# Architectures
## Web (AWS)
![[week04_web_arch.png]]
## Web and Mobile
![[week04_arch_web_mobile.png]]
## Traditional Web
![[week04_arch_traditional_web.png]]
## Modern (Client Centric) Web
![[week04_arch_modern_client.png]]
## Microservices API Gateway
![[week04_arch_microservice_01.png]]
![[week04_microservices_02.png]]