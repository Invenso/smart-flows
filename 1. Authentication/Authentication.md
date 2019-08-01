# Authentication

To start using the api, you need to be authenticated. There are 2 ways to get authenticated:
1. Use API keys
2. Use JWT token

### API keys
Use the Project console to generate an API key:
- Go to your project
- Go to "Control panel"
- Go to "Users"
- Click your user or select and edit
- Go to API keys
- Generate API key - copy it and store it somewhere safe

This key can be used for every following API request by adding it as a custom header: "X-API-Key: your-api-key".
You should revoke this key (remove it from your user) if you think it is compromised. Thereafter the API key 
will be invalid.
---
### JWT tokens
Why should you should use JWT tokens in your application? API keys are so easy to use.

Start using JWT tokens when you want multiple users to use the application. This way, your project 
stays clear. Because this means every flow which has been ran, every template which has been created,... 
has parameters which reference the user who has created or modified the item. It is also safer than api keys.

#### How to use?
##### GET /api/v1/authenticate
<table>
<tr><th>Response body</th><th>Description</th></tr>
<tr><td>login.enabled</td><td> Whether username/password login is supported.</td></tr>
<tr><td>methods</td><td> show the list of methods which are allowed to log in.</td></tr>
<tr><td>oauth2</td><td> if there are Oauth methods supported, this contains more info about them.</td></tr>
<tr><td>resetPasswordSupported</td><td> Whether reset password is supported</td></tr>
</table>

##### POST /api/v1/authenticate

Send a body with username, password & loginContext. LoginContext can be derived from GET /api/v1/authenticate.
Returns a token which can be used in future requests by the header: "Authorization: Bearer your-jwt-token". This 
token will expire after a while (configured per server). If this happens, you can ask another token.

##### POST /api/v1/oauth2

First, create an url based on the oauth2 method returned by GET /api/v1/authenticate. This should be a GET 
formed by oauth2.url with oauth2.parameters as query parameters. Go to it and log in with the Oauth provider. 
The return url query parameter should be your own, which can handle the response query parameters. Send the 
responseParams to this endpoint to receive a JWT token.


---
### Extras in the authentication API
This contains the functionality to reset the password. SMTP configuration should be done server side so mails can be send.


##### POST /api/v1/authorizeReset
Ask to reset the password for a certain user.
##### POST /api/v1/authorizeReset
<table>
<tr><th>Request body</th><th>Description</th></tr>
<tr><td>username</td><td> The name for the user for which you want to reset the password.</td>
<tr><td>path</td><td> Will send an email to the emailaddress of the the user with a link to the Project Console or the Flow 
Execution Panel. This only supports the relative links "/project" & "/client".</td>
</table>

##### POST /api/v1/reset
Do the actual reset password for the user.
<table>
<tr><th>Request body</th><th>Description</th></tr>
<tr><td>password</td><td>The new password for the user</td>
<tr><td>resetToken</td><td>The token is appended to the url in the email</td>
<tr><td>userId</td><td>The id is appended to the url in the email</td>
</table>
