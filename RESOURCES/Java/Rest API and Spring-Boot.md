
# Creating beans of classes having different values
For creating different beans of same type, make abstract and then make child classes become the components which become beans.
## What is the issue when Parent class object is trying to get autowired and child child class beans are available
Here the problem isn't there is no bean as programming to interface means it can hold child beans, but the issue is it gets confused which bean to inject.
Here as base class doesn't become bean it cant populate the bean we need to tell which bean to supply.
hence we use @Qualifier to tell which bean.
**Note : Qualifier cannot use string as extrapolated string to fetch value dynamically at runtime**
It isn't tight coupling as application properties can hold string for @Qualifier.
Also even the  implementing class should have same same @Qualifer annotation on top.

Things like users, etc are objects managed by user. Only constant things like controllers etc are beans.

Bean Scopes
- Singleton
- Prototype
- Request : Per Request
- Session : Per Session
- GlobalSession : Global One

@Primary to use a type of bean by default.

# SpringBoot
A less verbose version from Spring, Taking things as scales of what we want but auto configured. But it takes away control for achieving this.

Structure of Web Application
Controller(Rest API, manage request ) -> Service (Business Logic) -> Repo (Data Access) -> Entity (Data Model)

![[Pasted image 20251209182322.png]]


Hence for Controller, Service beans used by Controller , Service use beans of Repository
Data helps with Persistence.

## Working behind the scenes
User interacts with only API, but how does it work then? 
Dispatcher Servlet: Handles the request
Handler Mapping : Chooses which controller should the req go to
Handler Adapter : converts the req data to java understandable (Serialisation, De-serialisation)
All this provided by Spring boot but in spring we have to do all this.
Then Controller gets the req
Controller then interacts with service -> service to -> Repo -> Data Model(Entity)

Dispatcher, Handler Mapping, Handler Adapter -> Constitute of Embedded System


![[Pasted image 20251207130003.png]]

Two types of Packaging
JAR - provided by SpringBoot, Standalone application. Its Deployable. Has. server also
WAR : don't have embedded servers

## Spring Initialiser
Spring Initialiser
Group is package
What dependencies
- Spring Web

gradlew build -> builds gradle application

java -jar and path to jar to run.

	@RestController : annotation for restController, tells this is component
	@Service for service beans

# APIs
We use http as protocol to get something from server.For this we have standard that needs to followed

## REST (Representational state transfer)
Not a framework for a principle.
resources is Orders, Users etc. The http verb is used to show the action

Request Structure :
headers
body
Verb (method)

Response :
headers
status code 
body

Data represented using XML, JSON, HTML
JSONS take whitespace, and even this takes bandwidth etc.
Read about better Protobuf, AVRO etc

RPC etc better ways

### Key Principles
Stateless
Client Server Architecture
Uniform Interfaces
Resource Orientated

# Rest API Request Structure
![[Pasted image 20251207135510.png]]
to disambiguate between resource -> Application Context


# Additional Resources to read.
https://stackoverflow.com/questions/52409579/protocol-buffer-vs-json-when-to-choose-one-over-the-other

https://www.linkedin.com/blog/engineering/infrastructure/linkedin-integrates-protocol-buffers-with-rest-li-for-improved-m

https://github.com/toon-format/toon


