---
title: Azure AD v2 JS SPA Guided Setup - Query Graph | Microsoft Docs
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
ms.date: 06/01/2017
ms.author: andret

---

# JavaScript Single Page Application (SPA) tutorial - Sign-out

This tutorial demonstrates how a JavaScript Single Page Application (SPA) can sign out a user after user has signed-in.

## Before you start
Before you start with this tutorial, you should have an understanding of the following tutorials:

> [!div class="checklist"]
> * [Intro & Setup](active-directory-javascriptspa-intro.md) 
> * [Register an app](active-directory-javascriptspa-register-app.md) 
> * [Sign-In](active-directory-javascriptspa-register-app.md) 

You can skip some of the tutorials above using the download option:

## Download

If you prefer to download the project for this tutorial, you have complete two steps:

### First step: Download the code sample

<table>
<tr>
<td>
<h4>Option 1: Download the pre-requisites</h4>
Download the pre-requisites for this tutorial, then complete the steps for this tutorials to finish it:
<ul>
<li>
[Visual Studion 2017 project: Sign-In](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip) <br/> - or - 
</li><li>
[Python: Sign-In](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip)
</li>
</ul>
</td>
<td>
<h4>Option 2: Download the complete sample</h4>
Download the complete sample, which includes the code for this tutorial:

<ul>
<li>
[Visual Studion 2017 project: Sign-out](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip) <br/> - or - 
</li><li>
[Python: Sign-out](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip)
</li>
</ul>
</td>
</table>

### Second Step: Configure the sample

Register an application and configure the code sample:

* [Register an app](active-directory-javascriptspa-register-app.md) 

## Sign-out the user

Add the following code to your `app.js` file:

[!code-javascript[main](../../../../active-directory-javascript-graphapi-v2/JavaScriptSPA/app.js?name=signout "app.js")]

### More Information

After a user clicks the *‘Sign-out’* button, he will sign-out etcetera, etcetera...

## What is next

Now that you signed in a user, select one of the options below to proceed:

> [!div class="nextstepaction"]
> [Call the Microsoft Graph API](active-directory-javascriptspa-sign-in.md)