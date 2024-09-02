---
title: "Automation Best Practices"
date: 2023-09-02T12:31:23-04:00
draft: false
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
    image: "/posts/post-files/internships/automation.jpeg" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
---

I think I have had one of the most interesting years of my life working on automation and testing. I think I have gained a ton of knowledge which I have written about below. 

My experience with automation is based off a year of experience building automation tools in both Java and C# and using different frameworks and features which are used throughout the industry for both test automation and automation of deploying / configuring code.  

I like to think about automation as more than just automated testing. Much of our world can be automated and efficiency gains can be achieved in many areas. Repetitive manual tasks are the first area which can be drastically improved. Like robotics replacing auto workers, the same can be said about automation replacing IT workers. Once automation is made easy, then AI (Artificial Intelligence) models can be easily added and adopted throughout the industry. I do not believe this is negative for the economy, as human work can now be focused on more beneficial areas and used towards actions that are more valuable to organizations.  

During my internships, there was a key focus regarding how automation had yet to catch up to the many advancements done in both developing software and AI. For the past 10-15 years, browser automation for instance has been heavily dominated by Selenium while web frameworks have changed drastically with Angular, React, Vue, and Svelte coming out. Only in the past few years in browser automation has Playwright been considered a strong competitor to Selenium. In addition, the idea of PowerAutomate automating areas with SharePoint has only just begun. Same as how reporting automation with Power BI has only sprung out recently.  

When we look at what an organization can automate, the most glaring area of course is testing automation. Tests are often done manually, and this can be very tedious, unrepeatable, and takes up a lot of time. Automation can save manual testing efforts, especially with repetitive tasks. Testing oftentimes has a lot of repetition especially if validating that a certain build/deployment is working.  

There are two key elements to any type of testing automation: smoke testing and regression testing.  

When looking at automated smoke tests, we want to ensure that our tests verify that the applications work and do not break any functionalities. This is smoke or sanity testing. These tests should be quick and ideally report back results within 10 mins. I was taught that sanity testing should take less than 30 minutes, but ideally it should be as quick as possible. An end-to-end test should be enabled that will check application components are working, and services are up.  

Regression testing on the other hand involves validating functional specifications and ensuring that test cases cover the required expectations of the application. This type of automation works for test cases which are going to be repeated and applications that are going to be static over time.  

I would argue that automation extends beyond testing and includes areas such as CI/CD pipelines for developers. The full automation scale includes:  

1. Developers commit changes. Automatic build kicks in. Ideally the build is parallelized so that it is as quick as possible. If there are multiple parts that need to be built, build them in different pipelines and then publish artifacts. Limit checkout depth to 1, enable build parallelization, and find ways to make the executions quicker. For instance, NuGet restore is slow, so caching makes it quicker. 

2. Unit tests kick in in parallel while building and quickly sanity check that the build is correct.  

3. Integration tests are kicked off immediately after unit tests. Integration tests may involve multiple components and could require the build to successfully complete. For instance, these could be UI tests that check sanity. This may need to come after a deployment to a QA environment is done.  

4. As soon as tests are finished, deploy to the next environment. In a fast-moving company, if unit tests are comprehensive, theoretically one could deploy straight to prod. However, in teams where there are set release cycles, changes can be pushed to a QA team and QA environment. The deployment ideally has no manual intervention so DB flashbacks/refreshes can be done automated, and code deployments automated. In addition, automatic environment monitoring and observability can be done to ensure applications are up. There can be different automated checks that can be run to ensure a successful deployment is completed.  

5. After a successful deployment we can execute end-to-end UI tests which test the core functionalities of the application followed by end-to-end regression tests. These include logins, logouts, saving data, downloading files, generating reports, creating extracts, initializing services, and more. 

6. At some point before the release, full scale regression testing should be done. This can be done as soon as sanity testing is done or afterwards. These tests should be testing comprehensively the requirements from the previous release cycle and the newer requirements for the application. 

7. Infrastructure teams can automate environment observability by running monitoring tools such as Elasticsearch, Dynatrace, or internal reporting.  


In addition, there are other tools out there such as PowerAutomate which allows for direct integration with Microsoft Office products and allows users to avoid having to program their own applications and interact with the Azure Portal services. For instance, automated emails can be sent before releases, work items can be pulled, forms can be automated, and teams messages automated.  

## Summary 

As far as automation is concerned, this is my understanding of what and where automation stands like today in 2024. I do believe that automation is going to be the backbone of any revolution with AI with web applications. There is still a ton left to get down in the industry.  

 