---
layout: post
title:  "Importance of Software Testing in Continuous Integration/Continuous Delivery or DevOps"
date:   2018-02-22
author: rakesh
categories: testing
---


**Software Testing** is the process of identifying the correctness and quality of a software program. In other words, testing is executing a system or application in order to find software **bugs, defects, errors or unexpected behavior**. 

Software Testing is necessary because we all make mistakes. Some of those mistakes are unimportant, but some of them are expensive or dangerous. We need to check everything and anything we produce because things can always go wrong.

Testing is mainly classified into two types i.e., **Functional Testing** and **Non-Functional Testing**.

[!['Testing in DevOps'][testing1]][testing1]
[!['Testing in DevOps'][testing2]][testing2]

As per the **Test Pyramid** concept displayed above, around 70% of testing efforts are at the Unit Level, approximately 20% at the Integration/Business Layer and 10% at the UI/Front-end layer.

## Testing Strategy in the DevOps culture [Java-based development]
[!['Testing in DevOps'][testing3]][testing3]

## Sample Build Pipeline model along with Software Testing steps
[!['Testing in DevOps'][testing4]][testing4]

In the above build pipeline model, there are three pre-production servers i.e. Development, Testing and Staging. Normally DEV server will be used for all the development activities, with the Testing or System Integration Server (SIT) for Functional Testing activities for the Quality Assurance (QA) Team and Staging Server for the Performance Testing as well as for the User Acceptance Testing (UAT) activities. On some occasions, there will only be DEV, TEST and PROD servers available. In such cases, internal testing and UAT will happen on the TEST Server itself.

You might have noticed the build pipeline steps ‘Sanity Tests’ & ‘Regression Tests’ from the Pipeline sample displayed above. Sanity Tests consist of critical functionalities of an application and are required to run every commit to make sure the critical business functionalities are not affected. Whereas Regression Tests are the superset of the Sanity Test Suite that will normally run in the Test Environment for every new deployment.

Below are the most commonly used and unavoidable Testing types.

## Unit Testing

In Unit Testing, the scope of testing is limited to that particular unit or component. 

**Tips:**
*	Focus on the field level validation
*	Branch coverage or statement coverage. 
*	Add some negative tests 
*	Add, Edit or Remove data from the database if applicable. 
*	As a best practice, it is more reliable to use ‘mock’ service(s) to write the Unit tests in order to avoid the interdependence between components. 
*	Think about the data re-usability and clearing off the test data, which is used by the test from the database at end of your test if applicable. 
*	Have separate Unit Tests for the Web Services

**Tools / Framework:**

**Junit** and **TestNG** Unit Testing Frameworks are quite popular for the Java based development environment and for Ruby, **RSpc** is widely used. For the front-end, frameworks like **ember.js** already have an integrated unit testing provision to implement the unit tests. Whereas **Karma** – Test Runner is commonly used in AngularJS-based development environments to run the JavaScript-based Unit Tests. **Mocha** is an alternative for the front-end Unit Testing solution. In the JavaScript world, **Protractor** along with the **Jasmine** unit testing framework (BDD-based) is widely using.


## System Integration Testing

System Integration Testing will touch multiple units/components and it is a black box Testing. People who perform this testing do not really want to know the logic behind it.

Normally within the Sprint, Manual Testing will be the first step of the **System Integration Test**. Later on, this will convert to an Automated Test script. If there is a dedicated Automation Testing resource available in the Agile team, then an Automation Test script can be developed in parallel to the development activities. The Automated Test script will fast-track the regression testing prior to each release or every commit in the Continuous Integration / Continuous Deployment model. 

**Tools / Framework:**

Defect tracking tool – JIRA

Automation Testing tool – Selenium

Automation Framework – Serenity BDD

Programming Language - Java

Unit Testing Framework for Test Automation – JUnit

Build Tool – Maven

Schedule and Execution – Jenkins

Automation scripts [browser-based] scripts can be developed in any language and it is not mandatory to use the same technology that the Development team uses.

## User Acceptance Testing (UAT)

UAT is normally conducted by the actual users of that particular system. There will be end-to-end scenarios for the UAT users to execute and verify the system functionalities. In the Waterfall model, UAT will be conducted only at the end, whereas in the Agile world, UAT can be performed at the end of every sprint and feedback given to the team. 

## Usability Testing

**Usability testing** is a technique used in user-centered interaction design to evaluate a product by **testing** it on users. This can be seen as an irreplaceable usability practice, since it gives direct input on how real users use the system. 

## Performance Testing

Software performance testing is used to determine the speed or effectiveness of a computer, network, software program or device. This process can involve quantitative tests done in a lab, such as measuring the response time or the number of MIPS (millions of instructions per second) at which a system functions.
Performance Testing = how fast is the system
Load Testing = how much volume can the system process?

**Tools / Technique**

Gatling or JMeter

## Security Testing

**Security testing** is a **testing** technique to determine if an information system protects data and maintains functionality as intended. It also aims at verifying three basic principles - Confidentiality, Integrity and Authentication.

## Automation Testing 

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

## Test Flows, Test Management & Execution Frequency

[!['Testing in DevOps'][testing5]][testing5]

[!['Testing in DevOps'][testing6]][testing6]

## Sample Automation / Cucumber-BDD-Serenity Test Report

[!['Testing in DevOps'][testing7]][testing7]

## Sample 'Gatling' Performance Test Results 

[!['Testing in DevOps'][testing8]][testing8]

## Proposed Tools & Framework Summary

[!['Testing in DevOps'][testing9]][testing9]

## TL;DR

Considering the multiple iterations in the Agile/DevOps model, **Testing** is one of the most important phases of software delivery and to fast track the testing process, automated functional & non-functional test-scripts are in high demand. In the ideal scenario, each Agile team may have at least one QA resource who ensures the Testing activities for the current sprint as well as taking care of the existing functionalities through the Regression Tests. It is also very clear that Test Automation is not the responsibility of a DevOps engineer whereas he/she will concentrate only on the **Infrastructure Automation** rather than enhance your **codebase**.

  [testing1]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST1.JPG
  [testing2]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST2.JPG
  [testing3]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST3.JPG
  [testing4]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST4.JPG
  [testing5]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST5.JPG
  [testing6]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST6.JPG
  [testing7]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST7.JPG
  [testing8]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST8.JPG
  [testing9]: {{ site.baseurl }}/images/posts/importance-of-software-testing-in-ci-cd/TEST9.JPG

