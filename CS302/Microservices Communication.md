# Terminology
![[week06_terminology_01.png]]
![[week06_terminology_02.png]]
![[week06_terminology_03.png]]
# Styles
How _many entities_ are you communicating with?
- **One-to-one** - One sender, one receiver
- **One-to-many** - One sender, any number of receivers
When do you need a _response_?
- **Synchronous** - Sender expects timely response; blocks
- **Asynchronous** - Response (if there is one) may not come immediately; no blocking
![[week06_style_01.png]]
# Asynchronous Architecture
Implemented using _message-oriented middleware (MOM)_
![[week06_async_arch.png]]
## Publish-Subscribe Pattern
![[week06_pub_sub_01.png]]
![[week06_pub_sub_02.png]]
Publishers are not privy to what happens to the message it publishes. It is the job of the receivers to process the message.
![[week06_pub_sub_03.png]]
Subscribers also do not care where the messages come from.
# Advanced Message Queuing Protocol
also known as _AMQP_.
- This is an open standard protocol for MOM
	- Defines a message format for standard and extensible representation of data
	- _Interoperability_ among different AMQP-compliant sender/receivers
- **RabbitMQ** is an implementation of an AMQP broker
- pika is a Python implementation of the AMQP protocol
## Message Structure
![[week06_amqp_struct.png]]
![[week06_amqp_struct_example.png]]
## RabbitMQ
Message broker that supports the AMQP protocol.
Routes messages to FIFO queues via an exchange and key matching
![[week06_rabbitmq_01.png]]
### Exchange Types
- A message is publised to an exchange, but consumed from a queue
- Exchanges are bound to queues with a routing key
- An exhcnage routes a new message to a bound queue according to the message's routing key and the exchange type:
	- Fanout - Routes messages to all bound queues (regardless of key)
	- Direct - Routes messages via bindings with the same routing key
	- Topic - Routes messages vie wildcard matches on bindings
		- * matches one word; # matches 0 or more words
![[week06_rabbitmq_exchange_types_01.png]]
### pika
_pika_ provides library code for declaring exchanges/ queues / bindings
![[week06_pika_01.png]]
It is also used for publishing / consuming messages
![[week06_pika_02.png]]
![[week06_rabbitmq_02.png]]
## Process Patterns
### Notation - Implicit Broker
![[week06_process_notation_implicit.png]]
### Notation - Explicit Broker
![[week06_process_notation_explicit.png]]
### Orchestration
![[week06_process_orchestration.png]]
A composite service orchestrates the process flow
This is achieved using synchronous request/ reply communication
![[week06_process_orchestration_02.png]]
![[week06_process_orchestration_03.png]]
The example above is fine as it has no impact on the outcome of the request
### Choreography
![[week06_process_choreography_01.png]]
There is no controller. Instead, services publish events (messages) when there is a state change, and services subscribe to those events.
This is achieved using asynchronous message-based communication
![[week06_process_choreography_02.png]]
### Choreography with a Process Engine
![[week06_process_choreography_engine_01.png]]
![[week06_process_choreography_engine_02.png]]
The process engine ensures the execution of steps by publishing and subscribing to events.
Combines the asynchronicity of choreography and process visibility of orchestration.
An example tool is Conductor by Netflix
### Saga
If we have a database-per-service => no ACID transaction for **whole** process
(e.g. one service fails in part of the process, we are unable to undo our previous steps)
Saga aims to solve this by doing the following:
- A sequence of local transactions such that...
- if a step fails, _compensating_ transactions are executed to "undo" previous local transactions
- Facilitates "all or nothing" semantics across multiple services
This however can be challenging to implement as there is no isolation property
- Concurrent processes
- Lose updates, dirty reads (Data is accessed in the middle of a rollback)
#### In Orchestration
![[week06_saga_01.png]]
#### In Choreography
![[week06_saga_02.png]]