
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

Essential features
- AutoConfiguration
- Product Ready Defaults
- Embedded Server

![[Pasted image 20251209182322.png]]


Hence for Controller, Service beans used by Controller , Service use beans of Repository
Data helps with Persistence.

## Working behind the scenes
User interacts with only API, but how does it work then? 
- Dispatcher Servlet: Handles the request
- Handler Mapping : Chooses which controller should the req go to
- Handler Adapter : converts the req data to java understandable (Serialisation, De-serialisation)
All this provided by Spring boot but in spring we have to do all this.
- Then Controller gets the req
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

# Learner Management System with SpringBoot

## Database
Need to persist the info, hence database.
Ways to achieve this 
- write to file
- write to database
	- MySql
	- No Sql
- cloud - blob structure
- redis cache
When structured -> relational database -> MySql

Application to Database steps (Things needed to to talk to database)
- Connect to database via connection URL (JDBC) -> this is the protocol framework we are using, Its not an API. We don't use API to communicate wit database.
- Talk to database in language it understand 
	- ORM -> Object relational mapping -> Hibernate (Framework) -> Converts to bytes to write on disk
- DDL -> Data definition language (Exposing a contract to talk to the database) -> Spring DATA JPA (translate our thing to database, does the thing of making statement and executing it while we use abstraction like save(abstraction) to implement the whole thing of adding to DB )
- Way to do CRUD operations -> Spring Data
- Flow from 4 to 1

need to add 
- Spring Data JPA
- H2 Database
- MySql Driver
Also need to a driver to communicate to Database. Makes them compatible
H2 -> Memory
MySql -> Disk

Framework of frameworks -> Spring/SpringBoot

Now for making applications
-> controller
- In req, 
	- req body (JSON ->)
	- response body
- Response
	- Status code, reflection -> we get original information from data, along with id in case of success
- Also needs instance of service hence needs it to be auto wired

-> @Entity
- makes class have equivalent table in db
	- Here @ Id needed for primary value
	- @ GeneratedValue (strategy = GenerationType=AUTO) 
	- This info is for Database
	- Converting one data type to another (JSON to Java (Done by Jackson) -> serialisation, opposite to it deserialisation)
	- @RequestBody tells to convert to JSON
	-  should have default constructor to allow json for deseriailisation 
	- FlyWay for migration
	- 

-> Service
- @Service
- Autowired instance of repository
- 

- Repository
- @Reposiotry
	- For interacting with database
	- Should extends JpaRepository(Learner, primaryKey) with triangle brackets like in the way of generics


# API Modelling
We should have query parameters, as then we need to distinguish between endpoints as for browser, learner/1 and learner/pawan is same
- Cant have to endpoints with 2 path-variables 
- Cant have to endpoints with same resource and same verb

@PathVariable("learnerId") binding needed when variable named different or else we don't need it

with OPtional of type t we use get(),  then we can get ot else null pointerException

Complex relationships, parent child relationships
Here law of demetre isnt violated in the represenations

We use JPAQL 
@Query when we want to define our own query

# Errors and Exceptions
- Errors are un-handleable (Not recoverable)
- Exceptions are handleable (Recoverable)
	- Checked : They are checked by compiler on compile time. Otherwise cant compile
		- Achieved by extending Exception
	- Unchecked : Runtime Exceptions that happens 
		- Achieved by extending runtime exception

Bubbling : pushing it up to service, controller etc so we can actually get it.

@ExceptionHandler
get called by servlet 
For method handling the exception for specific class

However
For handling exceptions, here we use @ControllerAdvice fro class which wants to be universal error handler 

## Entity Relationships
6 ways
- 
Normalised ways




# Additional Resources to read.
https://stackoverflow.com/questions/52409579/protocol-buffer-vs-json-when-to-choose-one-over-the-other

https://www.linkedin.com/blog/engineering/infrastructure/linkedin-integrates-protocol-buffers-with-rest-li-for-improved-m

https://github.com/toon-format/toon



