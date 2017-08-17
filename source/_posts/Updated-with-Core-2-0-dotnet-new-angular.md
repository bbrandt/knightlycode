---
title: 'Updated with ASP.NET Core 2.0: dotnet new angular'
tags:
  - csharp
  - dotnetcore
  - aspnetcore
  - angular
date: 2017-08-16 23:26:12
---


Back in February 2017, Jeffrey T. Fritz blogged about [Building Single Page Applications on ASP.NET Core with JavaScriptServices](https://blogs.msdn.microsoft.com/webdev/2017/02/14/building-single-page-applications-on-asp-net-core-with-javascriptservices/), introducing how to get started with a Angular + ASP.NET Core application.  With the release of ASP.NET Core 2.0 there are some changes to this workflow.

For one, the `Microsoft.AspNetCore.SpaTemplates` is shipped with ASP.NET Core 2.0 [#948](https://github.com/aspnet/JavaScriptServices/issues/948) and does not need to be installed separately.  Once you've installed ASP.NET Core 2.0, you can simply get started with your new project like so:

Create a new project:
```
mkdir mynewproject
cd mynewproject
dotnet new angular
```

Restore packages:
```
dotnet restore 
npm install
```

Set environment to Development:
```
setx ASPNETCORE_ENVIRONMENT "Development"
```

Start your dev server:
```
dotnet run
```

By default the server starts on port 5000, so browse to http://localhost:5000 to see the output.  At this point you have a running ASP.NET Core 2.0 server application with an Angular/Bootstrap frontend.  Ready for innovation!


## What Else Is New?

Doing a compare folders produced from a clean `dotnet new angular` from ASP.NET Core 2 preview 2 and ASP.NET Core 2 RTM reveals a number of dependencies have received minor updates, including Angular which has been updated to 4.2.5.  Some work has also been done to make dev builds faster and fix a couple minor issues.

Happy coding!