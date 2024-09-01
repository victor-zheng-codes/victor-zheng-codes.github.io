---
title: "Internship at the Ministry of Education 2023"
date: 2024-07-01T16:14:00-04:00
draft: true
author: "Victor Zheng"
showToc: true
tags: ["internships"]
categories: ["intern"]
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
    image: "/posts/post-files/internships/ddsb-csc-victor.jpeg" # image path/url    
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: false # only hide on current single page
editPost:
    URL: "https://github.com/victor-zheng-codes/Personal-Website/tree/main/content"
    Text: "Suggest Changes" # edit text
    appendFilePath: true # to append file path to Edit link
---

From May 2023 to December 2023, I interned at the Community Services Cluster (CSC) of GovTechON in the Government of Ontario. As my first internship experience, I thought the overall experience was excellent and it sparked my curiosity into a lot more than what I had originally signed up for. 

The official mission of the OPS is “taking pride in strengthening Ontario, its places and its people” and I thought this was a great chance for me to be involved in shaping the future of Ontario. 

Here is my reflection on my time there.

----

## Introduction
I joined the CSC in a Software QA / automation role on the Regression Team in the Summer of 2023. I had just finished my second year at the University of Toronto’s Computer Science program. The Cluster is like an internal consultant company of the Government with the Ministries being the clients. My branch (Data Collection and Decision Support Solutions, aka DDSB) was responsible for data collection of mainly the Ministry of Education and Ministry of Colleges and Universities. The data included data on items such as program funding, school year systems, calendars, library systems, program administration, student information, program outlines, capital funding, grants, experience programs, and enrolment information. 

The systems in essence are the core foundations of any education system worldwide. My team was responsible for the regression of a Candidate Release and before being handed over to the Operations teams. 

As I progressed through my work and experience at the CSC, I was able to get my hands on a lot of very interesting projects and tools. It was also a very exciting time as many major migration projects were underway or started while I was interning.

## Migration Projects
For instance, one of the first areas I learned about was Team Foundation Server which is an archaic way of doing version control. Essentially, we had folders which stored the versioning of code and changes were merged into one Main branch after being released into production. While there, I was involved with projects migrating to Azure DevOps and initializing Git version control strategies. 

I also gained experience using a system called Microfocus ALM (aka HP ALM and now OpenText ALM), which is an Application Lifecycle Management tool like Jira or Azure DevOps (more on this later). However, the main drawback that I found was that the ALM was that it does not have ability to link code changes with work items and is very slow and clumsy to use. It’s not configurable as code (VBA only) and was being run on our own on-premises infrastructure. This meant that to even launch the program, you needed to install special software, generate licenses, and run the right operating system. During my time on the team, I saw us transition towards Azure DevOps which is similar to GitHub.

At the same time, teams were also moving away from SharePoint on-premises server to the new SharePoint Online system. The entire backbone of SharePoint is via a server which hosts all the documentation and information which is internal to government teams. The migration saw a lot of our data moved from the on-prem server to the new one which is cloud hosted and supported by Microsoft.

Finally, we were also in the transition to Azure Active Directory which was later renamed Entra ID. Essentially this login foundation is based on the concept that applications can be logged into via the login credentials that you use for Microsoft Office, Teams, and eventually Windows 11 operating systems. It's the backbone of Microsoft's single-sign-on infrastructure that the Government is also trying to adapt to. We also had a legacy authentication mechanism which involved passwords as well which saw a small migration as well.

While at the DDSB, I was able to experience and work on projects that migrated us towards the future. It was satisfying to be a part of projects that I knew would help Ontarian's.

|![](/posts/post-files/internships/government-view.jpg?raw=true)|
| :--: |
| <b>I had the opportunity to visit the Government of Ontario legislative assembly.</b>|


## Cloud Computing and DevOps
I think there’s a lot out here that I have yet to touch and Cloud computing, and cloud architecture is one of the major ones. In particular, I learned the term virtualization (creating a simulated, or virtual, computing environment as opposed to a physical environment) but never really had a chance to experiment on how we can apply virtualization. I think it’s a shift in thinking which is slowly making its way to the government as well. A lot of the programs and projects are meant for on-premises environments and are not really ready for cloud adoption. It was refreshing to see some progress in this regard though. 

