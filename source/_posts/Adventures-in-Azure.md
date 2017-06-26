---
title: 'Adventures in Azure: Adding in Azure Functions'
tags: azure cloud
date: 2017-03-30 06:40:12
---

## Adventures in Azure

What would it take to publish a simple Web API in Azure? More specifically, what would be involved in building an Web API providing a service that I could securely make available on the internet and bill for usage?

[Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-overview) is a simple way to deploy a small piece of code to Azure and have it run and scaled without having to think about the hardware it will run on or care about VM provisioning.  The code can be triggered by messages in an incoming queue, from a GitHub WebHook, or, what I am interested in currently, by an HTTP request.  Code can be written in C#, F#, Node.js, Python, PHP, Powershell, batch, or bash.

I know that I need a low number of endpoints to my simple API, so Azure Functions seems like an easy way to get things going as long as all my dependencies can be supported in the sandbox in which Azure Functions runs.  The price also seems to be write, with the first 1 million requests included free each month.  I am a frugal fellow, so free is one of my favorite words.  There are additional constraints on [Resource consumption](https://azure.microsoft.com/en-us/pricing/details/functions/), but this all seems reasonable at the moment.

So, I set out on testing the solution.  A simple Add function will suffice for the test. My API endpoint will be a `GET` request with parameters a and b that get added to produce a result.  The request looks something like this:

```
https://{my site}.azurewebsites.net/api/CalcAdd?a=4.5&b=37.9
```

For this example I would expect a JSON response body like so:

```
{
  "operation": "Add",
  "a": 4.5,
  "b": 37.9,
  "result": 42.4
}
```

Instead of using the online code editor for Azure Functions, I opted to use the [VS2015 preview tooling](https://blogs.msdn.microsoft.com/webdev/2016/12/01/visual-studio-tools-for-azure-functions/) and setup my code with [continuous deployment from GitHub](https://docs.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment).  This experience was much more seamless than I expected.

A single async static method serves as the entry point for the Azure Function.
{% gist 117a6512f4f241280e3bb9007bf94b10 run.csx %}

The inputs are parsed as query parameters. An anonymous type is constructed on line 25 to form the response.

The only real roadblock I hit that stumped me for a few minutes is that the preview tooling creates a directory structure that is not compatible with deployment to Azure Functions.  Fortunately, [the documentation](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference#folder-structure) nicely states that all Azure Function code must be in a sub-folder directly beneath the root folder.

Developing the code locally in VS2015 gives you the ability to set breakpoints and debug code when necessary.

Feel free to [fork my repo](https://github.com/bbrandt/AzureAddFunction) and try it for yourself.

Up next: Azure API Management

### Update 05/07/2017

It [looks like](https://github.com/Azure/Azure-Functions/issues/201) the VS2017 tooling for Azure Functions is being timed to release at the start of the [Microsoft Build](https://build.microsoft.com/) conference.