# Blocking / Synchronous Operation
If you wait for a operation to complete -> synchronous / blocking
- If data is needed to be processed, then we cant make it asynchronous


# Non-Blocking / Asynchronous Operations
Not Waiting for an operation
- Fire and forget, handled using call-back
- Usually I-O operations
- Two Ways
	- Rest Template : Synchronous
	- Web client : Synchronous or asynchronous
- Tomcat has threads for handling requests and answering requests
- NIO threads for each request coming to the server
- Totally how many threads : 10 by default
- Latency is also the time the request is in queue
- server.tomcat.threads.max=1
- throughput -> ability to churn through
- Only 1 acceptor and poller, but exec threads are what we have 1 or 10 of.
- Tomcat Thread calls another background thread, which does the work

## Head of the line Problem
Till first response not given, then others are blocked till first not finished

![[Pasted image 20260118123013.png]]
as soon as webflux returned, http-nio is freed

# Asynchronous Programming
- It can never be a return type of object.
- Have to autowire webclient. Has a builder function for which we have to build. It also needs tio be made a bean so that we can autowire
	- Promise : I will return the result in the future
		- Mono - Wrapped with mono for return type 
			- Have to add webflux dependency
			- Reactor-nio threads handle these things.
			- To make blocking, just add block() at the end 
		- Flux


Cant use pagination as that works for one endpoint, not when you have multiple endpoints as in the case of zomato.

ZeroDha - Get fast rendered result
Zomato to render all results and then return

unless callback defined, we arent calling the api.
- .zip() -> makes sure success called only when all composing monos are successfull.
- .first() -> if you want to return the first one result we get

![[Pasted image 20260118130423.png]]

## Chaining
Begining of operation n depends on completion of operation n-1

- Synchronous Chaining : All operations happen on server threads (http-nio)
- Asynchronous Chaining : 
	- We can put the chained commmands in onSuccess on each call where last merges all results to send.
	- flatMap : for flatmapping the result or else we get mono of mono of mon depending on which position in the chain it comes


## Flux
Streaming : 
- Bi-Directional Streaming : The server can start sending without client requesting
	- WebSockets are examples
- Uni-Directional Streaming : Client wants something continuously and server keeps giving
	- Achieved using flux
- Cant send JSON, sends stream

Read Bi-directional
WEB-RTC
JRPC 
HTTP 2.0