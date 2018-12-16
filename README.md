# Cucumber
Basic Cucumber project


Introduction to Basic Terminologies & keywords

Behaviour-driven development (BDD)
BDD emerged from and extends TDD. Instead of writing unit tests from specification why not make the specification a test itself. The main idea is that business analysts, project managers, users or anyone without technical, but with sufficient business, knowledge can define tests.

#Gherkin
BDD ideas sound very nice but actually are not so easy to put in practice. In order to make documentation sufficient for testing, it should follow some rules. This is where Gherkin comes in place. It is a Business Readable, Domain Specific Language created especially to describe behavior without defining how to implement it. Gherkin serves two purposes: it is your project’s documentation and automated tests
Gherkin is a line-oriented language that uses indentation to define structure. Line endings terminate statements (called steps) and either spaces or tabs may be used for indentation. Finally, most lines in Gherkin start with a special keyword

#Cucumber
Cucumber is not a testing tool it is a BDD tool for collaboration between all members of the team. So if you are using Cucumber just for automated testing you can do better. Testwise Cucumber is a framework that understands Gherkin and runs the automated tests. It sounds like a fairy tale, you get your documentation described in Gherkin and tests just run. Actually, it is not that simple, each step from documentation should have underlying test code that manipulates the application and should have test conditions.

#keywords
•	Features
•	Background
•	Scenarios
•	Steps
o	Givens
o	Whens
o	Thens
o	And, But
•	Scenario Outlines
•	Examples
•	* ->Regular expression to match test data

#Getting Started with Cucumber 
•	Pre-requisites:
o	IDE plugins — to enable BDD coding support in IDEs– e.g. Cucumber plugin for IntelliJ IDEA and Eclipse IDEs. Install Cucumber Editor from eclipse market place
o	BDD Test Framework — Used to define application behavior in plain meaningful English text using a simple grammar defined by a domain specific language (DSL)– e.g. Cucumber (DSL: Gherkin), JBehave (DSL: Gherkin), Behat (DSL: Gherkin), Mocha (DSL: user-defined). Add Cucumber java dependencies in POM.xml file
o	Test Runner — to automate and run the behavior tests– e.g. TestNG (Java), jUnit (Java), Mocha (JavaScript). Add Cucumber junit or cucumber-testng dependencies in POM.xml file

•	Create a Sample Cucumber Project using Maven
•	Create a Package & Write a Feature file using the Gherkin syntax
•	Write the step definition in Java
•	Write TestRunner & then
•	Run Cucumber
•	Learn the basic workflow of Behaviour-Driven Development (BDD)


#Creating a Cucumber Maven architype project

Configure Maven_Home & Maven bin path in Environmental variables
Navigate to the Path where we needed to create the project, type the below command from command line
mvn archetype:generate                     
   -DarchetypeGroupId=io.cucumber          
   -DarchetypeArtifactId=cucumber-archetype
   -DarchetypeVersion=2.3.1.2              
   -DgroupId=SampleCucumberTest                 
   -DartifactId=CucumberTest              
   -Dpackage=CucumberTest                 
   -Dversion=1.0.0-SNAPSHOT                
   -DinteractiveMode=false    
 
<groupId>SampleCucumberTest</groupId>
    <artifactId>CucumberTest</artifactId>
    <version>1.0.0</version>
    <packaging>jar</packaging>

 is created with all the cucumber dependencies

#Writing Feature files
Cucumber executes your .feature files in test/resources/features directory. These files contain executable specifications written in a domain specific language (DSL) called Gherkin which is a business-readable, plain-text, English-like language with a simple grammar. To specify business rules by real world examples, Gherkin use main keywords: Feature, Scenario, Given, When, Then, And, But, Background, Scenario Outline, Examples and some extra syntax “”” (Doc strings), | (Data tables), @(Tags), # (Comments).

#Features
Everything starts with a plain text file with .feature extension written in Gherkin language that describes only one product feature. It may contain from one to many scenarios.
Every *.feature file conventionally consists of a single feature. Lines starting with the keyword Feature: (or its localized equivalent) followed by three indented lines starts a feature. A feature usually contains a list of scenarios. You can write whatever you want up until the first scenario, which starts with Scenario: (or localized equivalent) on a new line. You can use tags to group features and scenarios together, independent of your file and directory structure.

A feature is a Use Case that describes a specific function of the software being tested. There are three parts to a Feature [16]
•	The Feature: keyword
•	The Feature name (on the same line as the keyword)
•	An optional description on the following lines

#Background 
Don’t repeat yourself
In some features, there might be one and the same Given steps before each scenario. In order to avoid copy/paste, it is better to define those steps as feature prerequisite with Background keyword.

 
Example Feature definition
Feature: Update User Profile
 A user with an account at a bank would like to update his profile information
 Provided he has a valid account, he should be allowed to make the Updation. 

