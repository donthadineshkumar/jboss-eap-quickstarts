bean-validation: Bean Validation Tested Using Arquillian
=======================================================
Author: Karel Piwko  
Level: Beginner  
Technologies: CDI, JPA, BV  
Summary: The `bean-validation` quickstart provides Arquillian tests to demonstrate how to use CDI 1.0, JPA 2.0 and Bean Validation 1.0.  
Target Product: JBoss EAP  
Source: <https://github.com/jboss-developer/jboss-eap-quickstarts/>  

What is it?
-----------

The `bean-validation` quickstart demonstrates how to use CDI 1.0, JPA 2.0 and Bean Validation 1.0 in Red Hat JBoss Enterprise Application Platform. It includes a persistence unit and some sample persistence code to introduce you to database access in enterprise Java. 

This quickstart does not contain a user interface layer. The purpose of this project is to show you how to test bean validation with Arquillian. If you want to see an example of how to test bean validation with a user interface, look at the [kitchensink](../kitchensink/README.md) example.

_Note: This quickstart uses the H2 database included with Red Hat JBoss Enterprise Application Platform 6. It is a lightweight, relational example datasource that is used for examples only. It is not robust or scalable and should NOT be used in a production environment!_

System requirements
-------------------

The application this project produces is designed to be run on Red Hat JBoss Enterprise Application Platform 6.1 or later. 

All you need to build this project is Java 6.0 (Java SDK 1.6) or later, Maven 3.0 or later.

 
Configure Maven
---------------

If you have not yet done so, you must [Configure Maven](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/CONFIGURE_MAVEN.md#configure-maven-to-build-and-deploy-the-quickstarts) before testing the quickstarts.


Start the JBoss EAP Server
-------------------------

1. Open a command prompt and navigate to the root of the JBoss EAP directory.
2. The following shows the command line to start the server:

        For Linux:   EAP_HOME/bin/standalone.sh
        For Windows: EAP_HOME\bin\standalone.bat


Run the Arquillian Tests 
-------------------------

This quickstart provides Arquillian tests. By default, these tests are configured to be skipped as Arquillian tests require the use of a container. 

_NOTE: The following commands assume you have configured your Maven user settings. If you have not, you must include Maven setting arguments on the command line. See [Run the Arquillian Tests](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/RUN_ARQUILLIAN_TESTS.md#run-the-arquillian-tests) for complete instructions and additional options._

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. Type the following command to run the test goal with the following profile activated:

        mvn clean test -Parq-jbossas-remote 


Investigate the Console Output
----------------------------

When you run the tests, JUnit will present you test report summary:

    Tests run: 5, Failures: 0, Errors: 0, Skipped: 0

If you are interested in more details, look in the `target/surefire-reports` directory. 

You can also check the server console output to verify that the Arquillian tests deployed to and ran in the application server. Search for lines similar to the following ones in the server output log:

    [timestamp] INFO [org.jboss.as.server.deployment] (MSC service thread 1-2) Starting deployment of "test.war"
    ...
    [timestamp] INFO [org.jboss.as.server] (management-handler-threads - 1) JBAS018559: Deployed "test.war"
    ...
    [timestamp] INFO [org.jboss.as.server.deployment] (MSC service thread 1-3) Stopped deployment test.war in 48ms
    ...
    [timestamp] INFO [org.jboss.as.server] (management-handler-threads - 1) JBAS018558: Undeployed "test.war

Server Log: Expected warnings and errors
-----------------------------------

_Note:_ You will see the following warnings and errors in the server log. This is because Hibernate attempts to drop the table and constraints before they are created without checking first to see if they exist. The issues can tracked here: <https://hibernate.atlassian.net/browse/HHH-6670> and <https://hibernate.atlassian.net/browse/HHH-9545>. You can ignore these warnings and errors.

    HHH000431: Unable to determine H2 database version, certain features may not work

    HHH000389: Unsuccessful: drop sequence hibernate_sequence
    Sequence "HIBERNATE_SEQUENCE" not found; SQL statement: drop sequence hibernate_sequence [90036-168]


Test the Quickstart in JBoss Developer Studio or Eclipse
-------------------------------------
You can also start the server and deploy the quickstarts or run the Arquillian tests from Eclipse using JBoss tools. For more information, see [Use JBoss Developer Studio or Eclipse to Run the Quickstarts](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_JBDS.md#use-jboss-developer-studio-or-eclipse-to-run-the-quickstarts) 


Debug the Application
------------------------------------

If you want to debug the source code of any library in the project, run the following command to pull the source into your local repository. The IDE should then detect it.

        mvn dependency:sources


