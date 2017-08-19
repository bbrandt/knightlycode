---
title: Fail Fast - Publishing NUnit Tests in Jenkins
date: 2017-08-18 09:20:20
tags: 
 - jenkins
 - nunit 
 - soft skills
---
# The Problem
We’ve run into a couple of cases where at some point Jenkins silently stopped reporting test results and we did not notice the failure for quite some time, because the failure was not failing the Jenkins build.

# The Solution
When configuring Jenkins to `Publish an NUnit test result report`, ensure that you enable to `Fail the build if no test results are present`.


In the `Publish an NUnit test result report` task of your Jenkins job config, click Advanced:

![](/images/jenkins-publish-nunit-advanced.jpg)

Enabled `Fail the build if no test results are present`:
 
![](/images/jenkins-publish-nunit-fail.jpg)
 
# The Why
Why do I want to fail the build?
In 2004, Jim Shore published a paper in IEEE Software titled, [Fail Fast](https://martinfowler.com/ieeeSoftware/failFast.pdf) that explains the reasoning quite well.  In short, we would like to know immediately if there is a problem, even if its slightly inconvenient.  Bugs in the build or our code are like confrontation you read about in all those self-help books.  The longer you put it off, the more difficult it becomes to resolve.  Better to get it out in the open and resolve it quickly than to let it linger!

So, go resolve some conflicts in your personal life and fail fast in software! It may be difficult at first, but the alternative is much worse.
