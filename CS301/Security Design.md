# Security Concepts
Web (Injection, HTTP Parameter Tampering, etc...) and network security (Man in the Middle, HTTPS Downgrade)
The attack surface of the software environment is the sum of the different points where an attacker can attempt to enter or extract data from said environment
# Risk Management Concepts
- ## Threats
	- Any potential danger to information or system
	- ![[week03_sql_injection.png]]
		- We can attempt to mitigate this SQL Injection with validation and prepared statements
	- ![[week03_xsrf.png]]
	- ![[week03_mitm.png]]
		- Easily done through HTTP only pages (data sent to and fro client and server is not encrypted)
	- ![[week03_http_parameter_tampering.png]]
	- ![[week03_ssl_strip.png]]
- ## Vulnerability
	- A weakness in the system
- ## Asset
	- Valuables to the company
- ## Control
	- Safeguards to prevent or minimise losses (countermeasures)
- ## Risk
	- Probability of a threat exploiting any vulnerability
# Cryptography and Hashing
## Symmetric Key
This uses a single key. This is faster for encryption and decryption but has bad availability.
## Asymmetric Keys
Uses 2 keys. This is slower because of 2 keys to either encrypt or decrypt the data but has better availability because you can now hand out a public key
## Hashing
A function that maps data to data of a fixed size (Passwords)
# Firewall
## Types
- Host based
	- Filter in/outgoing traffic to a specific host
- Network based
	- Filter in/outgoing traffic from a less secure to more secure zone
## Filtering
- Stateless Packet Filtering
	- Allow/Deny action as per the source and destination of the port and address
	- Last rule to deny all by default
	- ![[week03_stateless_firewall.png]]
- Stateful Packet Filtering
	- Keeps track of client-server sessions
	- Checks each packet validly belongs to one
	- ![[week03_stateful_firewall.png]]
- Application Level Firewalls
	- Works at app level
	- Separate proxy for each service
	- AWS Web Application Firewall rules to manage HTTP(S) web request based on criteria
	- ![[week03_application_level_firewall.png]]
# AWS Architecture Security
Consists of
- AWS Regions, Virtual Private Cloud(VPC), Availability Zones and Subnets
- AWS Access Control Lists (ACL)
- AWS Security Groups (SG)
- AWS Identity Access Management (IAM)
Refer to slides for details

