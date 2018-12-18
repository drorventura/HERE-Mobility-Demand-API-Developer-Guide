# HERE Demand API Workflow: *Handling Update Messages* #

Throughout the lifecycle of a ride, the HERE Marketplace can send updates about the ride's status, location, ETA and price. In your application, you must implement a webhook callback function to handle these updates. The webhook must implement the **DemandWebhookAPI** service, which contains 4 functions: 

* HandleStatusUpdate
* HandleETAUpdate
* HandlePriceUpdate
* HandleLocationUpdate

>**Note:** See [Getting Started](DemandDevGuide_GettingStarted.md) to learn more about how to register your webhook service.

You can also request this information actively, by calling *GetRide* and *GetRideLocation*, and we recommend that you do this occasionally. However, it's inefficient to poll for this information frequently, and this is why Marketplace-initiated updates are useful, as they're sent only when a change has occurred.

When you receive an update about a ride, you can choose how to convey this information to the end user (display it within your app, send an SMS, etc.).

>**Note:** It's possible that the same update message will be sent more than once. Each update message has an **event_id** field with a unique ID value. Your app should discard messages that it's already received (as determined by the **event_id** value).

Here are examples of updates your webhook function can receive:

**Status update:**

	COMING SOON


**Location update:**

	COMING SOON


**ETA update:**

	COMING SOON


**Price update:**

	COMING SOON
