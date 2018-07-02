---
title: Azure AD v2 JS SPA Quickstart | Microsoft Docs
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
ms.date: 05/09/2018
ms.author: andret

---


# Sign-in users and acquire an access token from a JavaScript application

1. Test block 1

    ```javascript
    var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
        redirectUri: msalconfig.redirectUri
    });
    ```

1. Test Block 2

    ```javascript
    var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
        redirectUri: msalconfig.redirectUri
    });
    ```

1. Test block 3

    ```javascript
    var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
        redirectUri: msalconfig.redirectUri
    });
    var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
        redirectUri: msalconfig.redirectUri
    });

    var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
        redirectUri: msalconfig.redirectUri
    });
    ```

1. Add *OWIN* and *Microsoft.IdentityModel* references to `Startup.cs`:

    ```csharp
    using Microsoft.Owin;
    using Owin;
    using Microsoft.IdentityModel.Protocols.OpenIdConnect;
    using Microsoft.IdentityModel.Tokens;
    using Microsoft.Owin.Security;
    using Microsoft.Owin.Security.Cookies;
    using Microsoft.Owin.Security.OpenIdConnect;
    using Microsoft.Owin.Security.Notifications;
    ```

1. Replace Startup class with the code below:

    ```csharp
    public class Startup
    {
        // The Client ID is used by the application to uniquely identify itself to Azure AD.
        string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

        // RedirectUri is the URL where the user will be redirected to after they sign in.
        string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

        // Tenant is the tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
        static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

        // Authority is the URL for authority, composed by Azure Active Directory v2 endpoint and the tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
        string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

        /// <summary>
        /// Configure OWIN to use OpenIdConnect 
        /// </summary>
        /// <param name="app"></param>
        public void Configuration(IAppBuilder app)
        {
            app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

            app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
                new OpenIdConnectAuthenticationOptions
                {
                    // Sets the ClientId, authority, RedirectUri as obtained from web.config
                    ClientId = clientId,
                    Authority = authority,
                    RedirectUri = redirectUri,
                    // PostLogoutRedirectUri is the page that users will be redirected to after sign-out. In this case, it is using the home page
                    PostLogoutRedirectUri = redirectUri,
                    Scope = OpenIdConnectScope.OpenIdProfile,
                    // ResponseType is set to request the id_token - which contains basic information about the signed-in user
                    ResponseType = OpenIdConnectResponseType.IdToken,
                    // ValidateIssuer set to false to allow personal and work accounts from any organization to sign in to your application
                    // To only allow users from a single organizations, set ValidateIssuer to true and 'tenant' setting in web.config to the tenant name
                    // To allow users from only a list of specific organizations, set ValidateIssuer to true and use ValidIssuers parameter 
                    TokenValidationParameters = new TokenValidationParameters()
                    {
                        ValidateIssuer = false
                    },
                    // OpenIdConnectAuthenticationNotifications configures OWIN to send notification of failed authentications to OnAuthenticationFailed method
                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed
                    }
                }
            );
        }

        /// <summary>
        /// Handle failed authentication requests by redirecting the user to the home page with an error in the query string
        /// </summary>
        /// <param name="context"></param>
        /// <returns></returns>
        private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
        {
            context.HandleResponse();
            context.Response.Redirect("/?errormessage=" + context.Exception.Message);
            return Task.FromResult(0);
        }
    }
    ```

This quickstart contains a code sample that demonstrates how a JavaScript Single Page Application (SPA) can sign in personal, work and school accounts, get an access token, and call the Microsoft Graph API.

![How the sample app generated by this guide works](media/active-directory-javascriptspa/javascriptspa-intro.png)

::: zone render="docs"

## Register your application and download your Quickstart app

You have two options to start your Quickstart application:

### Option 1: Register your application and download your Quickstart app [Express]

