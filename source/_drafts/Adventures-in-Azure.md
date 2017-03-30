## Adventures in Azure

The software development work I've done thus far that I get paid for has all been deployed on-premise or packaged up and shipped to customers that run on-prem, so any fun cloud experimentation has to be on my own time.  This week I decided to take a look at building simple API's in Azure. More specifically, what would be involved in building an API that I could securly make available on the internet and bill for usage.  

The first thing I looked into was Azure Functions.  If you haven't heard of it Azure Functions is a simple way to deploy code to Azure and have it run and scaled without having to think about the hardward it will run on or care about VM provisioning.  The code can be triggered by messages in an incoming queue, from a GitHub Webhook, or, what I am interested in currently, by an HTTP request.  Code can be written in C#, F#, Node.js, Python, PHP, Powershell, batch, or bash.  Related buzzwords are Function as a Service (FaaS) and serverless.

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

For some reason I felt too cool for the online code editor for Azure Functions, however nice it may be.  I opted to use the VS2015 preview tooling and setup my code with continuous deployment from GitHub.  This experience was much more seamless than I expected.

The only real roadblock I hit that stumped my for a few minutes is that the tooling creates a directory structure that is not compatible with deployment to Azure Functions.  Fortunately, [the documentation](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference#folder-structure) nicely states that all Azure Function code must be in a subfolder directly beneath the root folder.

Developing the code localy in VS2015 gives you the ability to set breakpoints and debug code when necessary.

Feel free to [fork my repo](https://github.com/bbrandt/AzureAddFunction) and try it for yourself.