# HERE Demand API Workflow: *Handling Update Messages* #

Throughout the lifecycle of a ride, the HERE Marketplace can send updates about the ride's status, location, ETA and price. In your application, you must implement a webhook callback function to handle these updates.

You can also request this information actively, by calling *GetRide* and *GetRideLocation*, and we recommend that you do this occasionally. However, it's inefficient to poll for this information frequently, and this is why Marketplace-initiated updates are useful, as they're sen only when a change has occurred.

When you receive an update about a ride, you can choose how to convey this information to the end user (display it within your app, send an SMS, etc.).

Here are examples of updates your webhook function can receive:

**Status update:**

	COMING SOON


**Location update:**

	COMING SOON


**ETA update:**

	COMING SOON


**Price update:**

	COMING SOON
