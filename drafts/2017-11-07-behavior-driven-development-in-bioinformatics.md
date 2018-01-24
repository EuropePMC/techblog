---
layout: post
title:  "Behavior-Driven Development in Bioinformatics"
date:   2017-11-07
author: rakesh
categories: testing
---

## What is BDD?

<b>Behavior-Driven Development (BDD)</b> is a set of Software Engineering practices designed to help teams deliver more valuable and high-quality software features.

It adopts general techniques and principles of <b>Test Driven Development [TDD]</b> with ideas from domain-driven design. BDD incrementally builds functionality guided by the expected behavior.

A simple BDD scenario / requirement is as follows:
{% highlight html %}
  @TC01_EPMC_SearchTest
  Scenario: Specific Search by Keyword
    Given I am researcher
    When I open the 'Europe PMC' Website
    And Enter the keyword "Glycosyl transferases" on the Query field
    And Click on the Search button
    Then I should be able to see the matching results on the Search Result page
{% endhighlight %}

## How does BDD work?
!['BDD Framework'][bdd1]

## Benefits of BDD
<ul style="line-height:95%">
<li>Understandable by both Technical & Non-Technical people</li>
<li>Business Analyst (BA) /Subject Matter Expert (SME) can contribute while creating BDD scenarios</li>
<li>Data can be fed along with the scenarios, which can updated any time without any changes in scripting</li>
<li>Developers can write the scripts in a language of their choice</li>
<li>Attractive Test reports at the end of the execution [HTML and JSON]</li>
<li>Availability of easy and Continuous Integration tools like Jenkins, Bamboo, etc...</li>
<li>Single platform for Web, Mobile, API, Thick client & Database Testing</li>
</ul>

## How BDD fits in Agile/DevOps environment
!['BDD Diagram'][bdd2]

After Story grooming on the first day of the Sprint both the Developer & Test teams will have the frozen Acceptance Criteria for each User Story identified for the current sprint. Developer(s) should prepare BDD scenarios as per the acceptance criteria with the scope being limited to unit level testing. Further QA or the domain expert will write the functional scenarios for each of the acceptance criteria in the user story. Both Unit and Functional BDD scenarios may or may not contain negative scenarios. All the Test case design techniques like Equivalent Partitioning, Boundary Value Analysis, and Decision Table can be applied while writing the BDD scenarios.

As a best practice, BDD functional scenarios should be sent to the BA or SME for sign-off prior to the Test Scripting. Both Development and automation test scripting activities can be carried out in parallel based on the agreement with the front-end developers, on how the UI elements on the page look like and what the element’s characteristics are for the script to act upon.

For instance, assume the agile team is going to work on a user story for the Europe PMC Login screen. Both the UI/front-end developer and QA Automation team must agree up on unique element locator like id=<i>’ login–email ’</i> for the ‘ Email ’ field, id=<i>’ login–password ’</i> for the ‘Password’ field etc. shown as below as in the below figure.

Using this technique, the QA team will not have to wait until the development team completes the front-end and back-end development processes to start test scripting. Once the actual build is available for Testing, the QA team can run the automated test script and fast tract the QA tasks and detect the defects during the early stages of the Sprint.

!['BDD Object Identification'][bdd3]

## ‘Magic’ behind the scenes?
You might wonder how the plain English text will trigger the Test execution. The answer to that question is the ‘Cucumber’ tool as it is smart enough to parse the plain text scenarios. Cucumber will either generate a function skeleton or call the respective function for each step in the given scenario (see below).

<strong> Java Steps: </strong>
<!-- !['BDD Java Code'][bdd4] -->
{% highlight html %}
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

<strong> JavaScript Steps: </strong>
{% highlight html %}
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

<strong> Ruby Steps: </strong>
{% highlight html %}
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
{% highlight html %}
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
In the above example, Java programming language is used along with Selenium and jUnit.

## How to parameterize the BDD Test?
{% highlight html %}
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

By default Cucumber, generates the HTML report and you can configure the JSON report if you wish. Cucumber-JVM is equipped to convert the JSON report displayed as below in Jenkins using the <b>Cucumber Reports</b> plugin.

!['BDD Cucumber Report'][bdd5]

The <b>Serenity BDD Framework</b>, (popular Java based open source framework) used for the BDD implementation, will provide the enhanced report, as shown below.

!['BDD Serenity Report1'][bdd6]
!['BDD Serenity Report2'][bdd7]
It is also smart enough to capture the screenshot according to the user settings.

## Conclusion
<b>BDD</b> become popular and widely used by many big companies due to its transparency and readability of the application behaviour.

## References
<a href="https://cucumber.io/">https://cucumber.io/</a><br>
<a href="http://www.thucydides.info/#/">http://www.thucydides.info/#/</a>
 

  [bdd1]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd1.JPG
  [bdd2]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd2.JPG
  [bdd3]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd3.JPG
  [bdd4]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd4.JPG
  [bdd5]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd5.JPG
  [bdd6]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd6.JPG
  [bdd7]: {{ site.baseurl }}/images/posts/behavior-driven-development-in-bioinformatics/bdd7.JPG