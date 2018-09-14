---
title: Configure NuGet Package Source at the Repo Level
date: 2017-10-16 10:28:55
tags: 
  - NuGet 
  - VisualStudio 
  - CSharp 
---

A long time ago in a galaxy far, far away, we used to configure NuGet package sources at the machine level in Visual Studio.  Each time a new PC was dropped on our desk, we would dutifully go through our Visual Studio configuration steps, including setting up a NuGet package source pointing to our ProGet server.  

Recently we have been able to reduce the amount of configuration needed at the machine level by instead configuring our package source at the repository level.

## NuGet.Config

The packages source configuration is in a nuget.config that gets committed to the repo right beside the .sln.

{% gist b8a39be78f0cb209bd4d4a4450683172 nuget.config %}

You can learn more about nuget.config from the [Microsoft Docs](https://docs.microsoft.com/en-us/nuget/schema/nuget-config-file).
