---
title: 'IMHO: Working With Git Mono Repositories'
description: 'A dive into the world of Git mono repositories.'
author: 'Darius Weber'
date: 2024-05-05
image: /blog/git-mono-repositories/thumbnail.jpg
tags:
    - imho
    - git
    - git-scm
    - version control
    - github
layout: 'single'
socialShare: false
---

This post delves into my experience working with mono repositories in Git.

## What Do I Mean By "Mono Repository"?

In general, a mono repository (monorepo) in Git houses all of a company or organization's projects and libraries in a single repository, as opposed to multiple individual repositories for each project or library. However, in this context, it also describes repositories storing all code belonging to one project, even if it contains multiple applications. For example, an ordinary client-server application consisting of at least one server and one client. Often, they share some code or resources or use the same programming language, but that's not mandatory. To make developers' lives easier, everything is stored in the same place where everything is accessible without any effort.

## What Are The Benefits?

Below is a list of benefits most people bring up in this discussion, and they are true. But every effect has a (negative) side effect!

- **Consistency and Collaboration:** All projects and libraries are in one place, facilitating collaboration and consistency between them. Developers can more easily access code in other parts and make changes. Everyone has access to these resources, making it much easier to share knowledge and reuse code.
- **Easier Dependency Management:** In a mono repo, dependencies between projects and libraries can be easily managed since they exist in the same repository. This can reduce dependency problems that may occur when using separate repositories. For example, you do not need to perform any kind of release to extend libraries and use the new functions.
- **Refactoring and Code Reuse:** Centralized management of all code means that refactoring can be carried out more easily, as changes in one part of the code can be easily applied to other parts. The reuse of code is also made easier.
- **Simpler Build and Deployment Processes:** The build and deployment process can be simplified as all components are in the same repository. This can help reduce inconsistencies in builds and deployments.

## What Are The Drawbacks?

Besides the benefits, there are some drawbacks.

- **Size:** A mono repo can quickly become large, especially in organizations with many projects and libraries. This can lead to longer synchronization and change tracking processes, as well as increased memory requirements.
- **Complexity:** Managing a mono repo may require more complex tooling and workflows compared to separate repositories. This can increase the learning curve for new developers and overall administrative burden.
- **Version Control and Access Control:** In a mono repo, it can be more difficult to implement granular access controls and version control, especially when different teams are working on different parts of the code.
- **Performance:** The performance of commands such as syncing, merging, and tracking changes can be affected in a large mono repo, especially if network bandwidth is limited or the infrastructure of the centralized server is not optimized for large repositories.

## What About Git And Mono Repos?

In general, Git isn't good at working with large repositories - by large, I mean repositories with more than half a million files.  
For example, when you run `$ git status`, Git scans every file belonging to the repository for changes. This is very expensive, especially on systems with a slow file system, such as Windows.

But 'Windows' is a good keyword!  
Microsoft bought GitHub on June 4th, 2018, and started using Git for developing Windows in early 2017.
At this point, their repository had approximately 3.5 million files, resulting in a repository of about 300 gigabytes in size. By mid-2017, 4,000 developers were producing 1,760 daily "lab builds" across 440 branches, plus thousands of pull request validation builds.  
And for these stats, it is rightly called the biggest Git repository!

But I said that Git doesn't work well with large repositories, and this is a very large one. How can Microsoft develop Windows effectively with Git?  
The answer is simple: they extended Git!

They introduced some features focused on improving Git performance.  
One of them is the Git Virtual File System (GVFS). GVFS, together with a set of other enhancements to Git, virtualizes both the .git folder and the working directory. Rather than downloading the entire repo and checking out all the files, it dynamically downloads only the portions you need based on what you use.  
Another feature is the File System Monitor (FSMonitor). Enabling this feature improves the performance of some main commands, such as `$ git add` and `$ git status`. It is a service running in the background and continuously checks the work tree for changes. 

If you're interested in Microsoft's success story (or better, "we improve Git to work with large repositories" story), you can read it in their [developers blog][ms-devblog].

## What Are My Complaints?

So... today Git can work very well with the largest repositories on earth. Everything should be fine, and the remaining issues are of an organizational nature - which can be solved easily!

Maybe...

### Remaining Drawbacks  

First, let's tackle the drawbacks and why some of them are showstoppers!

- **Size, Performance, and Version Control:** They are mostly solved, thanks to Microsoft! There are some edge cases that still cause trouble, but I expect that they will be resolved in the next few years and are not showstoppers. The biggest issue will be that developers may not notice the enhancements and therefore may not use them.
- **Access Control:** Git itself does not handle access control. Tools like GitHub and GitLab add this layer on top of the repository level, so it's still an issue for organizations where some developers are only allowed to access (or even read) some parts of the code.
- **Complexity:** Due to the enhancements for large repositories, handling has become better, but it still requires much more specialized tooling. Often, this must be developed in-house. By extending Git, Microsoft developed their own tooling but published it to the community.

### The Problems With The Benefits

You may have already noticed: I am critical of the benefits!

In my experience, some of the benefits are the results of laziness and lack of time.
But first, where do I agree?

- **Collaboration and Code Reuse:** Yes, mono repos promote collaboration! They give everyone access to every part of the code. You can search for problems already solved by others, even if they are working on different projects, and you may never have heard of them. It ensures that people take on more responsibility and makes transparent what the organization is currently working on. I love it!
- **Consistency and Refactoring:** It ensures that code is (mostly) always compatible, and you don't get bothered by version management. That's nice.

But I have two main complaints with mono repos.  

First, even if I recognize that dependency management is easier, it also causes developers not to think about dependencies. They create links between projects and libraries, which sometimes result in circular dependencies or unexpected links that may include problematic dependencies. Solving these issues costs time and effort, which can be simply avoided by checking the context of included code. In my experience, that's often skipped or ignored.  
Dedicated repositories can solve the issue by defining code that can be used throughout the organization or only in a certain project. But it also reduces communication across teams and lets developers reinvent the wheel.

My second complaint is about tooling, build and deployment processes, and the administrative burden.
Organizations require individual tooling. Often this starts with a proper repository manager. Platforms like GitHub and GitLab don't have mono repos in mind when providing their service.  
Defining pipelines is often much more complex. You only want to clone the part of the mono repo belonging to your project, but you also need code from foreign paths to get the dependencies. Then you often have to optimize them for acceptable performance. And so on...  
One look at the necessary tooling often makes me cry. The responsibility for them lies with the senior developer who is involved in almost every project and has no time to maintain all the tools he has developed. In other words: no one is responsible or knows how to maintain these tools. They also try to solve all possible problems at once instead of using and defining standards.  
Maybe this is a syndrome of every organization, but I notice it to a much larger extent in companies using mono repos.

## So, What Do I Recommend?

Use them if you like! But be aware of the benefits and drawbacks.  
Currently, many organizations are switching to or introducing mono repos for good reasons.  
Maybe it's only a trend, maybe not.

For me, it's important that you make a conscious decision and don't be afraid of challenging your decision.  
Like I said, every effect has a (negative) side effect!


[ms-devblog]: https://devblogs.microsoft.com/bharry/the-largest-git-repo-on-the-planet/
