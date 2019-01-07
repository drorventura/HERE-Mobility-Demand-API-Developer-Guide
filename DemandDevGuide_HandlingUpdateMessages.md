# HERE Demand API Workflow: *Handling Update Messages with Webhooks* #

Throughout the lifecycle of a ride, the HERE Marketplace can send updates about the ride's status, location, ETA and price. There are 2 ways your application can get updates about a ride's status and other details:

* By calling the *GetRide* and *GetRideLocation* functions periodically (polling)
* By implementing a webhook callback function (updates are pushed to your application by the HERE Marketplace)

>**Note:** Currently only GRPC webhooks are supported.

If you choose to use a webhook function, it must implement the **DemandWebhookAPI** service, which contains 4 functions: 

* HandleStatusUpdate
* HandleETAUpdate
* HandlePriceUpdate
* HandleLocationUpdate

>**Note:** See [Getting Started](DemandDevGuide_GettingStarted.md) to learn how to register your webhook service.

As mentioned above, you can also request this information actively, by calling *GetRide* and *GetRideLocation*, and we recommend that you do this occasionally. However, it's inefficient to poll for this information frequently, and this is why Marketplace-initiated updates are useful, as they're sent only when a change has occurred.

When you receive an update about a ride, you can choose how to convey this information to the end user (display it within your app, send an SMS, etc.).

>**Notes:** 
>* It's possible that the same update message will be sent more than once. Each update message has an **event_id** field with a unique ID value. Your app should discard messages that it's already received (as determined by the **event_id** value).
>* Each webhook message has an authentication token in its header. (This is the token you received when you registered your webhook.) Your application should always verify that you received the expected token value, and if not, discard the message without processing it.

Here are examples of updates your webhook function can receive:

**Status update:**

	COMING SOON


**Location update:**

	COMING SOON


**ETA update:**

	COMING SOON


**Price update:**

	COMING SOON
