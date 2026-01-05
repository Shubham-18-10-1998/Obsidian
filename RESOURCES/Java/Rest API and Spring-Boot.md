
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
- ### Dispatcher Servlet
	- Handles the request
	- It checks for format of endpoint, doesn't do validation for dataType or check for dataType
- ### Handler Mapping 
	- Chooses which controller should the req go to
- ### Handler Adapter 
	- Converts the req data to java understandable (Serialisation, De-serialisation)
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
Need a driver to communicate to Database to Make them compatible
H2 -> Memory
MySql -> Disk

Framework of frameworks -> Spring/SpringBoot

## Now for making applications
- ### @RestController
- In req, 
	- req body (JSON ->)
	- response body
- Response
	- Status code, reflection -> we get original information from data, along with id in case of success
- Also needs instance of service hence needs it to be auto wired

- ### @Entity
- makes class have equivalent table in db
	- Here @ Id needed for primary value
	- @ GeneratedValue (strategy = GenerationType=AUTO) 
	- This info is for Database
	- Converting one data type to another (JSON to Java (Done by Jackson) -> serialisation, opposite to it deserialisation)
	- @RequestBody tells to convert to JSON
	-  should have default constructor to allow json for deserialisation 
	- FlyWay for migration
	- Learnings
		- Values need to Long, Integer DataTypes instead of primitive as this allows for null values which are needed when not supplied by JSON in case of id which is supplied as null in case of autogeneration

- ### Service
	- @Service
	- @Autowired instance of repository

- ### Repository
	- @Reposiotry
		- For interacting with database
		- Should extends JpaRepository(Learner, primaryKey) with triangle brackets like in the way of generics
	- We use JPQL -> we have predefined functions to map to the possible query with keywords specified by JPQL.
	- @Query when we want to define our own query
	- Or we can use @NamedQuery

## Application.properties for setup and to see consoles and debug for database operations
spring.datasource.driverClassName=org.h2.Driver  
spring.datasource.username=user  
spring.datasource.password=pass  
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect  
spring.jpa.show-sql=true  
spring.h2.console-path=/h2-console  
spring.h2.console.enabled=true

# API Modelling
We should have query parameters, as then we need to distinguish between endpoints as for browser, learner/1 and learner/pawan is same
- Cant have two endpoints with path-parameters because of above mentioned reason 
- Cant have two endpoints with same resource and same verb

## Difference between query parameters and path parameters

- ### Query Parameteres
	- They are optional key-value pairs after ? in url.
	- They are used to identify HOW/WHICH
	- In SpringBoot passed using @RequestParam
	- They don't come in path, hence @GetMapping(/resource) itself and the function gets the as @RequestParam("key-for-value-we-are-supplying", ).
	- We can supply opyional queryParamters as (@RequestParam(value = "key",  required = false))
- ### Path Parametres
	- They are part of the url itself and used to identify specific resources. Passed after / in {} brackets
	- They **CANNOT** be omitted.
	- In SpringBoot passed using @PathVariable
	- If name same don't have bind with @PathVariable("keyName"), if values name is same as variable name.
	- For binding value in url of mapping should be same as value in pathVariable supplied.

|Feature|Path Parameter|Query Parameter|
|---|---|---|
|URL position|Part of path|After `?`|
|Purpose|Identify resource|Filter / modify request|
|Mandatory|Yes|Usually optional|
|Order matters|Yes|No|
|RESTful usage|Strong|Secondary|
**NOTE: We shouldn't use query parameters to identify resources.**

## 🎯 **Rule of Thumb**

- **Path Parameter → WHO / WHICH resource**
    
- **Query Parameter → HOW / WHICH filters**

@PathVariable("learnerId") binding needed when variable named different or else we don't need it

with Optional of type t we use get(),  then we can use get to fetch non-null value or else NullPointerException

Complex relationships, parent child relationships
Here law of demetre isnt violated in the represenations

# Errors and Exceptions
- Errors are un-handleable (Not recoverable)
- Exceptions are handleable (Recoverable)
	- Checked : They are checked by compiler on compile time. Otherwise cant compile
		- Achieved by extending Exception
	- Unchecked : Runtime Exceptions that happens 
		- Achieved by extending runtime exception
- Two ways to handle
	- Throw
	- Try, catch blocks

Bubbling : pushing it up to service, controller etc so user can actually get it.

We can handle runtimeExceptions too, but they represent runtime issues hence aren't meant to be handled. so its like s principle to have expected exceptions to be checked which extend Exception Class.

@ExceptionHandler
get called by DispatcherServlet 
For method handling the exception for specific class

However
For handling exceptions, here we use @ControllerAdvice for class which wants to be universal error handler 

## Entity Relationships
6 ways (Cohort and Student)
- Make a column for studentID in cohort
	- this leads to redundancy as we have to copy same cohort data as many times as unique students for it are there.
