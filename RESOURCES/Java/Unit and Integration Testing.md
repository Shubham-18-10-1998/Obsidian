


## Unit Testing
Testing in isolation
- Can't mock database
- Requirements
	- Runner Framework -> JUNIT / TestNG
	- Assertion Framework -> AssertJ / Hamcrest
	- Mocking Framework


- Steps 
	- @SpringBootTest for the spring to make test container 
		- Instead of @ExtendWith(MockitoExtension.class) for unit testing
		- Used for integration Testing
	- @Test for each test
	- Structure
		- Arrange
		- Act
		- Assert
	- For the bean, we add mocks

So we use InjectMocks to create a fake bean of class and then pass fake dependencies using mock for which we to mimic behaviour

NOTE : Test need not run in order.

Anatomy of Test :
- BeforeAll :
	- Should be static as before any test of class happens
- BeforeEach
- AfterAll
- AfterEach

For testing Repository : we don't mock the database
Issues -
-  Database calls are very long -> Flakiness in test
- H2 database so we can avoid concurent issue cause by common database.
- @DataJpaTest
	 Each establishes a unique session

Testing Controller
MockMVC : responsible for mocking a server getting calls, without actually starting a server.
With @SpringBootTest, we don't need to do inject with Mock. The auto-wired gets the mock bean itself.
Controller always gets api call, never call function of controller.
SpringBootTest -> automatically creates all the beans. and since we don't need to call controller explicitly, we don't need to inject the dependency by auto wiring.

Best Practices 
- Anatomy of tests followed
- Independent
- Arrange , Act, Assert


## Integration Testing
Testing blocks working together
 SpringBootTest we have to do database cleanup
 @Priority(Number) is used to give order to tests.

Testing has to be done first before jacoco test coverage .




Tests arent packaged as deployable jar