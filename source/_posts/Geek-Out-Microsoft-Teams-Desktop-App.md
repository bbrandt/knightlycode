---
title: 'Geek Out: Microsoft Teams Desktop App'
tags: 
  - geekout 
  - web 
  - electron 
  - desktop
date: 2017-06-27 01:24:23
---


For anyone else curious about how Microsoft is now developing desktop applications, here's some info on Microsoft Teams:
The Microsoft Teams app is built with Angular, TypeScript, & HTML. This web-based application is then wrapped with the Electron shell just like VSCode.  The desktop client shares the same code as the Microsoft Teams web client.

## How Does This Apply to Me?
Worth noting, here are some potential non-functional requirements of the Teams client that may differ from your needs:
* Cross-platform (Windows, Linux, Mac)
* Share code between desktop and web
* Prove out modern web technologies in a greenfield product
* Cloud backend support

## Edit 8/14/2017
The Visual Studio 2017 installer UI is an electron app as well.

"We’re using Electron for the UI of the setup engine because it gives us the potential of sharing the installer code with other developer tools that ship on multiple platforms." -- [Tim Sneath](https://blogs.msdn.microsoft.com/visualstudio/2016/04/01/faster-leaner-visual-studio-installer/)

## References:
https://blog.thoughtstuff.co.uk/2017/04/under-the-hood-of-the-microsoft-teams-desktop-application/
https://techcommunity.microsoft.com/t5/Microsoft-Teams-Blog/Ask-Microsoft-Anything-Microsoft-Teams-11-10-16/ba-p/30212
