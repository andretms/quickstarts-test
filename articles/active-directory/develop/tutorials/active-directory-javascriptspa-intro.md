---
title: Azure AD v2 JS SPA Tutorial - Intro | Microsoft Docs
description: How JavaScript SPA applications can call an API that require access tokens by Azure Active Directory v2 endpoint
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: ''

ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity 
ms.date: 10/29/2017
ms.author: andret

---

# JavaScript Single Page Application (SPA) tutorial - Introduction & Setup

This tutorial demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call the Microsoft Graph API or other APIs that require access tokens from the Azure Active Directory v2 endpoint.

<!--start-collapse-->
### Libraries

This guide uses the following library:

|Library|Description|
|---|---|
|[msal.js](https://github.com/AzureAD/microsoft-authentication-library-for-js)|Microsoft Authentication Library for JavaScript Preview|

> [!NOTE]
> *msal.js* targets the *Azure Active Directory v2 endpoint* - which enables personal, school and work accounts to sign in and acquire tokens. The *Azure Active Directory v2 endpoint* has [some limitations](..\active-directory-v2-limitations.md). If you are interested only in school and work accounts, use *adal.js* and the *V1 endpoint*. 
> To understand differences between the v1 and v2 endpoints read the [v1-v2 comparison](..\active-directory-v2-compare.md).

## Setting up your web server or project

## Prerequisites
A local web server such as [Python http.server](https://www.python.org/downloads/), [http-server](https://www.npmjs.com/package/http-server/), [.NET Core](https://www.microsoft.com/net/core), or IIS Express integration with [Visual Studio 2017](https://www.visualstudio.com/downloads/) is required to run this guided setup. 

Instructions in this guide are based on both Python and Visual Studio 2017, but feel free to use any other development environment or Web Server.

## Create your project 

> ### Option 1: Visual Studio 
> If you are using Visual Studio and are creating a new project, follow the steps below to create a new Visual Studio solution:
> 1.	In Visual Studio:  `File` > `New` > `Project`
> 2.	Under `Visual C#\Web`, select `ASP.NET Web Application (.NET Framework)`
> 3.	Name your application and click *OK*
> 4.	Under `New ASP.NET Web Application`, select `Empty`

<p/><!-- -->

> ### Option 2: Python/ other web servers
> Make sure you have installed [Python](https://www.python.org/downloads/), then follow the step below:
> -	Create a folder to host your application.

## What is next

> [!div class="nextstepaction"]
> [1. Sign-In users](active-directory-javascriptspa-sign-in.md)