# HERE Demand API: Getting Started #

## Getting HERE Mobility Account and Credentials ##

To create your account at HERE mobility [email the HERE support team](mailto:mobility_developers@here.com) and provide your full name and email address.

You'll receive an initial password and verification email to your mailbox.
At a later stage, you'll be able to manage your account via our HERE mobility developer portal.

To obtain application user credentials for the Demand API, [email the HERE support team](mailto:mobility_developers@here.com) and specify the following:

-   Your application name
-   A URL for a web application or a package/store ID for a mobile app

You will receive: 

-   An application key 
-   An application secret value

HERE is an example of what the application key and secret values look like:  


```{"applicationKey": "Casd9nS4WUs90***cCvsurYgtpLEgm8", "applicationSecret": "QcVyN7Wq3HNqWN3DEAI0H***mibtsdUkJ_8zS0skrRHfZyzKbW0gmvjSKgnLt"}```

>**Note**: For security reasons, the **applicationSecret** value must not be exposed to the end user. Store the **applicationSecret** value in your server-side code and not in your client-side code. If any abuse of the **applicationSecret** is detected, your credentials will be revoked.

## Authenticating Application Users ##

For security reasons, when you access the HERE Mobility Demand API on behalf of your users, you will need to sign in with their user ID and with the Demand API App Key and App Secret values.

### Getting a Client-to-Service (C2S) Token ###

When calling the Client-to-Service (C2S) API, your backend server should calculate a signed hash value (with limited expiration) and pass it to the app. The app should then pass the hash value to the Demand C2S API. (This is because you are not allowed to pass the application secret value to your client side.) 

The following JavaScript example shows how to calculate the hash correctly, including sample values of each step of the way, so you can ensure your calculation is correct.

```
user_id = pm.environment.get("user_id");
application_key = pm.environment.get("application_key");
application_secret = environment.application_secret;

var now = new Date();
var expiration = Math.round(new Date().getTime()/1000) + 60*30;
pm.environment.set("expiration", expiration);

sample = false; // CHANGE TO TRUE TO DEBUG YOUR HASHING CODE IF YOU GET 401
if (sample)
{
    console.log("***USING SAMPLE***");
    user_id = "1";
    application_key = "AnAppl1cat10nK3yFr0mHEREMobility";
    application_secret = "y0uRAppl1cati0nS3cr3tFr0mHEREIsLooong3rThanTh3Appl1cat10nS3cr3t";
    expiration = 1550140346;
}

function Base64Encode(str) {
    var bytes = CryptoJS.enc.Utf8.parse(str);
    return CryptoJS.enc.Base64.stringify(bytes);
}

var message = Base64Encode(application_key) + "." + Base64Encode(user_id) + "." + expiration;

var privateKeyBytes = CryptoJS.enc.Utf8.parse(application_secret);
console.log("private key");
if(sample)
{
    console.log("(for sample, should be: ");
  console.log("793075524170706c3163617469306e5333637233744672306d4845524549734c6f6f6f6e6733725468616e5468334170706c3163617431306e533363723374");
    console.log(")");
}

console.log("your result: ");
console.log(privateKeyBytes.toString(CryptoJS.enc.Hex));
var hash = CryptoJS.HmacSHA256(message, privateKeyBytes);
var hashHex = hash.toString(CryptoJS.enc.Hex);
console.log("hash in Hex");

if (sample)
{
    console.log("(for sample, should be: ");
    console.log("fdb1ae8445692bf8a4071caff257e3274615b3f5829fc58a8f801a3d97e74d5f");
    console.log(")");
}

console.log("your result: ");
console.log(hashHex);

pm.environment.set("hash", hashHex);
```

Here is an example of the REST call for passing the hash value:

```GET accounts.v1/application/c2s/token?application_key=<application_key>&user_id=<user_id>&expiration=<expiration>&hash=<hash>```

>**Notes**:
>-   The **application_key** and **user_id** values are plain strings (not converted to Base64 as when providing them to the hash function)
>-   The **expiration** value determines when the authentication token expires (in seconds, since Epoch).

## Sandbox and Production Environments ##

You can use the HERE Mobility Sandbox environment to develop and test your app's functionality without calling the production platform. Requests to the sandbox environment are ephemeral (do not affect the "real world").

Initially your credentials are created in the Sandbox environment, as indicated in your Demand API section at https://developer.mobility.here.com. When you're ready for production, click "Start" under "Ready for Production?" and HERE Mobility Support will handle your activation request.

## Registering a Webhook for Marketplace-Initiated Updates ##

The HERE Marketplace can send updates about a ride's status, location, ETA and price.
In your application, you must implement a webhook service to handle these updates.
(See [Handling Update Messages](DemandDevGuide_HandlingUpdateMessages.md) to learn more about the possible update messages.)

During the onboarding stage, you must supply the HERE support team with the following details about your webhook:

* **Protocol** - the protocol that the webhook supports (GRPC or REST)
* **Version** - the Demand API version you're working with
* **Endpoint** - the webhook's URL and port
* **Token** - the authentication token supplied by HERE
* **Timeout** - the number of seconds the Marketplace should wait when calling the webhook, before a timeout is declared. This value may be between 1 and 10 seconds (the default is 3 seconds).

>**Note:** You should supply webhook details for each of your applications, and for both Sandbox and Production environments.