Background: Launch the web browser & login 
Given User is on the Login page

Scenario: Update the User profile
 When User is on the Home Page
 And User clicks on update button
 And User update contact info as 996235512
 And User clicks on Update Button
 Then User should be displayed with a Successfull updation message
 
 Scenario: Scenario 2


#scenarios
Scenario is one of the core Gherkin structures. Every scenario starts with the Scenario: keyword (or localized one), followed by an optional scenario title. Each feature can have one or more scenarios, and every scenario consists of one or more steps.
Given
The purpose of Given steps is to put the system in a known state before the user (or external system) starts interacting with the system (in the When steps). Avoid talking about user interaction in givens. If you have worked with use cases, givens are your preconditions.
When
The purpose of When steps is to describe the key action the user performs 
Then
The purpose of Then steps is to observe outcomes. 

Multiple Givens.feature
Feature: Multiple Givens
Scenario: Multiple Givens
  Given one thing
  Given an other thing
  Given yet an other thing
  When I open my eyes
  Then I see something
  Then I don't see something else

If you have several Given, When or Then steps you can write:

Multiple Givens.feature
@tags @smoke @regression
#grouping, we can use multiple tags, which will be applicable for the feature, hence applies to all the scenario’s
Feature: Multiple Givens
#Use the feature file name as the “Feature name”
#when multiple keywords are to be repeated then we use “And” keyword. “But” keyword is used in negative steps

Scenario: Multiple Givens
  Given one thing
#second Given is replaced with And
    And an other thing
#second Given is replaced with And
    And yet an other thing
  When I open my eyes
  Then I see something
    But I don't see something else

#Tags
Organise features and scenarios
Tags can be used in order to group feature files. A tag can be applied as annotation above Feature or Scenario keyword in .feature file. Having correctly tagged different scenarios or features runners can be created per each tag and run when needed.
Quick Recap: Steps

•	Given - Describes the preconditions and initial state before the start of a test and allows for any pre-test setup that may occur
•	When - Describes actions taken by a user during a test
•	Then - Describes the outcome resulting from actions taken in the When clause
•	Occasionally, the combination of Given-When-Then uses other keywords to define conjunctions
•	And - Logical and
•	But - Logically the same as And, but used in the negative form

#Scenario’s cont..
Each Feature is made of a collection of scenarios. A single scenario is a flow of events through the Feature being described and maps 1:1 with an executable test case for the system.Keeping with the example ATM withdrawal feature, a scenario might describe how a user requests money and what happens to their account.
Feature: ATM Withdrawl
Scenario: Eric wants to withdraw money from his bank account at an ATM
    Given Eric has a valid Credit or Debit card
    And his account balance is $100
    When he inserts his card
    And withdraws $45
    Then the ATM should return $45
    And his account balance is $55


#Scenario Outline
Data-driven testing
Cucumber makes it very easy to handle cases of different business scenarios with different input data and different results based on that input data. The scenario is defined with Scenario Outline. Then data is fed to this scenario with Examples table where variables are defined with concrete values.
In some cases, one might want to test multiple scenarios at once to perform Equivalence partitioning and Boundary-value analysis.
A Scenario Outline provides a technique to specify multiple examples to test against a template scenario by using placeholders
At runtime the scenario is run against each row in the table. Column values are substituted for each of the named placeholders in the scenario.

Feature: ATM Withdrawl
Scenario Outline: A user withdraws money from an ATM
    Given <Name> has a valid Credit or Debit card
    And their account balance is <OriginalBalance>
    When they insert their card
    And withdraw <WithdrawalAmount>
    Then the ATM should return <WithdrawalAmount>
    And their account balance is <NewBalance>

    Examples:
      | Name   | OriginalBalance | WithdrawalAmount | NewBalance |
      | Eric   | 100             | 45               | 55         |
      | Gaurav | 100             | 40               | 60         |
      | Ed     | 1000            | 200              | 800        |



#Writing Step Definition files
To make it easy, Once the Feature file is ready, Run it. In the console we get the message about missing Step Definitions. Now create a new java file & add them into it.

Run as Maven Test

[INFO] Scanning for projects...
[INFO] 
[INFO] ------------------< SampleCucumberTest:CucumberTest >-------------------
[INFO] Building CucumberTest 1.0.0
[INFO] --------------------------------[ jar ]---------------------------------
[INFO] 
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ CucumberTest ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory E:\API_Testing\Eclipse\CucumberTest\src\main\resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.7.0:compile (default-compile) @ CucumberTest ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-resources-plugin:2.6:testResources (default-testResources) @ CucumberTest ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] Copying 2 resources
[INFO] 
[INFO] --- maven-compiler-plugin:3.7.0:testCompile (default-testCompile) @ CucumberTest ---
[INFO] Nothing to compile - all classes are up to date
[INFO] 
[INFO] --- maven-surefire-plugin:2.12.4:test (default-test) @ CucumberTest ---
[INFO] Surefire report directory: E:\API_Testing\Eclipse\CucumberTest\target\surefire-reports

