---
title: "Testing Automation Framework"
date: 2024-09-02T12:31:16-04:00
draft: true
author: "Victor Zheng"
showToc: true
tags: [""]
categories: [""]
TocOpen: false
hidemeta: false
comments: false
description: ""
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
cover:
    image: "/posts/post-files/internships/test-automation-view.png" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
---

# Test Automation Framework

The Test Automation Program was one of the main projects that I worked on while at the Ministry of Education of the Government of Ontario.

The code is open-source and is a comprehensive, end-to-end testing framework for UI testing and reporting. The original developers had a multi-repo model which I combined into a mono-repo to enable easier versioning, feature enhancements, and documentation.

The full, open-source framework is available here: [github.com/zzzrst/AutomationTestingProgram](https://github.com/zzzrst/AutomationTestingProgram).

All thoughts are my own and I have redacted any personal information and team information. The main goal for all my blogs is to provide a personal reflection of different years of my life.

## Background

The framework is Keyword Driven, with Selenium 4.0 running in the background and abstractions made to make it executable with test steps defined in Excel or Oracle. The thinking for making test step definitions defined in Excel is that it allows for the ease of sending the file via email, and for the non-technical team members to use the framework for testing. The need to understand how the scripting is done is abstracted and so PM or someone with no technical knowledge can still generate and understand tests. See my section below on BDD for some thoughts on this though.

The framework interacts with the Oracle DB or Excel test cases before parsing the results into Test Step, Test Suites, and Test Sets using the builder design pattern. Each Test Suite is built, then Test Cases are added to the Test Suite, and then Test Steps are added to the Test Case. When we execute the tests, we start from the Test Steps and report results to the Test Case, which in turn reports back to the Test Suite. The framework would read the ALM Test Suite and Test Case definitions, query the Oracle DB within one table for the test step ordering, and then execute the test via C#. Before reporting results to ALM or any other testing reporting platform.

The framework also allows for a Traceability Matrix to be used to map requirements for testing. Traceability is usually done in an Excel file and mapped directly to test cases and steps which can be in a separate tab in the same Excel.

When I first joined the team at the Ministry of Education, we were working with an Oracle Database which stored our test cases alongside Micro Focus’ ALM project management platform. As in all companies, migration projects are always underway.

We were moving to Microsoft’s SharePoint Online from on-prem SharePoint and to Azure DevOps from Microsoft TFS. With Azure DevOps, work items would be logged into DevOps and manual tests would also no longer be done in ALM.

Therefore, there was a necessary need to investigate how we could migrate our tests to Azure DevOps and get results published to Azure DevOps instead of simply ALM. The quest began to build this new framework.

## Why Azure DevOps

Microsoft Azure is the future, and it enables continuous integration and continuous delivery, which will speed up product delivery, and bring development to production timelines faster. The barrier between development and operations teams will drastically decrease and we can more quickly iterate to build better products. Using TFS, we would never be able to say we are Agile as we would always be waiting for gates to be approved and deployments to be manually executed.

Micro Focus’ ALM is an on-prem server, which is hard to use, difficult to configure, and filled with buttons which we will never need to use and are hard to understand. It runs very slowly, does not store build/deployment information, and does not have a linkage between code and executions. It also does not allow us to link test cases to different builds, so we are not 100% sure that the tests we are executing are in the right environments. Setting up ALM itself requires a ton of configuring and downloading archaic software from the web.

When we use Azure DevOps (like Jira), we can directly see the linkage between defects and code changes. It also has many integrations with popular products directly from its marketplace. It has task groups available, and agent pools for deployment. It is Team Foundation Server but much more modern and with Git. The main benefit, however, is that it is on the cloud and accessible with any web browser. This means that simply accessing defects does not take a few minutes and logging issues can be quick and simple. It is a modern approach to software development.

## Why I took up the project

At first, I wanted to understand how ALM communicated with Oracle and how the Selenium running in the background worked. However, I also noticed that our methodologies were lacking some major items such as version control, ease of updating, and the ability to see the big picture. I also had major questions about how to update the framework to fit the needs of QA teams. For instance, I remember asking how we could update browser versions or add new features to execute scripts against an Oracle DB. In addition, the need to interact with a database using SQL is not easy. Looking at a table in a database does not give you information on what is being run. One month into my internship, I landed on the migration project and some initial source-code of a framework which was discussed 5 years ago. The blueprint was there, but the framework still was not finished. The framework needed major tune-ups and fixing so that it would be usable with the modern-day approaches.

How I managed the project

Personally, I excel in ambiguous projects which require careful thinking, strategizing, and planning to achieve. However, the main problem with ambiguity is that there is not always a clear idea of what needs to be done. My manager and my team decided to first discuss the requirements for the migration project in a holistic view. We defined what our main objectives were at the very start:

- Have ability to execute tests in Excel instead of Oracle and remove the dependencies on the Oracle DB
- Have better reporting of test cases to Azure DevOps, send emails, and be able to provide good graphs of results
- Configurations for features available to be configurable as code. Easy ability to turn on and off features.

As I began the project, I discussed daily enhancements with the team and developed the framework slowly but surely. I listed all our advancements and features on Azure DevOps and tracked over 400 work items prioritizing high priority items to 1 and lower ones to 4. I also included latest ideas as things to “Investigate” such as integrations with other common tools.

|![](/posts/post-files/internships/RunResults.png)|
| :--: |
| <b>Run results of executions.</b>|

## Technical Problems

### Importing Oracle Database Data into a Viewable Format

When we look at an Oracle Database table, it is just like any relational database. The data is stored on one table, but you cannot get one list of everything ordered correctly. So, if we simply exported the table from SQL Developer it would be thousands of lines of unordered test steps. We wanted to be able to extract and then immediately run the tests directly from the XML, TXT, CSV, or Excel that it was extracted into.

The problem with XML and TXT is that it is not configurable per column. We wanted to be able to interact with columns and update columns quickly.

This led us to believe that Excel running an .xlsx or .csv was the right choice. We also wanted to add triggers for validations of columns just like how we had in Oracle.

We also found that some of our values in the Oracle had commas built in, so exporting it may cause issues with the tests. We could overwrite the values, but we also knew that some validations required the checks of commas. The benefit of CSV would be that we would be able to perform proper version control on the values as they were in plaintext.

In the end, we started with the idea of moving all the test definitions to Excel by building a program to grab test case steps and test suite steps from ALM, creating excel binaries using an Excel library, querying Oracle using client libraries for the test steps and then inputting the data into Excel. I called this the ALM Migrator.

For ease of users of the ALM Migrator, I built the framework and added it to a network drive. Then modified the VBA scripts in ALM to add a button that we execute the framework from the network drive to report results into the local user’s C drive.

### Reading Excel Data

The next problem I faced was in reading excel test data. There was a builder model in the framework outline which did not include implementations for Excel. Since our framework outline had been published into NuGet packages which were segregated, I decided to download our binaries and rebuild them locally. This is the idea of a mono repo.

I ran a debugger and turned off Just My Code which allowed me to understand what was causing issues with the framework. Eventually I got the framework to read the Test Suite named by the excel name, read the Test Cases within the Excel, and then read the Test Steps inside excel. I finally was able to make the framework work by just reading, but executing was still a big question mark.

### Executing Data

As I began trying to run our Testing Driver, I was perplexed. How does our framework interact with the browsers, what are chrome drivers? Definitions of implicit vs explicit waits, how many attempts, timeouts, Selenium drivers, compilation modes, and what are AODA (Accessibility for Ontarians with Disabilities Act) drivers.

In addition, took a long time to understand how our frameworks’ action on objects were interacting with the Selenium Driver and the Chrome Drivers which we installed. Figuring out how the drivers worked was the biggest learning curve.

Slowly but surely though I was able to make the Automation program build and run.

### Functionality Development

For developing features, I focused on making feature flags available to end users. This enables us to create unique features so that if something breaks, the framework itself will still work. Some features I added were the abilities to report test results to DevOps, report results to Micro Focus ALM, report results to CSV, run AODA reports, highlight elements, enable VNC video, enable PDF reports, enable emailed reports, and to report to Report Portal. If one day one of the features stops working, all the QA team needs to do is turn off the feature in app.config.

### Unit Tests

I put a lot of emphasis on building good unit tests and expanding our code coverage for the unit tests. When we have high coverage, we can be more confident that the framework is doing its job. Writing good unit tests allows us to be able to make more releases and iterate at a faster rate.

### Authorization and Authentication

For authorization and authentication, I worked on support for three main methods. The first method was through an Excel file for storing credentials. The second method was through hard coded values, and the third method was through Azure Key Vault. The mechanisms for all three allow any QA team to operate efficiently and allow for any project team to use the framework.

### Azure DevOps

For Azure DevOps, I worked extensively with the Azure DevOps Test Management API and SDK to report test results to DevOps. I sent API requests to check for Test Plan, Test Case, Test Step, and Test Run existences in DevOps. If any of those did not exist, then I would create another request to create them. Finally, I would combine everything into a Test Run involving Azure Test Points to generate a test instance. The execution involves running test steps, reporting results to the test case, running the next test case until none exists, then reporting results to the test set. This idea of building separately and running separately is the backbone of the test automation framework that we developed.

### Results Reporting

Result reporting was a huge challenge at first in Azure DevOps. There was always duplication of Test Case and Test Plan details, and the results were not clear. I worked on making the results more aligned and preventing duplication of results. I ran into batching issues which is when REST API is overloading. I overcame this by using client libraries instead of APIs which enabled batching requests. I also enabled async functionalities where possible.

I worked on email reporting and designing robust copies of execution results via email. I created an HTML template for results reporting which would be filled out at the end of the execution. Then I created two copies of the HTML: one that could be embedded in an email (static html) and one which could have embedded JavaScript for viewing results in an accordion.

### Deployment of Code

This took a long time to understand. Initially, I packaged the framework and threw it into a network drive. I also created a self-extracting zip file and msi files for users to navigate through. I created bash scripts, power shell scripts, and other scheduled scripts to execute tests. I also created excels with embedded VBA to execute tests. At some point I also created a C# windows application that would allow users to interact with the executable.

However, this turned out to be hard to use and difficult to view central results. I eventually landed on the benefits of using the Azure pipelines and agent pools to deploy the code to on-prem machines. My manager and I managed to install agents on all our on-prem machines and then deploy the latest framework to those machines. I investigated publishing NuGet packages and creating binaries for users to use. I also investigated the possibilities of creating Artifacts in DevOps and sending them to users.

I spent a lot of time developing pipelines and creating parallel executions available in Azure DevOps. I played around with Deployment Pools, Agent Pools, and Azure Pipelines quite a bit to figure out how to deploy the testing framework to users.

The idea that I landed on was to deploy the framework’s-built code to self-hosted agents on QA servers, then reference that path on a different pipeline’s executable. If the latest framework is deployed to the right folder, we will not have to worry about deploying the framework manually.

### Documentation

I started a markdown readme format for documentation. I enabled our wiki to have documentation which could be referenced and sent to all teams. I created mechanisms for users to report bugs in the framework and for users to fix bugs. I wrote documentation on how users can create Work Items and then how to triage them. I also created some KT videos, ran KT sessions, and interacted with QA teams for requirements gathering.

### Data Files

I worked converting Oracle Database tables into Excel, but I also worked with XML and JSON interpretations of the framework. The problem with non-column centered formats was that it was hard to interact with the tests. For Excel based test steps, it is easy to delete, add, and remove test steps.

### SQL Enhancements

I worked on SQL enhancements so that applications could be restarted at their initial states. I worked on developing scripts that reset states to Open or Input from Closed or Submitted states. This avoided having to run DB refreshes and allowed tests to start from the same initial state every time.

### Parameterization

I wanted to enable parameterization of testing so that tests could be executed with minor changes but still work. Especially with the format of our tests where a year could change a lot of tests, it was imperative that users could easily change the year with a parameter. I also wanted to enable uniqueness of tests so provided a default unique value which could be used for each test execution.

### Browsers

I investigated browser issues such as driver issues. I investigated updating test binaries from chromium to chrome for testing to the default browsers installed. I spent a lot of effort into determining how to isolate browsers and enable execution isolation and environment segregation. I wanted to avoid flaky tests and enable automation results to be more robust.

### Packaging

For packaging, I first looked at how we could manage packaging through zip files. Then zip files are shared through a network drive. Then through Azure DevOps artifacts. Then through git. And then finally through Azure DevOps Agents.

### Why BDD is Something That I Endorse More

Behavior Driven Development (BDD) is an especially important discussion in 2024. The Keyword Driven model is, to be honest, difficult to map requirements and hard for QAs to understand the WHY as tests are created. At the end of the day, QA testing should be focused on what the actual users will experience and NOT on what the application is behaving.

If I were to rewrite the framework, I would have thought about doing BDD with Playwright instead of spending hours working on fixing a program which did Keyword Driven Testing.

### Playwright

I worked with another colleague on running a Playwright POC and testing out how to integrate Playwright with our framework. Overall, we enabled Playwright with our framework. However, I do believe that Playwright could even be usable out of the box without additional configurations. If I were to re-start automation efforts, I would combine Playwright and BDD into a new framework.


## Summary

Overall, this project was an incredibly fun project which allowed me to experience developing working software from start to finish. During the project, I learned everything from writing reusable software, building, and deploying software, getting requirements and feedback, and creating new features.