1. Go to the [Azure Portal - Application Registration [Prod]](https://portal.azure.com/signin/index/?Microsoft_AAD_RegisteredApps=true#blade/Microsoft_AAD_RegisteredApps/applicationsListBlade/quickStartType/JavascriptSpaQuickstartPage/sourceType/docs)
1. Enter a name for your application and click **Register**
1. Follow the instructions to download and configure your new application, adding **http<span/>://localhost:30662/** as Redirect URL and setting the **Implict Flow** automatically for you.

### Option 2: Register your application and configure sample [Manual]

#### Step 1: Register your application
 
1. To register an application, go to the [Azure Portal - Application Registration [Prod]](https://aka.ms/registeredappsprod) and select **New registration**
1. Enter a name for your application, add **http<span/>://localhost:30662/** in Reply URL, and click **Register**
1. Select **Authentication** menu and set **ID tokens** under *Implict Grant* and select 'Save'
<span/>

::: zone-end


::: zone render="chromeless"

### Step 1: Configure your application in Azure Portal
For the code sample for this quickstart to work, you need to add a reply URL as *http<span/>://localhost:30662/*.
> [!div renderon="portal" id="makechanges" class="nextstepaction"]
> [Make these changes for me]()

> [!div id="appconfigured" class="hidden"]
> ![Already configured](media/active-directory-windesktop/checkmark.png) Your application is configured with these attributes
<span/>

::: zone-end


> [!NOTE]
> If you use Visual Studio, the Redirect URL will be set to to *http:<span/>//localhost:30662/* as it is configured in the code sample's project. If you use Python or any other web server, set redirect URL to *http://<span/>localhost:30662/*, run the following command line:
>> ```bash
>> python -m http.server 30662
>> ```

### Step 2: Download your web server or project

- [Download the Visual Studio project](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/VisualStudio.zip)
- [Download the core project files - for a local web server, such as Python](https://github.com/Azure-Samples/active-directory-javascript-graphapi-v2/archive/core.zip)

### Step 3: Configure your JavaScript SPA

> [!div renderon="docs"]
> Edit `msalconfig.js` and replace `Enter_the_Application_Id_here` with the Application ID your application:

> [!div class="sxs-lookup" renderon="portal"]
> Edit `msalconfig.js` and replace msalconfig with:

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```

## More Information

### *msal.js*

MSAL is the library used to sign in users and request tokens used to access an API protected by Microsoft Azure Active Directory. The Quickstart's *index.html* contains reference to the library:

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/0.1.1/js/msal.min.js"></script>
````

### MSAL initialization

The quickstart code also shows how you how you initialize the library:

```javascript
var userAgentApplication = new Msal.UserAgentApplication(msalconfig.clientID, null, loginCallback, {
    redirectUri: msalconfig.redirectUri
});
```

> |Where  |  |
> |---------|---------|
> |ClientId     |Application Id from the application registered in the Azure Portal|
> |loginCallBack | Name of a callback method called after the authentication|
> |redirectUri     |URL where users are sent after authentication against Azure AD v2 Endpoint|

### Sign-in users

Below how you sign in users:

```javascript
userAgentApplication.loginRedirect(graphAPIScopes);
```

> |Where  |  |
> |---------|---------|
> |graphAPIScopes     | (Optional) Contains scopes being requested at login time (i.e. `{ "user.read" }` for Microsoft Graph or `{ "api://<Application ID>/access_as_user" }` for custom Web APIs)|

> [!TIP]
> Alternativelly you may want to use `loginPopup` method to display a popup window for sign-in the user.

### Requesting tokens

Msal has two methods to used acquire tokens `acquireTokenRedirect` (or `acquireTokenPopup`) and `acquireTokenSilent`:

#### Getting a user token silently

The `acquireTokenSilent` method handles token acquisitions and renewal without any user interaction. After `loginRedirect` (or `loginPopup`) is executed for the first time, `acquireTokenSilent` is the method commonly used to obtain tokens used to access protected resources for subsequent calls - as calls to request or renew tokens are made silently.

```javascript
// Try to acquire the token used to query Graph API silently first:
userAgentApplication.acquireTokenSilent(graphAPIScopes)
```

> |Where  |  |
> |---------|---------|
> |graphAPIScopes     | (Optional) Contains scopes being requested at login time (i.e. `{ "user.read" }` for Microsoft Graph or `{ "api://<Application ID>/access_as_user" }` for custom Web APIs)|

#### Getting a user token interactively

 There are situations however that you need to force users interact with Azure Active Directory v2 endpoint – some examples include:
- Users may need to reenter their credentials because the password has expired
- Your application is requesting access to a resource that the user needs to consent to
- Two factor authentication is required

Calling the *acquireTokenRedirect(scope)* result in redirecting users to the Azure Active Directory v2 endpoint (or *acquireTokenPopup(scope)* result on a popup window) where users need to interact with by either confirming their credentials, giving the consent to the required resource, or completing the two factor authentication.

```javascript
userAgentApplication.acquireTokenRedirect(graphAPIScopes);
```

## What is next

Try out the JavaScript tutorials for a complete step-by-step guide on building applications and building new features, including a full explanation of this Quickstart, and other tutorials, like call Microsoft Graph API, sign-out:

### Learn the steps to create the application for this Quickstart

> [!div class="nextstepaction"]
> [Call Graph API tutorial](../tutorials/active-directory-javascriptspa-call-graph-api.md)

### Learn from tutorials for additional scenarios

> [!div class="nextstepaction"]
> [Call a custom Web API tutorial](../tutorials/active-directory-javascriptspa-call-api.md)

<!--
### Learn other scenarios
> [!div class="nextstepaction"]
> [Sign-Out tutorial](..\tutorials\active-directory-javascriptspa-sign-out.md)
> [Call Graph API tutorial](..\tutorials\active-directory-javascriptspa-call-graph-api.md)
-->

[!INCLUDE [Help and support](../../../../includes/active-directory-develop-help-support-include.md)]
