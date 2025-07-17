## Concept of Graph, API and Postman tool as well as their set up in Azure
### Summary:

  - Postman is a tool for testing APIs
  - Mirosoft Graph is an API providing access to Microsoft 365 data
  - API is a general term for the communication interface between different systems or applications

Together, Postman can be used to interact with APIs like Microsoft Graph to fetch and manipulate data.


#### <u> Postman </u>:
  - Postman is a popular API development tool used to test, develop, and document APIs. It provides a user-friendly interface where developers can send HTTP requests to web services, test responses, and analyze API performance.
  - Postman is commonly used to simulate client requests, get access tokens for authentication, and manage APIs without writing code.

#### <u> Microsoft Graph </u>:

  - Microsoft Graph is a RESTful API that provides access to Microsoft 365 services and data (such as Office 365, Azure AD, OneDrive, Outlook, Teams, and more) via a single endpoint (https://graph.microsoft.com).
  - It allows developers to integrate Microsoft services into their apps, retrieve user data, manage organizational directories, send emails, access calendar events, etc.
  - Graph API supports delegated permissions (user-level access) and application permissions (app-level access).

#### <u> API (Application Programming Interface) </u>:
  - APIs are commonly used in web development to enable applications (like web or mobile apps) to communicate with back-end services, databases, or other external systems.



### To register an app in Azure Active Directory (Azure AD) and use Postman to get delegated rights for a user, follow these steps:


#### Step 1: Register an App in Azure AD
* Log in to the Azure Portal:
* Go to https://portal.azure.com and sign in with an account that has the necessary permissions to create app registrations.
* Navigate to Azure AD:
* On the left-hand menu open manage
* Create a New App Registration
* Select App registrations > New registration
* Provide a name for your app (e.g., “Postman API”)
* Choose the supported account type : Accounts in this organizational directory only
* For Redirect URL, select Public Client/Native and enter a placeholder value as https://oauth.pstmn.io/v1/callback if using Postman, or configure it as needed later.
* Click Register
* Configure API Permissions:
  * After registering the app, go to the app’s API permissions section. 
  * Click Add a permission, select Microsoft Graph, and then select the appropriate permissions:
  * For delegated permissions (acting on behalf of the user), select permissions: 
    * Group.Read.All 
    * User.Read.All
    * Directory.Read.All
* Once permissions are added, click Grant admin consent to grant these permissions for all users in the tenant
* Go to Authentication section
  * Click Add Platform
  * Click Web
  * Add URL : https: //login.microsoftonline.com/ Azure Tenant ID /oauth2/v2.0/token
* Generate a Client Secret:
>[!NOTE]  
>Copy the client secret immediately after creation since you won’t be able to view it later
* In the app, go to Manage->Certificates & secrets, New Client secret 
  - Provide a description and expiration (6 months) and then click Add.

#### Step 2: Use Postman to Get an Access Token

* Open Postman:
* Download and open Postman (if you haven’t already).
* To update an environment in Postman, follow these steps:
  * Open the Environment Settings:
  * In the Postman application, locate the environment tab at the top-right corner to open the Manage Environments dialog.
  * Click Add to create a new environment
  * Give your environment a name e.g. “Microsoft Graph”, so it’s easy to identify when switching between environments
* Define Environment Variables:
  * In the new environment, you’ll see three columns: Variable, Initial Value and Current Value.
  * In the Variable column, type the names of the variables you want to use : 
    * client_id
    * client_secret
    * base_url and 
    * tenant_id
>[!NOTE]  
> - Masked Variables: Postman allows hiding sensitive values like client_secret so they don’t appear in logs or screenshots.
> - Prevents Accidental Sharing: If you store credentials inside the request body instead of variables, they might be accidentally shared if someone exports the collection.
  * In the Initial Value and Current Value columns, enter the corresponding values for each variable obtained from Azure tenant for the app that has just been registered.
  * <i> Initial Value: The default value you want to set </i>
  * <i> Current Value: This is what Postman uses in the current session, allowing for temporary updates. </i>
* Save the Environment:
    * After adding all required variables, click Save to store your new environment.
* Use the Environment in Requests:  
  * Go to the Environment dropdown at the top right of the Postman window and select your newly created environment (Microsoft Graph) from the dropdown to make it active for your requests.  
* Create a New Request:
  - In Postman, create a new request to get the OAuth 2.0 token by clicking on the + icon.
  - Go to Authorization tab, set Auth Type : OAuth 2.0 
  - Header Prefix : Bearer
  - Grant type : Authorization Code
  - Call Back URL : https:// login.microsoftonline.com/Azure Tenant ID/oauth2/v2.0/token
  - Client ID : Select variable - {{client_id}}
  - Client Secret : Select variable - {{client_secret}}
  - Scope : https://graph.microsoft.com/User.Read.All
* Get an Access Token:
  * Click Get New Access Token at the bottom. This will direct you to the Azure login page. Sign in using ID/password and authenticator. 
  * Once authenticated, Postman will store the access token.
  * By clicking on "Use Token" one can now use this token to make authenticated requests on behalf of the user with the delegated permissions.

#### Step 3: Use Access Token in Postman Requests
  - Once the token is generated, you can add it to the Authorization header of your API requests in Postman.
  - Test as follows:
    * Go to collections in left pane in postman
    * Click on Applications -> Users -> Get users
    * Click on Authorization tab: 
      * Select Auth Type: Bearer Token
      * Token : Copy paste the access token we just generated in previous step  
      * Click on "send" button up top right which should generate a result at the bottom extracting info. of the users in the tenant


### Summary:

* App Registration in Azure AD sets up the app, assigns the necessary API permissions, and generates credentials like the client secret.
* Postman is used to request OAuth tokens, and the access token can be used in subsequent API requests for delegated rights.
* Think about Public Client/Native in Azure like having a special pass for certain apps that can’t keep secrets.
* When you register an app in Azure and pick Public Client/Native, you’re telling Azure, “This is an app that can’t keep secrets, so let’s make it easier for it to access things safely without needing a hidden key.”
With Public Client/Native, your app can get permission to do things like access files or information securely by just proving its identity. This way, apps like Postman, which isn’t meant to store secret codes, can still get permission to connect safely and work as needed.


