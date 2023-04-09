# BDD - Behaviour-Driven Development

What is BDD?
============

BDD is a way for software teams to work that closes the gap between business people and technical people by:

*   Encouraging collaboration across roles to build shared understanding of the problem to be solved
*   Working in rapid, small iterations to increase feedback and the flow of value
*   Producing system documentation that is automatically checked against the system’s behaviour

BDD and agile
-------------

We assume that your team are using some kind of agile methodology already, planning work in small increments of value like [User Stories](https://cucumber.io/docs/terms/user-story/). BDD does not replace your existing agile process, it enhances it.

Think of BDD as a set of plugins for your existing process that will make your team more able to deliver on the promises of agile: timely, reliable releases of working software that meets your organisation’s evolving needs, requiring some maintenance effort and discipline.

Three practices
===============

Essentially, day-to-day BDD activity is a three-step, iterative process:

1.  First, take a small upcoming change to the system – a [User Story](https://cucumber.io/docs/terms/user-story/) – and talk about concrete examples of the new functionality to explore, discover and agree on the details of what’s expected to be done.
2.  Next, document those examples in a way that can be automated, and check for agreement.
3.  Finally, implement the behaviour described by each documented example, starting with an automated test to guide the development of the code.

The idea is to make each change small and iterate rapidly, moving back up a level each time you need more information. Each time you automate and implement a new example, you’ve added something valuable to your system, and you’re ready to respond to feedback.

We call these practices _Discovery_, _Formulation_, and _Automation_.

  

*   _Discovery_
*   _Formulation_
*   _Automation_

  

Over time, the documented examples become an asset that enables your team to continue confidently and rapidly making changes to the system. The code reflects the documentation, and the documentation reflects the team’s shared understanding of the problem domain. This shared understanding is constantly evolving.

  

![](https://t6616188.p.clickup-attachments.com/t6616188/dfb8677b-7ad3-4da8-b433-a1cf984b49b9/Screenshot%20from%202022-12-25%2014-24-09.png)

  

Discovery: What it _could_ do
-----------------------------

> The hardest single part of building a software system is deciding precisely what to build.  
> – Fred Brooks, The mythical man-month

Although documentation and automated tests are produced by a BDD team, you can think of them as nice side-effects. The real goal is valuable, working software, and the fastest way to get there is through conversations between the people who are involved in imagining and delivering that software.

BDD helps teams to have the right conversations at the right time so you minimise the amount of time spent in meetings and maximising the amount of valuable code you produce.

We use structured conversations, called [discovery workshops](https://cucumber.io/docs/bdd/discovery-workshop/), that focus around real-world examples of the system from the users' perspective. These conversations grow our team’s shared understanding of the needs of our users, of the rules that govern how the system should function, and of the scope of what needs to be done.

It may also reveal gaps in our understanding, where we need more information before we know what to do.

The scrutiny of a discovery session often reveals low-priority functionality that can be deferred from the scope of a user story, helping the team to work in smaller increments, improving their flow.

If you’re new to BDD, discovery is the right place to start.

You won’t get much joy from the other two practices until you’ve mastered discovery.

Formulation: What it _should_ do
--------------------------------

As soon as we have identified at least one valuable example from our discovery sessions, we can now formulate each example as structured documentation. This gives us a quick way to confirm that we really do have a shared understanding of what to build.

In contrast to traditional documentation, we use [a medium that can be read by both humans and computers](https://cucumber.io/docs/gherkin), so that:

*   We can get feedback from the whole team about our shared vision of what we’re building.
*   We’ll be able to automate these examples to guide our development of the implementation.

By writing this executable specification collaboratively, we establish a shared language for talking about the system. This helps us to use problem-domain terminology all the way down into the code.

Automation: What it _actually does_
-----------------------------------

Now that we have our executable specification, we can use it to guide our development of the implementation.

Taking one example at a time, we automate it by connecting it to the system as a test. The test fails because we have not implemented the behaviour it describes yet. Now we develop the implementation code, using [lower-level examples of the behaviour of internal system components](https://anarchycreek.com/2009/05/20/theyre-called-microtests/) to guide us as required.

The automated examples work like guide-rails, helping us to keep our development work on track.

When we need to come back and maintain the system later, the automated examples will help us to understand what the system is currently doing, and to make changes safely without unintentionally breaking anything.

This rapid, repeatable feedback reduces the burden of manual regression testing, freeing people up to do more interesting work, like exploratory testing.

Who Does What?
==============

Who should be writing [Gherkin](https://cucumber.io/docs/gherkin/) documents, and who should write [step definitions](https://cucumber.io/docs/cucumber/step-definitions)?

Product owners, business analysts, programmers and testers are often confused about who should take on what responsibilities.

The answer depends on several factors, such as team structure, skills, culture, process and more.

The Three Amigos
================

_The Three Amigos_ is a meeting that takes user stories and turns them into clean, thorough Gherkin scenarios. It involves three voices (at least):

*   **The product owner** - This person is most concerned with the scope of the application. This involves translating user stories into a series of features. As the tester comes up with edge cases, the product owner is responsible for deciding what is within scope.
*   **The tester** - This person will be generating lots of Scenarios, and lots of edge cases. How will the application break? What user stories have we not accounted for within these Features?
*   **The developer** - This person will add many of the Steps to the Scenarios, and think of the details that go into each requirement. How will this application execute? What are some of the roadblocks or requirements behind the scenes?

These conversations can produce great tests, because each amigo sees the product from a different perspective. For this reason it is _essential_ that all of these roles have conversations to discover examples _together_. [Example Mapping](https://cucumber.io/docs/bdd/example-mapping) and Event Storming are great collaborative analysis techniques for discovering examples.

Finally, there is no reason to limit these meetings to three people—or to hold only one such meeting at the beginning of the project. Continually refine your features and collaborate with everyone to best understand how to talk about, develop, and test your application.

Writing Gherkin
===============

To start with, when the language and style used in the scenarios is still being established, it is recommended that the entire team collaborate on writing the Gherkin. Later, it can be efficiently done by a pair: a developer (or someone who is responsible for the automation) and a tester (or someone who is responsible for quality) as long as their output is actively reviewed by the product owner (or business representative).

There are several ways to make your Gherkin better.

Describe behaviour
==================

Your scenarios should describe the intended behaviour of the system, not the implementation. In other words, it should describe _what_, not _how_.

For example, for an authentication Scenario, you should write:

```gherkin
When "Bob" logs in
```

instead of:

```gherkin
  Given I visit "/login"
  When I enter "Bob" in the "user name" field
    And I enter "tester" in the "password" field
    And I press the "login" button
  Then I should see the "welcome" page
```

The first example, **When “Bob” logs in**, is a _functional requirement_. The second, much longer, example is a _procedural reference_. Functional requirements are features, but procedures belong in the implementation details.

That way, when the implementation of a feature changes, you’ll only need to change the process steps behind the scenes. The behaviour does not have to change just because the implementation does. In fact, a good question to ask yourself when writing a feature clause is: “Will this wording need to change if the implementation does?”.

If the answer is “Yes”, then you should rework it avoiding implementation specific details. As a side benefit, in consequence your scenarios will be a lot shorter and much easier to follow and understand.

Consider a more declarative style
=================================

One way to make scenarios easier to maintain and less brittle is to use a declarative style. Declarative style describes the behaviour of the application, rather than the implementation details. Declarative scenarios read better as “living documentation”. A declarative style helps you focus on the value that the customer is getting, rather than the keystrokes they will use.

Imperative tests communicate details, and in some contexts this style of test is appropriate. On the other hand, because they are so closely tied to the mechanics of the current UI, they often require more work to maintain. Any time the implementation changes, the tests need to be updated too.

Here’s an example of a feature in an imperative style:

```gherkin
Feature: Subscribers see different articles based on their subscription level 

Scenario: Free subscribers see only the free articles
  Given users with a free subscription can access "FreeArticle1" but not "PaidArticle1" 
  When I type "freeFrieda@example.com" in the email field
  And I type "validPassword123" in the password field
  And I press the "Submit" button
  Then I see "FreeArticle1" on the home page
  And I do not see "PaidArticle1" on the home page

Scenario: Subscriber with a paid subscription can access "FreeArticle1" and "PaidArticle1"
  Given I am on the login page
  When I type "paidPattya@example.com" in the email field
  And I type "validPassword123" in the password field
  And I press the "Submit" button
  Then I see "FreeArticle1" and "PaidArticle1" on the home page  
```

Each step is a precise instruction. The inputs and expected results are specified exactly. But it’s easy to imagine changes to the application which would require changing these tests. The available options for free versus paid subscriptions can change. Even the means of logging in could change. What if, in the future, users log in with a voice interface or a thumbprint?

A more declarative style hides the details of how the application’s capabilities are implemented.

```gherkin
Feature: Subscribers see different articles based on their subscription level
 
Scenario: Free subscribers see only the free articles
  Given Free Frieda has a free subscription
  When Free Frieda logs in with her valid credentials
  Then she sees a Free article

Scenario: Subscriber with a paid subscription can access both free and paid articles
  Given Paid Patty has a basic-level paid subscription
  When Paid Patty logs in with her valid credentials
  Then she sees a Free article and a Paid article
```

With a declarative style, each step communicates an idea, but the exact values aren’t specified. The details of _how_ the user interacts with the system, such as which specific articles are free or paid, and the subscription level of different test users, are specified in the step definitions (the automation code that interacts with the system). The subscription packages could change in the future. The business could change what content is available to subscribers on free and paid plans, without having to change this scenario and other scenarios that use the same step definitions. If another subscription level is added later, it’s easy to add a scenario for that. By avoiding terms like “click a button” that suggest implementation, the scenario is more resilient to implementation details of the UI. The intent of the scenario remains the same, even if the implementation changes later. In addition, having too many implementation details in a scenario, makes it harder to understand the intended behaviour it illustrates.

  

Writing Features
================

Cucumber tests are written in terms of “Features”. Each feature consists of one or more “Scenarios”.

Let’s start with an example Feature file:

```plain
Feature: Explaining Cucumber
  In order to gain an understanding of the Cucumber testing system
  As a non-programmer
  I want to have an overview of Cucumber that is understandable by non-geeks

  Scenario: A worker seeks an overview of Cucumber
    Given I have a coworker who knows a lot about Cucumber
    When I ask my coworker to give an overview of how Cucumber works
    And I listen to their explanation
    Then I should have a basic understanding of Cucumber
```

  

Note that the scenarios do not go into the details of what the software (or, in this case, the coworker) will do. It stays focused on the perspective of the person the Feature is intended to serve (in this case, “a non-programmer”).

Every feature file has a single feature description at the top, but can have any number of scenarios.

The `Feature` line names the feature. This should be a short label.

`In order to` presents the reason/justification for having the feature. In general, this should match to one of the project’s core purposes or “business values” such as:

*   Protect revenue
*   Increase revenue
*   Manage cost
*   Increase brand value
*   Make the product remarkable
*   Provide more value to your customers

`As a` describes the role of the people/users being served by the feature.

`I want` is a one sentence explanation of what the Feature is expected to do.

So, those three lines cover Why, Who, and What. Then, the document gets into the “How” with scenarios.

  

Scenarios
=========

You can have any number of scenarios for a feature.

If you have lots and lots of scenarios in one feature, you might actually be describing _more_ than one feature. When that happens, we recommend splitting up the document into separate Feature definitions (The definition of “lots and lots” here is subjective, and it’s up to you to determine when it’s time to split up a feature).

The first line provides a short description of what the scenario is intended to cover. If you can’t describe your scenario in a single sentence (and not a run-on sentence), then it’s probably trying to cover too much, and should be split into multiple scenarios.

That is followed by some combination of “Steps”—lines that begin with the keywords `Given`, `When`, and `Then` (typically in that order).

You can have many lines that use the same keyword (e.g., `Given there is something` followed by `Given I have another thing`). To increase the readability, you can substitute the keywords `And` or `But` (e.g., `Given there is something` followed by `And I have another thing`).

In general, any `Given` step line should describe only one thing. If you have words like “and” in the middle of a step, you are probably describing more than one step, and should split it into multiple steps.

  

For example:

```gherkin
	When I fill in the "Name" field and the "Address" field
```

Becomes:

  

```gherkin
	When I fill in the "Name" field
	And I fill in the "Address" field
```

  

Cucumber features are best served by consistency. Don’t say the same thing in different ways — say it the same way every time.

For example:

```gherkin
	Given I am logged in
```

and

```gherkin
	Given I have logged in to the site
```

have identical meaning, so it’s better to pick one and use the same line in every Scenario where you need to be logged in.

  

Myths about BDD
===============

  

Myth: You can pick and choose the practices in any order
========================================================

Here’s [Liz Keogh’s take](https://lizkeogh.com/2014/01/22/using-bdd-with-legacy-systems/) on this:

> having conversations is more important than capturing conversations is more important than automating conversations.

Unless you’ve already done effective discovery work, trying to formulate scenarios is a waste of time.

Similarly, you can’t automate examples when you haven’t done the work to figure out the most important examples to automate, or got your business stakeholder’s feedback in how to word them.

Myth: You can automate scenarios after the code is implemented
==============================================================

Many people use Cucumber to do test automation, to check for bugs after the code has already been implemented. That’s a perfectly reasonable way to do test automation, but it’s not BDD.

Myth: Discovery doesn’t need a conversation
===========================================

We see plenty of teams who try to leave the work of identifying examples and turning them into formulated scenarios to a single individual on the team.

That’s not BDD. Discovery work needs to be done _collaboratively_, bringing together representatives of the different specialists who all need to share understanding about what will be built.

Myth: Using Cucumber means you’re doing BDD
===========================================

Just because you’re using Cucumber, doesn’t mean you’re doing BDD. [There’s much more to BDD than using Cucumber](https://cucumber.io/docs/bdd).

  

Localisation
============

```plain
  "fa": {
    "and": [
      "* ",
      "و "
    ],
    "background": [
      "زمینه"
    ],
    "but": [
      "* ",
      "اما "
    ],
    "examples": [
      "نمونه ها"
    ],
    "feature": [
      "وِیژگی"
    ],
    "given": [
      "* ",
      "با فرض "
    ],
    "name": "Persian",
    "native": "فارسی",
    "rule": [
      "Rule"
    ],
    "scenario": [
      "مثال",
      "سناریو"
    ],
    "scenarioOutline": [
      "الگوی سناریو"
    ],
    "then": [
      "* ",
      "آنگاه "
    ],
    "when": [
      "* ",
      "هنگامی "
    ]
  },
```