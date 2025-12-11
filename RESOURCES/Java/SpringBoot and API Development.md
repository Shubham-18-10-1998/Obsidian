
# What is a web-application?
An executable - What we alone can run on our device
A Web Application : Expose the logic over the internet, so that application is accessible over the internet
	- Can interact with Postman
	- One application can interact with another
	- Anything with interacts with application - Client
- Something to run the application and listen to the request - Server 
	- And this has a port where it listens.
	- Reserved ports : not accessible otherwise
	- The Port has JAR/WAR

The language of communication :
	- API : Application Programming Interface
	- Http : Language of communication

Bootstrap/BoilerPLate code : What handles auxiliary functions like what TCP socket listens, and transfers to application. This is done by framework which provides foundation to build application

SpringBoot is built on Spring.  Simplifies the process.
To Run Spring, add it to dependency via gradle.build

Features of Spring :
- All beans are singleton by default, to make copies we use prototype.

LEARNING: MAIN CLASS CANNOT BE EMPTY TO RUN APPLICATION

# Inversion of Control
The process of giving spring the control of making objects(beans) and managing them is called Inversion of Control (IoC).


# Bean 
## What is a bean?
Its an object thats created by Spring for us at the time of code compilation itself so that they are available to be used at runtime by us. The lifecycle is managed by Spring (including creation cause otherwise we create it using **new** keyword).

Helps us achieve Inversion of control as Spring now has the control to mange the objects instead of us.
**Note :  All beans are created at once**

To make a bean we have three ways supported by Spring:
- XML based configuration
- Java Based Configuration
- Annotations Based using @Annotaions

POJO (plain Old Java Object ) is the object that java manages as a bean.
So in essence, the class with setters and getters and constructors is our POJO.

### XML Based Configurations
For this we create an xml file to list the beans to be used/made by the spring to put in Spring Container so we can use them.
- XML based configuration : oldest
	- create an xml file :
	- Then we do 
		- ApplicationContext context = new  ClassPathXMLApplicationContext("filename.xml")
			- This tells where to get the context to make the beans.
			- Application context is creating the spring container with beans.
		- Then object = context.getBean(ClassName.class)
		- If we create more than one bean for a class without id, the code breaks because of ambiguity as the code doesn't understand which bean to use.
	- Learnings :
		- If we are using constructor based (constructor-arg tag), we need a matching constructor.
		- If we are using setters to put values (using property tag), we need a default constructor to instantiate the object, so that object can be instantiated and then we can use the setters.
		- We can also fetch beans using only id and not supplying class, but then we need to explicitly type cast to the class of the reference we are using to make it compatible getBean("name") returns an object, and child reference cant hold parent type object which is enforced during compile time type checking

### Java Based Config
For this we create config class and then pass that to the AnnotationConfigApplicationContext(ConfigClassName.class);
- We have to put @Configuration on top of configuration class to help Java know that this class provides the config.
- Here the method name becomes the bean id. Or we can explicitly provide a name @Bean(name="newName). This overrides the method name as id.
	- **Note :** The name of one bean cannot be method name of another bean method.


### Annotation Based 
For this we use annotations to achieve the bean structure.
**Note : ** Even for this we need to provide a configFile for context;
This is achieved by using Annotation
- SpringBoot uses only Annotation
- @Component : object of classes will be beans
- @Value("${class.property})
- @Autowired : automatically find an object appropriate bean and put it here.
- @ComponentScan("packages") - where to find the components
- @PropertySource("classpath:application.properties")
- For putting @Value on top of instance variables, setters needed.
- Or else pass through constructor and argument put @Value
- application.properties : has values
- All beans are singleton by default, to make copies we use prototype.

