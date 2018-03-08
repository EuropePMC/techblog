---
layout: post
title:  "The Importance of Software Testing in DevOps"
date:   2018-03-08
author: rakesh
categories: testing
---


Software testing is the process of identifying the correctness and quality of a software program. In other words, testing is executing a system or application in order to find software bugs, defects, errors or unexpected behavior. 

Software testing is necessary because we all make mistakes. Some of those mistakes are minor, but others can be expensive or dangerous. Especially while practicing [continuous integration, continuous delivery, or continuous deployment](https://www.atlassian.com/continuous-delivery/ci-vs-ci-vs-cd), we need to test anything and everything we produce, because things can always go wrong.

Testing is mainly classified into two types, **Functional Testing** and **Non-functional Testing**.

[![Types of Functional and Non-functional testing][testing1]][testing1]

Functional testing processes test against the specifications, or functional requirements for a system and its components (what the system should *do*), while non-functional testing processes test the operation of that system (how the system should *be*).

## Common types of Functional Testing

### Unit Testing

In Unit Testing, the scope of testing is limited to a particular unit or component—for example, a specific [API](https://en.wikipedia.org/wiki/Application_programming_interface), [database](https://en.wikipedia.org/wiki/Database), or [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface). 

#### Tips:
*	API: Have separate unit tests for individual web services
*	Database: Create tests to add, edit or remove data
*	GUI: Focus on field-level validation
*	Use [branch coverage or statement coverage](https://en.wikipedia.org/wiki/Code_coverage). 
*	Add some negative tests 
*	As a best practice, it is more reliable to use 'mock' service(s) to write unit tests, in order to avoid interdependence between components
*	Think about data re-usability, and clearing any test data from the database at end of your test (if applicable)

#### Tools / Frameworks:

The [Junit](https://junit.org/junit5/) and [TestNG](http://testng.org/doc/) unit testing frameworks are popular for a Java-based development environment. For Ruby, [RSpec](http://rspec.info/) is widely used. 

For the front-end, the [Karma test runner](http://karma-runner.github.io/2.0/index.html) is commonly used in development environments using AngularJS or Vue.js to run JavaScript-based unit tests. [Protractor](https://www.protractortest.org/#/) and the BDD-based [Jasmine framework](https://jasmine.github.io/) are also widely used. Those using React might prefer [Jest](https://facebook.github.io/jest/), while Ember.js has an integrated unit testing provision. [Mocha](https://mochajs.org/) is yet another JavaScript alternative for front-end unit testing.

### Sanity Testing

Sanity testing runs before any detailed functional or regression tests and tests basic, integral functionalities of an application. Sanity testing is required to run every commit to make sure critical business functionalities (such as the launching of the application) are not affected by code changes. 

### System Integration Testing

System Integration Testing (SIT) will touch multiple units/components and is a [black box testing](https://en.wikipedia.org/wiki/Black-box_testing) method. Performing this testing should not require knowledge of the internal workings of the system.

Normally within a sprint, manual testing will be the first phase of the SIT. Later on, this will be converted to an automated test script. If there is a dedicated automation testing resource available in the Agile team, then an automation test script can be developed in parallel to development activities. The automated test script will fast-track regression testing prior to each release or every commit in the continuous integration / continuous deployment model. 

#### Tools / Frameworks:

These tools and frameworks are used by the Europe PMC development team.

* Defect tracking tool &ndash; JIRA
* Automation Testing tool &ndash; Selenium
* Automation Framework &ndash; Serenity BDD
* Programming Language &ndash; Java
* Unit Testing Framework for Test Automation &ndash; JUnit
* Build Tool &ndash; Maven
* Schedule and Execution &ndash; Jenkins

Automation scripts can be developed in any language, and it is not mandatory for the testing team to use the same technology that the development team uses.

### Regression Testing

Regression testing ensures that software performs the same functionality in the same way after it is updated or changed. Regression testing should be performed after any code change to a previously developed and tested program, to ensure that new defects have not been introduced.

### User Acceptance Testing (UAT)

UAT is normally conducted by the actual users of a particular system. There will be end-to-end scenarios for the UAT users to execute to verify system functionalities. In the w[aterfall model](https://en.wikipedia.org/wiki/Waterfall_model), UAT will be conducted only at the end of development, whereas in the Agile model, UAT can be performed at the end of every sprint and feedback given to the team. 

## Common types of Non-functional Testing

### Performance Testing

Software performance testing is used to determine the speed or effectiveness of a computer, network, software program, or device. This process can involve quantitative tests done in a lab, such as measuring the response time or the number of MIPS (millions of instructions per second) at which a system functions. Performance testing ("How fast is the system?") can also include load testing ("How much volume can the system process?").

#### Tools / Frameworks:

[Gatling](https://gatling.io/) or [JMeter](https://jmeter.apache.org/)

*Sample 'Gatling' Performance Test Results:*

[![Sample 'Gatling' Performance Test Results:][testing8]][testing8]

### Security Testing

Security testing is a technique to determine if an information system protects data and maintains functionality as intended. Its aims should be verifying three basic principles&mdash;confidentiality, integrity, and authentication.

### Compatibility Testing

Compatibility testing involves verifying a service's functionality is the same across various browsers, different browser versions, mobile devices, operating systems, etc.

### Usability Testing

Usability testing is used in user-centered interaction design to evaluate a product by testing it on users. This is an irreplaceable testing practice, since it gives direct input on how real users use the system. 

## Automating your Testing

Test automation is the process of converting manual test scripts to automated test scripts, using testing tools like [Selenium](https://www.seleniumhq.org/), [Appium](http://appium.io/), [SoapUI](https://www.soapui.org/), [REST-Assured](http://rest-assured.io/), [Serenity](http://www.thucydides.info/#/), [Cucumber](https://cucumber.io/), etc. Test automation will fast-track regression testing, and it avoids repeated and time-consuming manual testing efforts. It is also convenient to use automated testing for compatibility testing.

*Sample Automation / Cucumber-BDD-Serenity Test Report:*

[![Sample Automation / Cucumber-BDD-Serenity Test Report][testing7]][testing7]

### Benefits of Automated Testing

*	Faster feedback
*	Earlier Detection of Defects
*	Accelerated Results
*	Running tests 24/7
*	Fewer human resources
*	Reusability
*	Reliability
*	Simultaneity
*	Better test coverage with multiple data combinations

### Test Flows, Test Management & Execution Frequency

[![Sample test flow][testing5]][testing5]

[![Example of execution frequency of different types of testing][testing6]][testing6]

<!--[!['Testing in DevOps'][testing2]][testing2]

As per the **Testing Pyramid** concept displayed above, around 70% of testing efforts are at the Unit Level, approximately 20% at the Integration/Business Layer and 10% at the UI/Front-end layer.-->

## Sample Build Pipeline model along with Software Testing steps
[![Sample Build Pipeline model along with Software Testing steps][testing4]][testing4]

In the above build pipeline model, there are three pre-production servers, i.e. Development (DEV), Testing (TEST), and Staging. Normally the DEV server will be used for all development activities, with the TEST server for functional testing by the quality assurance team, and the Staging server for performance testing and user acceptance testing. On some occasions, there will only be DEV, TEST and PROD (production) servers available. In such cases, internal testing and UAT will happen on the TEST server as well.

<!--### Testing Strategy in DevOps culture [Java-based development]
[!['Testing in DevOps'][testing3]][testing3]
It is also very clear that Test Automation is not the responsibility of a DevOps engineer whereas he/she will concentrate only on the **Infrastructure Automation** rather than enhance your **codebase**-->

## Proposed Tools & Framework Summary

<table style="font-size:smaller">
<thead><tr>
	<th>#</th><th>Description</th><th>Preferred&nbsp;&#8209;&nbsp;1</th><th>Paid?</th><th>Preferred&nbsp;&#8209;&nbsp;2</th><th>Paid?</th><th>Remarks</th>
</tr></thead>
<tbody>
	<tr><td>1</td><td>Automation Framework</td><td>Serenity-BDD with Cucumber - Junit</td><td>No</td><td>Python with Behave</td><td>No</td><td></td></tr>
	<tr><td>2</td><td>Front-end Automation </td><td>Selenium, Protractor</td><td>No</td><td>HP-UFT</td><td>Yes</td><td></td></tr>
	<tr><td>3</td><td>Mobile Automation</td><td>Appium</td><td>No</td><td>SeeTest</td><td>Yes</td><td></td></tr>
	<tr><td>4</td><td>Performance Testing</td><td>Gatling, JMeter</td><td>No</td><td>LoadRunner</td><td>Yes</td><td></td></tr>
	<tr><td>5</td><td>SOAP Web Service</td><td>SOAP-UI</td><td>No</td><td>ReadyAPI</td><td>Yes</td><td>JAX-WS/JAXB concept for Test Automation</td></tr>
	<tr><td>6</td><td>REST Web Service</td><td>SOAP-UI</td><td>No</td><td>Postman</td><td>No</td><td>Rest-Assured for Test Automation and  Frisby with JavaScript</td></tr>
	<tr><td>7</td><td>Continuous Integration</td><td>Jenkins</td><td>No</td><td>Bamboo</td><td>Yes</td><td></td></tr>
	<tr><td>8</td><td>Service Virtualization</td><td>Stub-o-matic, Mockito</td><td>No</td><td>HP Service Test</td><td>Yes</td><td></td></tr>
	<tr><td>9</td><td>Static Code Quality</td><td>SonarQube</td><td>No</td><td>PMD</td><td>No</td><td></td></tr>
	<tr><td>10</td><td>Code Coverage</td><td>JACOCO</td><td>No</td><td>Cobertura</td><td>No</td><td>Considering the primary language is Java</td></tr>
	<tr><td>11</td><td>Version Control</td><td>GitHub/GitLab</td><td>Yes</td><td>SVN</td><td>Yes</td><td></td></tr>
	<tr><td>12</td><td>Defect Management</td><td>JIRA</td><td>Yes</td><td>HP ALM</td><td>Yes</td><td></td></tr>
	<tr><td>13</td><td>Agile Project Management</td><td>JIRA-Agile</td><td>Yes</td><td>Trello</td><td>No</td><td>Trello free version is available with some limitations</td></tr>
	<tr><td>14</td><td>Security Testing</td><td>Vega</td><td>No</td><td>ZED Attach Proxy</td><td>No</td><td></td></tr>
	<tr><td>15</td><td>Penetration Testing</td><td>Metasploit</td><td>No</td><td>Wireshark</td><td>Yes</td><td></td></tr>
	<tr><td>16</td><td>Build Artifacts</td><td>jFrog Artifactory</td><td>No</td><td>Nexus</td><td>No</td><td></td></tr>
	<tr><td>17</td><td>CD Tool</td><td>OpenShift</td><td>Yes</td><td>Puppet</td><td>Yes</td><td></td></tr>
	<tr><td>18</td><td>Cloud-based Non-Mobile execution</td><td>Amazon - AWS</td><td>Yes</td><td>MS Azure</td><td>Yes</td><td>For Test Execution and deployment</td></tr>
	<tr><td>19</td><td>Cloud-based Mobile execution</td><td>SauceLabs</td><td>Yes</td><td>Amazon Device Farm</td><td>Yes</td><td></td></tr>
</tbody></table>

## Conclusion

Considering the multiple iterations over code in the Agile/DevOps software development model, testing is one of the most important phases of software delivery. To fast-track the testing process, automated functional & non-functional test-scripts are recommended. In the ideal scenario, each Agile team may have at least one QA resource who performs the testing activities for the current sprint, as well as ensuring the preservation of existing functionalities through regression tests.

### Useful links
* [BDD Serenity](http://www.thucydides.info/#/)
* [Gatling](https://gatling.io/)

  [testing1]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST1.JPG
  [testing2]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST2.JPG
  [testing3]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST3.JPG
  [testing4]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST4.JPG
  [testing5]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST5.JPG
  [testing6]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST6.JPG
  [testing7]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST7.JPG
  [testing8]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST8.JPG
  [testing9]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST9.JPG