DevOps development is quite different than the traditional methods which still are prevalent in the government. A lot of teams have pseudo-Agile delivery with Waterfall still being the major driver of projects. Big tech companies launch their products multiple times a day but that hasn’t yet been achieved. The first step though is to speed up development times and that’s something which I was very interested in working on.

## Government Philosophy
Regarding government speed, I think it is one of the items that a lot is talked about. There's this misconception that all government employees have it easy and don't do much.

Generally though, at the Ontario government, everyone is different and everyone is trying their best to improve how we operate at the government. There isn’t really an answer to how best to achieve these goals. 

To me, the philosophy of government work revolves around Work-Life-Balance. Employees want to have work-life-balance above everything else. It's important to have a life outside of work and to also feel valued doing the work at the same time.

The people in government are quite diverse but I would argue no different than any other organization. From my experience, there are some very highly intelligent people at every organization. Change management isn’t done through a spiritual leader or through CEO all hands meetings every day. 

Effective management is super important, and I think it’s more important to have good leaders than a high-paying job.

Leadership philosophy depends on the teams, but I think it is generally as follows: set achievable expectations, stick the course, and be transparent. People lead by having auditable and traceable requirements and they listen to their employees and team members to build towards a constructive result. Timelines and deadlines are quite different per team as well but I think it’s no different than any other company. 

Artificial Intelligence adaptability was discussed a lot with my mentor and manager. The government is neither shying away nor jumping on the bandwagon. At least while I was there, there were a few discussions on AI and working groups on it. 

Unions and job security is about stabilization. If there are big changes that employees are unhappy about, the union will fight for them. While I was there, unionized employees worked with management without problems. I did learn that there is a separate union for managers though. 

Contractors and pay scales are quite interesting. Apparently, contractors are paid much more than the average and that the rates are quite high. I met a lot of contractors at the government. You don’t get some of the benefits, but the pay is much higher. 

Generally, while I was there, it was a push towards leanness. I think teams are only slightly dependent on the Provincial leader and the party that is running the government.  Government leaders drive the vision, and the OPS tries to implement that vision. We are non-partisan though. Office perks are few because budgets don’t account for this type of thing. In addition, there must be someone who signs off on the spending and tallies receipts before getting them signed off. 

## What I learned

My main project was working on migrating the testing framework to Azure DevOps and configuring our framework to work for new scenarios to match the ongoing migration projects. More information is available on my separate post about it. 

I learned a ton about agents, on-premises applications, deployment strategies, building pipelines, branching strategies, and automation scripts. 

This project brought me into how to use C#, and how to write good code, but also a few interesting things about C#. Such as how to version files, the .NET framework, .NET Core, NuGet packages, project dependencies, and how .NET will be developed in the future. For instance, I now know that .NET 6.0 is the future long-term stable release of .NET, and that .NET framework is still very useful but different. I also learned about valuable skills in project versioning and releasing programs to production users. 

I also learned a ton about testing strategies and best practices. How we can strategically go about solving problems by thinking them through. I learned about AODA testing, UI testing, and end-to-end testing. I spent the majority of my time working on how to interact and work with Azure DevOps.

I worked on API requests and built our framework to be able to read and report results back to Azure DevOps. The framework was able to handle batched requests, and work with any number of users. Batching requests was important as sending one request was going to be very slow. I then realized that we could use Azure’s client libraries instead and batch requests inherently. From there, I went on to add DevOps reporting integrations from Excel to allow auditing and reporting of automated test exeuctions to DevOps.

By the time I was done with with the Azure DevOps migration, my 8-months had come up and it was time to move on.

As I left the CSC, I realized that there are a lot still out there for me to learn. This includes infrastructure work such as servers, databases, and enterprise application development.

## Conclusion
Overall, though, the experiences you gain from working in a place where you can see your changes go into production is something that I think I was looking for. Here, small and sometimes large efficiency gains are easy to envision whereas at a larger company it would be much harder. Here, your work is valued, and I think that’s something that is under appreciated. 

I am now on my second internship at the Ministry of Education working on the infrastructure team. I’m looking forward to contributing and learning more about the awesome world of technology with this great team! 

|![](/posts/post-files/internships/government-floor.jpg?raw=true)|
| :--: |
| <b>I had the opportunity to visit the Government of Ontario legislative assembly. Here is me on the floor of the assembly.</b>|