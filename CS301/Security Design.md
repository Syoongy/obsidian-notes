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
