# Arcjet Protocols for Decentralization
A full-featured platform for deployments of full-stack applications with decentralized network infrastructure that allows app developers to pay users to serve content instead of cloud providers

## Introduction and Rationale
An Introduction can be found here: 
[Arcjet - A Decentralized Application Server Platform — Steemit](https://steemit.com/apps/@cryptoquick/arcjet-a-decentralized-application-server-platform)

## Goals
* Decentralize Application Server Hosting
* Full-featured, offering secured and decentralized versions of:
	* Decentralized Data Services
	* Proxies for HTTPS, HTTP/2, WS, streaming protocols
	* & more
* Easy-to-use App Directory, App Dashboard (for app owners), and Apps

## Concepts
Requests to the network should be made with Arcjet clients that maintain a clientside DHT for hosts for that hostname, otherwise they are proxied through HA servers, which are more expensive. They can either run in fast mode, or secure mode. Secure mode verifies responses against those of other servers. Fast mode uses the first response.

## Roadmap
- [ ] Make Desktop Client App
	- [ ] Can install apps and services with docker containers
	- [ ] Can proxy requests to containers
	- [ ] Configurable proxy client rate limiting
		- [ ] Default 1 request per IP per second
	- [ ] Wallet with Network Coins and Application Tokens
	- [ ] Add AJC Miner Docker Image App
	- [ ] Decentralized Data Services
		- [ ] Services and their potential implementations
		- [ ] Object Store - weedfs
		- [ ] Document Store - nedb
		- [ ] K/V Store - levelup
		- [ ] Rotating Offline Backups
		- [ ] Data Viewers for each service
		- [ ] Data may be encrypted at rest
	- [ ] Resource allocation configuration (Defaults to 50% available)
		- [ ] Sliders for:
			- [ ] CPU
			- [ ] Disk Storage
			- [ ] Memory Allocation
			- [ ] Monthly Data Transfer
			- [ ] Bandwidth
		- [ ] CPU, Storage, Memory, and Data paid at different rates, combined to an estimated monthly payment as determined by rate measuring
	- [ ] List as HA Server
		- [ ] Increases payments but lists your server publicly with your IP with the expectation you will maintain high end server hardware with backup power supply and a business-tier ISP and that application developers will point to your server with their DNS to proxy initial requests to desktop clients running their application.
		- [ ] HA Servers maintain a DHT of applications and desktop clients that can respond to requests for those applications.
- [ ] Client Server Library
	- [ ] Initiallly Node.js and Go, others to come
	- [ ] Request
		- [ ] To make requests to other services within the network
	- [ ] Router
		- [ ] Application Secret Provider
		- [ ] Servers often have secrets that need to be configured in order to work. Must be on an HA server owned or trusted by application developer
		- [ ] Secrets cannot be distributed with container
	- [ ] Server Software Update Management
	- [ ] Backups
	- [ ] Decentralized Data Services Accessor Methods
- [ ] Client Frontend Library
	- [ ] JavaScript
	- [ ] Fetch - Fetch against Arcjet hostnames and routes. DHT with data owners and all servers running this specific app. DHT is kept up-to-date in client. Fetches against three sources. Hashes all source data to validate against other sources. Removes source from DHT if returns incorrect response.
	- [ ] Router to determine data ownership and source priority. If online, content owner receives priority for serving content.
- [ ] Arcjet Stack Docker Container
- [ ] Make Social Network App
	- [ ] Can announce new apps
- [ ] Make Marketplace App
	- [ ] Can install apps and purchase service using AJC equivalent to USD
		- [ ] In USD due to AWS fees being measured in USD, so is the best comparison
- [ ] App Clones
	- [ ] Medium Clone
	- [ ] Slack Clone
	- [ ] YouTube Clone
	- [ ] Messaging Client
	- [ ] Twitch Clone
- [ ] Service Clones
	- [ ] Identity and OAuth
	- [ ] Maps
	- [ ] Advertising
	- [ ] Analytics
	- [ ] Video Streaming
	- [ ] Object Storage
	- [ ] Datastore
	- [ ] Image Processing
	- [ ] Logging
	- [ ] Messaging
	- [ ] Inbound and Outbound Email
	- [ ] Certificates and App Secrets Providers
	- [ ] Billing and Payments
- [ ] Blacklists (and list payment / work reductions)
	- [ ] Must be opted in, and blacklists are maintained by independent users
	- [ ] Political/Controversial Content
	- [ ] Adult/Pornographic Content
	- [ ] User-Generated Content
	- [ ] Encrypted Content
	- [ ] Network Abuse (Spammers)

## Economics
* Requests are prioritized to data owners
* Data ownership is determined by route
* At least three requests are sent, 10% sent to verifiers and 80% to server with first response
* HA responses are worth up to 50% of the AWS rate. They are the most expensive.
* Arjcet Desktop App responses are worth up to 10% of the AWS rate.
* Market is normalized against AWS rates, but response rates can vary with the market against network supply and demand. This is to encourage people to install apps that pay more per month.

An HA (High Availaibility) server is determined by nines in the past year since the start of the network. Uptime is listed in a directory of app developers.

AJC is the coin used to validate transactions (payments for processing responses, CPU, storage, data, etc.).
All clients have the option to mine AJC.
All clients must run independent copies of the blockchain in order to maintain network diversity

Applications are pre-funded. Apps that run out of funds forward proxy to the donation screen

## Challenges
* Preventing cheating (such as, running a process to run up application requests for own content, charging app devs)
	* Rate limiting, daily payout caps, identification of bad actors and their software, possibly with application-chosen user IP blacklists
* Load balancing and incentivization across the network
* Security
* Avoiding single points of failure
* Being full-featured
* Identification and announcing behavior of bad actors
	* Users must voluntarily stop serving apps that exhibit bad behavior
	* Users can also subscribe to trusted app blacklists
* Market balance

## Contributing
Contact: [cryptoquick (Hunter Trujillo) · GitHub](https://github.com/cryptoquick)
Feel free to leave an issue!
[Join our Slack!](https://join.slack.com/t/arcjetspace/shared_invite/enQtMjc3OTIyMTEwOTk3LWZmZDFkZGJiNmQxY2Q2ODJiNGJlMDEzMzY0NzJlMjQ1YzMzNTVkNjI0NTE5OTM2OGU4OTg4NGZhNGE5NjFkODg)
[Trello for our initial Proof of Concept](https://trello.com/b/eg12Zgb1/arcjet-proof-of-concept)
