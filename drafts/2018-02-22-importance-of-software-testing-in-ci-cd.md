---
layout: post
title:  The Importance of Software Testing in DevOps
date:   2018-02-22
author: rakesh
categories: testing
---


**Software Testing** is the process of identifying the correctness and quality of a software program. In other words, testing is executing a system or application in order to find software **bugs, defects, errors or unexpected behavior**. 

Software Testing is necessary because we all make mistakes. Some of those mistakes are minor, but others can be expensive or dangerous. Especially while practicing [continuous integration, continuous delivery, or continuous deployment](https://www.atlassian.com/continuous-delivery/ci-vs-ci-vs-cd), we need to test everything and anything we produce, because things can always go wrong.

Testing is mainly classified into two types, **Functional Testing** and **Non-functional Testing**.

[!['Types of Functional and Non-functional testing'][testing1]][testing1]

Functional testing processes test against the specifications, or functional requirements for a system and its components (what the system should *do*), while non-functional testing processes test the operation of that system (how the system should *be*).

## Common types of Functional Testing

### Unit Testing

In Unit Testing, the scope of testing is limited to a particular unit or component—for example, a specific [API](https://en.wikipedia.org/wiki/Application_programming_interface), [database](https://en.wikipedia.org/wiki/Database), or [GUI](https://en.wikipedia.org/wiki/Graphical_user_interface). 

#### Tips:
*	Focus on the field level validation
*	Branch coverage or statement coverage. 
*	Add some negative tests 
*	Add, Edit or Remove data from the database if applicable. 
*	As a best practice, it is more reliable to use ‘mock’ service(s) to write the Unit tests in order to avoid the interdependence between components. 
*	Think about the data re-usability and clearing off the test data, which is used by the test from the database at end of your test if applicable. 
*	Have separate Unit Tests for the Web Services

#### Tools / Frameworks:

**Junit** and **TestNG** Unit Testing Frameworks are popular for the Java based development environment and for Ruby, **RSpc** is widely used. For the front-end, frameworks like **ember.js** already have an integrated unit testing provision to implement the unit tests. Whereas **Karma** – Test Runner is commonly used in AngularJS-based development environments to run the JavaScript-based Unit Tests. **Mocha** is an alternative for the front-end Unit Testing solution. In the JavaScript world, **Protractor** along with the **Jasmine** unit testing framework (BDD-based) are widely used.

### System Integration Testing

System Integration Testing (SIT) will touch multiple units/components and is a black box Testing method. People who perform this testing do not want to know the logic behind it.

Normally within the Sprint, Manual Testing will be the first step of the **System Integration Test**. Later on, this will convert to an Automated Test script. If there is a dedicated Automation Testing resource available in the Agile team, then an Automation Test script can be developed in parallel to the development activities. The Automated Test script will fast-track the regression testing prior to each release or every commit in the Continuous Integration / Continuous Deployment model. 

#### Tools / Frameworks:

Defect tracking tool – JIRA

Automation Testing tool – Selenium

Automation Framework – Serenity BDD

Programming Language - Java

Unit Testing Framework for Test Automation – JUnit

Build Tool – Maven

Schedule and Execution – Jenkins

Automation scripts (browser-based) can be developed in any language and it is not mandatory to use the same technology that the Development team uses.

### User Acceptance Testing (UAT)

UAT is normally conducted by the actual users of that particular system. There will be end-to-end scenarios for the UAT users to execute and verify the system functionalities. In the Waterfall model, UAT will be conducted only at the end, whereas in the Agile world, UAT can be performed at the end of every sprint and feedback given to the team. 

## Common types of Non-functional Testing

### Performance Testing

Software performance testing is used to determine the speed or effectiveness of a computer, network, software program or device. This process can involve quantitative tests done in a lab, such as measuring the response time or the number of MIPS (millions of instructions per second) at which a system functions.
Performance Testing = how fast is the system
Load Testing = how much volume can the system process?

#### Tools / Technique

Gatling or JMeter

### Security Testing

**Security testing** is a **testing** technique to determine if an information system protects data and maintains functionality as intended. It also aims at verifying three basic principles - Confidentiality, Integrity and Authentication.

### Usability Testing

**Usability testing** is a technique used in user-centered interaction design to evaluate a product by **testing** it on users. This can be seen as an irreplaceable usability practice, since it gives direct input on how real users use the system. 

## Automating your testing

**Test Automation** is process of converting the manual test-scripts to automated test scripts using Testing tools like Selenium, Appium, SoapUI, REST-Assured etc. Test Automation will fast track the **Regression Testing** (recommended after the code changes) and it avoids repeated manual testing efforts. It is also more convenient to use  Automated Testing for the **Compatibility Testing**, like verifying the functionality on various browsers, different browser versions, multiple mobile devices, more than one operating system etc.

*	Faster feedback
*	Earlier Detection of Defects
*	Accelerated Results
*	Running tests 24/7
*	Fewer human resources
*	Reusability
*	Reliability
*	Simultaneity
*	Better test coverage with multiple data combinations

[!['Testing in DevOps'][testing2]][testing2]

As per the **Testing Pyramid** concept displayed above, around 70% of testing efforts are at the Unit Level, approximately 20% at the Integration/Business Layer and 10% at the UI/Front-end layer.

## Testing Strategy in DevOps culture [Java-based development]
[!['Testing in DevOps'][testing3]][testing3]

## Sample Build Pipeline model along with Software Testing steps
[!['Testing in DevOps'][testing4]][testing4]

In the above build pipeline model, there are three pre-production servers i.e. Development (DEV), Testing and Staging. Normally DEV server will be used for all the development activities, with the Testing or System Integration Server (SIT) for Functional Testing activities for the Quality Assurance (QA) Team and Staging Server for the Performance Testing as well as for the User Acceptance Testing (UAT) activities. On some occasions, there will only be DEV, TEST and PROD servers available. In such cases, internal testing and UAT will happen on the TEST Server itself.

You might have noticed the build pipeline steps ‘Sanity Tests’ & ‘Regression Tests’ from the Pipeline sample displayed above. Sanity Tests consist of critical functionalities of an application and are required to run every commit to make sure the critical business functionalities are not affected. Whereas Regression Tests are the superset of the Sanity Test Suite that will normally run in the Test Environment for every new deployment.

## Test Flows, Test Management & Execution Frequency

[!['Testing in DevOps'][testing5]][testing5]

[!['Testing in DevOps'][testing6]][testing6]

## Sample Automation / Cucumber-BDD-Serenity Test Report

[!['Testing in DevOps'][testing7]][testing7]

## Sample 'Gatling' Performance Test Results 

[!['Testing in DevOps'][testing8]][testing8]

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

Considering the multiple iterations in the Agile/DevOps model, **Testing** is one of the most important phases of software delivery and to fast track the testing process, automated functional & non-functional test-scripts are in high demand. In the ideal scenario, each Agile team may have at least one QA resource who ensures the Testing activities for the current sprint as well as taking care of the existing functionalities through the Regression Tests. It is also very clear that Test Automation is not the responsibility of a DevOps engineer whereas he/she will concentrate only on the **Infrastructure Automation** rather than enhance your **codebase**.

### Useful links
* [Testing Pyramid](https://testing.googleblog.com/2015/04/just-say-no-to-more-end-to-end-tests.html)
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

