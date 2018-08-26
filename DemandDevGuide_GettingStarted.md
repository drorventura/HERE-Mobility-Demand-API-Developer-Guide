# HERE Demand API: Getting Started #

## Getting Here Mobility Account and Credentials ##

To create your account at Here mobility [email the Here support team](mailto:mobility_developers@here.com) and provide your full name and email address.

You'll receive an initial password and verification email to your mailbox.
At a later stage, you'll be able to manage your account via our Here mobility developer portal.

To obtain application user credentials for the Demand API, [email the Here support team](mailto:mobility_developers@here.com) and specify the following:

-   Your application name
-   A URL for a web application or a package/store ID for a mobile app

You will receive: 

-   An application key 
-   An application secret value

Here is an example of what the application key and secret values look like:  


```{"applicationKey": "Casd9nS4WUs90***cCvsurYgtpLEgm8", "applicationSecret": "QcVyN7Wq3HNqWN3DEAI0H***mibtsdUkJ_8zS0skrRHfZyzKbW0gmvjSKgnLt"}```

>**Note**: For security reasons, the **applicationSecret** value must not be exposed to the end user. Store he **applicationSecret** value in your server-side code and not in your client-side code. If any abuse of the **applicationSecret** is detected, your credentials will be revoked.

## Authenticating Application Users ##

For security reasons, when you access the Here Mobility Demand API on behalf of your users, you will need to sign in with their username and with the Demand API App Key and App Secret values.

### Getting a Client-to-Service (C2S) Token ###

When calling the Client-to-Service (C2S) API, the best practice is for your backend server to sign in to the Demand API when the user logs in, and send the signed hash value to the app. The app should then pass the hash value to the Demand API. See the REST call in the following example:

```GET accounts.v1/application/c2s/token?application_key=<application_key>&user_id=<user_id>&expiration=<expiration>&hash=<hash>```

>**Notes**:
>-   The **application_key** and **user_id** values are plain strings (not converted to Base64 as when providing them to the hash function)
>-   The **expiration** value determines when the authentication token expires (in seconds, since Epoch).

### Getting a Service-to-Service (S2S) Token ###

Here is an example of how to create a Service-to-Service (S2S) token:

```GET accounts.v1/application/s2s/token?application_key=<application_key>&&application_secret=<application_secret>```

### Sandbox and Production Environments ###

You can use the HERE Mobility Sandbox platform to develop and test your app's functionality without calling the production platform. Requests to the sandbox environment are ephemeral (do not affect the "real world").

The HERE Mobility service directs your app's calls to the sandbox or to the production environment, according to the API key you provide.