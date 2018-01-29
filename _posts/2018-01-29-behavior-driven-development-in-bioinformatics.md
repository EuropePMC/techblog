---
layout: post
title:  "Behavior-Driven Development in Bioinformatics"
date:   2018-01-29
author: rakesh
category: testing
---

## What is BDD?

**Behavior-Driven Development (BDD)** is a set of Software Engineering practices designed to help teams deliver more valuable and higher quality software features.

It adopts general techniques and principles of [Test Driven Development](https://en.wikipedia.org/wiki/Test-driven_development) (TDD) with ideas from [Domain-driven Design](https://en.wikipedia.org/wiki/Domain-driven_design) (DDD). BDD incrementally builds functionality guided by expected behavior.

A simple BDD scenario / requirement is as follows:
{% highlight java %}
  @TC01_EPMC_SearchTest
  Scenario: Specific Search by Keyword
    Given I am researcher
    When I open the 'Europe PMC' Website
    And Enter the keyword "Glycosyl transferases" on the Query field
    And Click on the Search button
    Then I should be able to see the matching results on the Search Result page
{% endhighlight %}

<!--more-->

## How does BDD work?
[!['BDD Framework'][bdd1]][bdd1]

## Benefits of BDD
* Understandable by both technical and non-technical people
* Business Analysts (BA) and Subject Matter Experts (SME) can contribute BDD scenarios
* Data can be fed along with the scenarios, which can updated any time without any changes in scripting
* Developers can write the scripts in a language of their choice
* Attractive test reports at the end of the execution [HTML and JSON]
* Availability of Continuous Integration tools like Jenkins, Bamboo, etc...
* Single platform for Web, Mobile, API, thick client, and Database Testing

## How BDD fits in an Agile/DevOps environment
[!['BDD Diagram'][bdd2]][bdd2]

After story grooming on the first day of a new sprint, the developer and test teams will agree on frozen acceptance criteria for each user story identified for the sprint. Developers should prepare BDD scenarios as per the acceptance criteria, with the scope being limited to unit-level testing. QA testers or the domain expert will write the functional scenarios for each of the acceptance criteria in the user story. Both Unit and Functional BDD scenarios may or may not contain negative scenarios. Test case design techniques such as [Equivalence Partitioning](https://en.wikipedia.org/wiki/Equivalence_partitioning), [Boundary Value Analysis](https://en.wikipedia.org/wiki/Boundary-value_analysis), and [Decision Tables](https://en.wikipedia.org/wiki/Decision_table) can be applied while writing the BDD scenarios.

As a best practice, BDD functional scenarios should be sent to the BA or SME for sign-off prior to test scripting. Both development and automation test scripting activities can be carried out in parallel, based on agreement with front-end developers, on how the UI elements on the page look and what the element’s characteristics are for the script to act upon.

For instance, assume the agile team is going to work on a user story for the Europe PMC login screen. Both the UI/front-end developer and QA automation team must agree on a unique element locator like `id="login–email"` for the 'Email' field, `id=login–password` for the 'Password' field, etc. (see the figure, below).

Using this technique, the QA team will not have to wait until the development team completes the front-end and back-end development processes to start test scripting. Once the actual build is available for testing, the QA team can run the automated test script and fast track the QA tasks, detecting defects during the early stages of the sprint.

[!['BDD Object Identification'][bdd3]][bdd3]

## 'Magic' behind the scenes?
Developers might wonder how plain English text will trigger test execution. The answer to that question is a tool called [Cucumber](https://cucumber.io/), which is smart enough to parse plain text scenarios. Cucumber will either generate a function skeleton or call the respective function for each step in the given scenario (see below).

### Java Steps:
<!-- !['BDD Java Code'][bdd4] -->
{% highlight java %}
import cucumber.api.PendingException;
import cucumber.api.java.en.Given;
import cucumber.api.java.en.When;
import cucumber.api.java.en.Then;
import cucumber.api.java.en.And;
import cucumber.api.junit.Cucumber;
import org.junit.runner.RunWith;

@RunWith(Cucumber.class)
public class MyStepDefinitions {

    @Given("^I am researcher$")
    public void i_am_researcher() throws Throwable {
        throw new PendingException();
    }

    @When("^I open the 'Europe PMC' Website$")
    public void i_open_the_europe_pmc_website() throws Throwable {
        throw new PendingException();
    }

    @Then("^I should be able to see the matching results on the Search Result page$")
    public void i_should_be_able_to_see_the_matching_results_on_the_search_result_page() throws Throwable {
        throw new PendingException();
    }

    @And("^Enter the keyword \"([^\"]*)\" on the Query field$")
    public void enter_the_keyword_something_on_the_query_field(String strArg1) throws Throwable {
        throw new PendingException();
    }

    @And("^Click on the Search button$")
    public void click_on_the_search_button() throws Throwable {
        throw new PendingException();
    }
}
{% endhighlight %}

### JavaScript Steps: 
{% highlight javascript %}
module.exports = function () {

  this.Given(/^I am researcher$/, function (callback) {
    callback.pending();
  });

  this.When(/^I open the 'Europe PMC' Website$/, function (callback) {
    callback.pending();
  });

  this.Then(/^I should be able to see the matching results on the Search Result page$/, function (callback) {
    callback.pending();
  });

  this.And(/^Enter the keyword \"([^\"]*)\" on the Query field$/, function (glycosyltransferases, callback) {
    callback.pending();
  });

  this.And(/^Click on the Search button$/, function (callback) {
    callback.pending();
  });

};
{% endhighlight %}

### Ruby Steps:
{% highlight ruby %}
Given /^I am researcher$/ do 
    # do something
end

When /^I open the 'Europe PMC' Website$/ do 
    # do something
end

Then /^I should be able to see the matching results on the Search Result page$/ do 
    # do something
end

And /^Enter the keyword \"([^\"]*)\" on the Query field$/ do |glycosyltransferases|
    # do something
end

And /^Click on the Search button$/ do 
    # do something
end
{% endhighlight %}

Once the function skeleton is ready, the script needs to be enhanced according to the step definition using UI automation tools like Selenium, Protractor or Appium as shown below.
{% highlight java %}
    @Given("^I am researcher$")
    public void i_am_researcher() throws Throwable {
        opens_home_page();
        ScenarioHook.getScenario().write("Logged-In User : Scientist");
    }

    @When("^I open the 'Europe PMC' Website$")
    public void i_open_the_Europe_PMC_Website() throws Throwable {
        Assert.assertTrue("ERROR: Home Page NOT available",homePage.verifyHomePageAvailable());
    }

    @When("^Enter the keyword \"([^\"]*)\" on the Query field$")
    public void enter_the_keyword_on_the_Query_field(String keyWord) throws Throwable {
        homePage.enterQueryString(keyWord);
    }

    @When("^Click on the Search button$")
    public void click_on_the_Search_button() throws Throwable {
        homePage.performSearch();
    }

    @Then("^I should be able to see the matching results on the Search Result page$")
    public void i_should_be_able_to_see_the_matching_results_on_the_Search_Result_page() throws Throwable {
        Assert.assertTrue("ERROR: Result Result Page NOT available", resultPage.verifyResultsPanelAvailable());
        printMessage("Successful");
    }
{% endhighlight %}
In the above example, Java is used along with Selenium and jUnit.

### How to parameterize the BDD Test
{% highlight java %}
  @TC_01_SearchTest
  Scenario Outline: Specific Search by Keyword
    Given I am researcher
    When I open the 'Europe PMC' Website
    And Enter the "<SearchKeyWord>" on the Query field
    And Click on the Search button
    Then I should be able to see the matching results on the Search Result page

    Examples:
    | SearchKeyWord         |
    | Cancer                |
    | blood                 |
    | Glycosyl transferases |
{% endhighlight %}

## Reports
By default, Cucumber generates an HTML report, and you can configure a JSON report if you wish. Cucumber-JVM is equipped to convert the JSON report displayed as below in Jenkins using the [Cucumber Reports](https://plugins.jenkins.io/cucumber-reports) plugin.

[!['BDD Cucumber Report'][bdd5]][bdd5]

The [Serenity BDD Framework](http://www.thucydides.info/) (a popular Java based open source framework), when used for the BDD implementation, will provide an enhanced report, as shown below.

[!['BDD Serenity Report1'][bdd6]][bdd6]
[!['BDD Serenity Report2'][bdd7]][bdd7]
It is also smart enough to capture a screenshot according to user settings.

## TL;DR
**Behavior-Driven Development (BDD)** is emerged from test-driven software development process that is becoming popular and widely used by Europe PMC and by many organizations, due to its transparency, and the readability of the application behaviour.

### Useful links:
* [Cucumber](https://cucumber.io/)
* [Serenity](http://www.thucydides.info/)
 

  [bdd1]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd1.JPG
  [bdd2]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd2.JPG
  [bdd3]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd3.JPG
  [bdd4]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd4.JPG
  [bdd5]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd5.JPG
  [bdd6]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd6.JPG
  [bdd7]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd7.JPG