-------------------------------------------------------
 T E S T S
-------------------------------------------------------
Running cucumberTest.RunCucumberTest
@Smoke @Regression
Feature: Gmail Login

  Background:                       # cucumberTest/Sample.feature:5
    Given The Gmail app is launched # null

  @Smoke @Regression @BVT
  Scenario: Login text Case2             # cucumberTest/Sample.feature:9
    When User is on the Gmail login page # null
    Then Enter the username as Ajay      # null
    And Enter the password as Password   # null
    And click on login button            # null

1 Scenarios (1 undefined)
5 Steps (5 undefined)
0m0.037s


You can implement missing steps with the snippets below:

====================================================================================
@Given("^The Gmail app is launched$")
public void the_Gmail_app_is_launched() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

@When("^User is on the Gmail login page$")
public void user_is_on_the_Gmail_login_page() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

@Then("^Enter the username as Ajay$")
public void enter_the_username_as_Ajay() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

@Then("^Enter the password as Password$")
public void enter_the_password_as_Password() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

@Then("^click on login button$")
public void click_on_login_button() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

Tests run: 5, Failures: 0, Errors: 0, Skipped: 5, Time elapsed: 0.59 sec

Results :

Tests run: 5, Failures: 0, Errors: 0, Skipped: 5

[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 4.542 s
[INFO] Finished at: 2018-12-17T02:03:28+05:30
[INFO] ------------------------------------------------------------------------

===================================================================================================================

Cucumber doesn’t know how to execute your scenarios out-of-the-box. It needs Step Definitions to translate plain text Gherkin steps into actions that will interact with the system. When Cucumber executes a Step in a Scenario, it will look for a matching Step Definition to execute.
When Cucumber matches a Step against a pattern in a Step Definition, it passes the value of all the capture groups to the Step Definition’s arguments.

Create a Step Definition File with the above 

=====================================================================================================================
@Given("^The Gmail app is launched$")
public void the_Gmail_app_is_launched() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

@When("^User is on the Gmail login page$")
public void user_is_on_the_Gmail_login_page() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

@Then("^Enter the username as Ajay$")
public void enter_the_username_as_Ajay() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

@Then("^Enter the password as Password$")
public void enter_the_password_as_Password() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

@Then("^click on login button$")
public void click_on_login_button() throws Exception {
    // Write code here that turns the phrase above into concrete actions
    throw new PendingException();
}

=====================================================================================================================



# Create a TestRunner - Auto generated with maven project type
After writing the features, the test runner code is implemented. In the following code TestRunner.java class, note the @CucumberOptions. One can define the location of features, glue files (step definitions), and formatter plugins inside this Cucumber options







Can also implement using TestNG as below


TestRunner.java

=========================================================================================================================
	@CucumberOptions(
	        features = "src/test/resources/features",
	        glue = {"stepdefs"},
	        tags = {"~@Ignore"},
	        format = {
	                "pretty",
	                "html:target/cucumber-reports/cucumber-pretty",
	                "json:target/cucumber-reports/json-reports/CucumberTestReport.json",
	                "rerun:target/cucumber-reports/rerun-reports/rerun.txt"
	        })
	public class TestRunner {
	    private TestNGCucumberRunner testNGCucumberRunner;

	    @BeforeClass(alwaysRun = true)
	    public void setUpClass() throws Exception {
	        testNGCucumberRunner = new TestNGCucumberRunner(this.getClass());
	    }

	    @Test(groups = "cucumber", description = "Runs Cucumber Feature", dataProvider = "features")
	    public void feature(CucumberFeatureWrapper cucumberFeature) {
	        testNGCucumberRunner.runCucumber(cucumberFeature.getCucumberFeature());
	    }

	    @DataProvider
	    public Object[][] features() {
	        return testNGCucumberRunner.provideFeatures();
	    }

	    @AfterClass(alwaysRun = true)
	    public void tearDownClass() throws Exception {
	        testNGCucumberRunner.finish();
	    }
	}
	 
	=========================================================================================================================

#Writing Hooks
Cucumber hooks are more like utility functions which help to perform some activity before/after/during execution. With that, you must remember that not only Cucumber, but also the test runner also performs hook functions. According to the priority of each hook type, one can implement their activities in them appropriately.

#Execution Priority
TestNG’s @BeforeClass → Cucumber’s @Before → Cucumber Background → Cucumber Scenario → Cucumber’s @After → TestNG’s @AfterClass
Running Tests


#Generating Reports