- Make a list column in cohort, but this is putting a nail in your own foot.
	- Reason : Lists cannot be indexed in SQL.
- Make a column in cohort
- Make a column in cohort with list, but again same problem
### Normalised ways
- Join table 
	- Make a table mapping cohortId to studentId
	- A primary key being referenced in another table becomes a foreign key there.
	- Only needed for many-many relationships

**NOTE: Way represented in table for data very different from class relationships**

JPA always represents data in normalised fashion without us taking care of it.

# Back Referencing

- ## Why we don't add reference in learner also for cohort
	- Because then we have two join tables. Because both are owning the relationship as one can own the others, not both way.
	- We add reference but use mappedBy("learner") list. this remembers that the table by owner is also utilised here, and this doesn't own the relationship
		- Back owning doesn't manage the relationship
	- We need the reference so we can query for learner's cohorts
	- We cant delete cohort without deleting the relationship wit learners. known as foreign key constraint
	- As learners is aggregation, cant pass learners list to Cohort. Cannot club cohort creation with learners. creation of cohort, Learner creation, and assigning learner to cohort is three different operations
	- Without getters and setters Jackson cannot add values for instance variables.
	- Circular reference leads to infinite
	- @JsonIgnore -> doesn't return in the JSON response
- Hence we use DTOs to reduce circular dependency in JSON.
- In Many to one -> the many to one is the owner of the relationship
- Many to one cannot use back-reference
- One to many is the back-reference
	- Without mapped by there will be a redundant join table
	- The Java representation isn't equivalent to DB representation
	- For entities always have to mention cardinality of the relationship
- When we add back-reference with then both body according to the code own the relationship, and hence we get a redundant join table

# Cascading 
Multiple Operations have to happen in an order.
- Keep transactional to allow atomicity so that if error occurs, then we revert everything that happened, or else if completed only then changes committed.
- Cascading operations, They don't do validations
- When added or deleted to the parent, then child also

# Learnings
- to see what process is running on a port, we use lsof -i:portNumber
- To kill the process on that id, we do, kill -9 proccesID. Where processID is the processID for process running on that port.
- Browsers always perform a GET.
- If we try doing getReferenceByID(), we only get a reference, and hence cant use this to return in get endpoint as the lazyLoading is done at the time of deserialisation, but by then session to hibernate is closed and hence we get lazyLoadingException. 
- ?1 refers to the first argument being passed
- @Param(email) and in query pass as :email
- JPQL != SQL, the syntax and way we pass values is very different. 
- When we are making a new relationship, then post
- Every-time there is a relationship between entities, we have to mention cardinality
- Foreign Key Constraint is that we cannot an entity from the parent table where foreign key is present without deleting the relationship itself
- Logically separate entities shouldn't cascade. But tightly coupled like Entity and Entity metadata should be cascade. Where validation could be required, there we shoudnt use cascade.
- Inheritance and aggregation -> eg -> Course has batched with id, the batched can have same id, as they all exist in the same table, but their parent in the data-world is different. 

# Sequel Ace
For querying the database

# Server health
Observability and Monitoring
- Event Driven System
	- Actuator is library in Spring-Boot to monitor server health


# Validating
- For user input -> controller
- For derived values -> db call time
- Extra fields are always neglected
- HIBERNATE VALIDATIONS are used to validate entity
- Validation rules added to entity. In controller, we add @Valid annotation to the entity we are inputting
- Validation throw MethodArgumentException

# Best Practices for APIs

## What is versioning for APIs
Contract BETWEEN US ANSD PAWAN ABOUT CLASS TIMES
What if he changes from 8 - 10 to 10-12

Changing contract such that, previous version fails -> backward incompatible change
If change like adding not required query parameter, is back-compatible changes
if cohort/{cohortId}/learners -> cohort/learners?=cohortId (back-incompatible)

To prevent breakages, we use versioning for not-backward incompatible changes.

## What is pagination and sorting

We use pagination when payload is going beyond 20mb, to break the response into segments.
To prevent 
- Add pagination to divide into segments
	- But every thing it needs it queries
	- Number of response to get each time is also parameter

# Why Sorting ?
If sorting in UI, then localised sorting
Global if done in server

@RequestingMapping("v1")

- For pagination -> Page
JPA -> support pagination

Use parent child relationships wherever necessary


# Unit testing and Integration Testing
Shift left -> 

Unit testing -> each indiviual functionality is working fine






# Additional Resources to read.
https://stackoverflow.com/questions/52409579/protocol-buffer-vs-json-when-to-choose-one-over-the-other

https://www.linkedin.com/blog/engineering/infrastructure/linkedin-integrates-protocol-buffers-with-rest-li-for-improved-m

https://github.com/toon-format/toon

Read normalisation

Doubts?
So Owning means - they have the original reference for the back-reference?

Many to one with-out mapped by what happens?








