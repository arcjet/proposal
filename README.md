# Arcjet Whitepaper: Architecture for Decentralized Cloud Applications
*0.2.0 - 12/15/2017*

A full-featured platform for deployments of full-stack applications with decentralized network infrastructure that allows app developers to pay users to serve content instead of cloud providers through a cryptocurrency, `AJC`.

## Introduction and Rationale
An Introduction can be found here: 
[Arcjet - A Decentralized Application Server Platform — Steemit](https://steemit.com/apps/@cryptoquick/arcjet-a-decentralized-application-server-platform)

## Goals
* Decentralize Application Server Hosting
* Full-featured, offering secured and decentralized versions of:
	* Local networks
	* Proxies for HTTPS, HTTP/2, WS, streaming protocols, on IPv4 and IPv6
	* Distributed network object storage and document storage
	* & many more distributed services
* Easy-to-use App Directory, App Dashboard (for app owners), and Apps
* Provide a comprehensive platform for decentralized serverless backend applications

## Concepts
Requests to the network should be made with Arcjet clients that maintain a clientside DHT for hosts for the application hostname, otherwise they are proxied through HA servers, requests to which are more valuable. Responses are checked against each other in order to validate consistency and authenticity.

A note on decentralization vs. distributed nomenclature: While Arcjet might be in some technical aspects distributed, the goal is decentralization, as there will still be organizational ownership and maintenance of applications. A truly open and distributed network is not yet within the scope of this project, however, may one day be possible through technologies we develop.

### Frontend Load Balancer

*TODO*

### Arcjet Space Program
The Arcjet Space Program is a storage network using a distributed hash table (DHT) which acts as a directory for each shard's contents, the contents of which are keyed by their route.

The Arcjet Space Program expects failure. It is designed to maintain a list of servers that are online and capable of providing access to data within certain shards. 

Until a migration requires it, objects and documents are to be kept on 32,768 shards of similar size, each of which maintain a hash which indicates the state of consistency of the shard to any query that might be run on it. The hash is calculated from a hashing function that effectively buckets each shard depending on a few different factors, but primarily its host and route, which will hash to a shard, and a shard will perfom a lookup of the contents of the file or document, depending on the shard index. The shard index maintains a consistency hash, a short-retention consistency journal (in order to resolve any consistency discrepancies within the network depending upon timestamp, write count, and current consistency hash), and a table pointing to the file seek point and byte length. Each shard has a variable size, depending upon the hashes that point to it. All shards must be evenly replicated across the network, so there is also a variable replication factor that varies with the number of individual network operators. An effective replication factor is calculated by server uptime multiplied by shard replication count.

Any query run on the Space Program must return the shard hash, hash date, and write count (somewhat equivalent in effect to a "block height" in a blockchain, but instead for a hash table), in order to prevent inconsistent responses. Usually, at least five requests will be made per frontend transaction, either over HTTP or WS, and the request will be acknowledged by multiple witnesses on the network.

### Arcjet Nebulous Network

The Arcjet Nebulous Network is a network which connects Space Program operators, which implements a distributed pub/sub system and a DHT which points to various resources on the network.

Network resource types and their attributes include, but are not limited to:
	* Files (Object Storage)
		* replication factor
	* Media (all are streamed to some degree)
		* Images
		* Audio
		* Video
	* Records (Document Storage)
		* collection
		* .properties
		* map()/reduce()
	* Logs
		* events
	* Messages
		* events
	* Transactions
		* currency
		* value
		* account
		* items

## Roadmap
- [ ] Make Desktop Client App
	- [ ] Can install apps and services
	- [ ] Can proxy requests to bundles
	- [ ] Configurable proxy client rate limiting
		- [ ] Default 1 request per IP per second
	- [ ] Wallet with Network Coins and Application Tokens
	- [ ] Add `AJC` Miner App
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
		- [ ] Secrets cannot be distributed with bundle
	- [ ] Server Software Update Management
	- [ ] Backups
	- [ ] Decentralized Data Services Accessor Methods
- [ ] Client Frontend Library
	- [ ] JavaScript
	- [ ] Fetch - Fetch against Arcjet hostnames and routes. DHT with data owners and all servers running this specific app. DHT is kept up-to-date in client. Fetches against three sources. Hashes all source data to validate against other sources. Removes source from DHT if returns incorrect response.
	- [ ] Router to determine data ownership and source priority. If online, content owner receives priority for serving content.
- [ ] Make Social Network App
	- [ ] Can announce new apps
- [ ] Make Marketplace App
	- [ ] Can install apps and purchase service using `AJC` equivalent to USD
		- [ ] In USD due to AWS fees being measured in USD, so is the best comparison
- [ ] App Clones
	- [ ] Medium Clone
	- [ ] Slack Clone
	- [ ] YouTube Clone
	- [ ] Messaging Client
	- [ ] Twitch Clone
	- [ ] Tidal Clone
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
	- [ ] Various content types
	- [ ] Network Abuse (Spammers)

## Economics
* Requests are prioritized to data owners
* Data ownership is determined by route
* At least three requests are sent, 10% sent to verifiers and 80% to server with first response
* HA responses are worth up to 50% of the AWS rate. They are the most expensive.
* Arjcet Desktop App responses are worth up to 10% of the AWS rate.
* Market is normalized against AWS rates, but response rates can vary with the market against network supply and demand. This is to encourage people to install apps that pay more per month.

An HA (High Availaibility) server is determined by nines in the past year since the start of the network. Uptime is listed in a directory of app developers.

`AJC` is the coin used to validate transactions (payments for processing responses, CPU, storage, data, etc.).
All clients have the option to mine `AJC`.
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
* Contact: [cryptoquick (Hunter Trujillo) · GitHub](https://github.com/cryptoquick)
* Feel free to leave an issue!
* [Join our Slack!](https://join.slack.com/t/arcjetspace/shared_invite/enQtMjc3OTIyMTEwOTk3LWZmZDFkZGJiNmQxY2Q2ODJiNGJlMDEzMzY0NzJlMjQ1YzMzNTVkNjI0NTE5OTM2OGU4OTg4NGZhNGE5NjFkODg)
* [Trello for our initial Proof of Concept](https://trello.com/b/eg12Zgb1/arcjet-proof-of-concept)
