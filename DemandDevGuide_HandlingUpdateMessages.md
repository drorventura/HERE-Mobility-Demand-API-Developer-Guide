# HERE Demand API Workflow: *Handling Update Messages with Webhooks* #

Throughout the lifecycle of a ride, the HERE Marketplace can send updates about the ride's status, location, ETA and price. There are 2 ways your application can get updates about a ride's status and other details:

* By calling the *GetRide* and *GetRideLocation* functions periodically (polling)
* By implementing a webhook callback function (updates are pushed to your application by the HERE Marketplace)

>**Note:** Currently only GRPC webhooks are supported.

If you choose to use a webhook function, it must implement the **DemandWebhookAPI** service, which contains 4 functions: 

* HandleRideUpdate (contains info about ride status, driver and price details)
* HandleETAUpdate (contains info about estimated pickup and dropoff times) 
* HandleLocationUpdate (contains info about the ride's current location)

>**Note:** See [Getting Started](DemandDevGuide_GettingStarted.md) to learn how to register your webhook service.

As mentioned above, you can also request this information actively, by calling *GetRide* and *GetRideLocation*, and we recommend that you do this occasionally. However, it's inefficient to poll for this information frequently, and this is why Marketplace-initiated updates are useful, as they're sent only when a change has occurred.

When you receive an update about a ride, you can choose how to convey this information to the end user (display it within your app, send an SMS, etc.).

>**Notes:** 
>* It's possible that the same update message will be sent more than once. Each update message has an **event_id** field with a unique ID value. Your app should discard messages that it's already received (as determined by the **event_id** value).
>* Each webhook message has an authentication token in its header. (This is the token you received when you registered your webhook.) Your application should always verify that you received the expected token value, and if not, discard the message without processing it.
>* All update messages contain the mandatory **event_metadata** field (see examples below). 

Here are examples of updates your webhook function can receive:

**Ride Update Example:**

>**Notes:** 
>* The **status_change** field will appear only if the ride status has changed since the last update message.
>* The **driver_vehicle_details** field will appear only if the relevant details have been provided by the ride Supplier.
>* The **cancellation_info** field will appear if a cancellation was requested. It contains details such as the time of the cancellation request and the reason for cancellation.
>* The **rejection_reason** field will appear only if the ride has been rejected.
>* The **price** field will appear only when the Supplier has provided the *final* price.
 
```
{
    "event_metadata": {
                "event_time": ,
                "event_id": "Ah723gdjahsvcnsac0xr823",
                "demand_info": {
                                "demander_id":"SomeDemander",
                                "user_id": "SomeUser",
                                "app_id": "SomeApp"
                },
                "ride_id": "Jfhdus84gfjdsgr634bjdskb"
    },
    "status_change": {
                "status": "ACCEPTED",
    },
    "driver_vehicle_details": {
                                "driver_details": {
                                "name": "someDriver",
                                "phone_number": "+555555555555",
                                "photo_url": "http://someUrl...",
                                "driving_license_id": "123456789"
                },
                "vehicle":{
                                "license_plate_number": "123456789",
                                "vehicle_type": "STANDARD",
                                "make": "SomeMaker",
                                "model": "SomeModel",
                                "color": "Blue"
                }
    },
    "cancellation_info": {
                "cancelling_party": "DEMANDER",
                                "cancel_reason": "changed my plans",
                                "request_time_ms": 12341,
                                "status": "PROCESSING",
                                "cancel_reason_category": "PASSENGER_REQUESTED_TO_CANCEL"
    },
    "rejection_reason": {"value": "rejected by MP"},
    "price": {
                "amount": 120,
                "currency_code": "USD"
    }
}
```

**ETA Update Example:**

>**Notes:** 
>* The **estimated_pickup_time_seconds** field will only appear until the passenger is onboard.
>* The **estimated_dropoff_time_seconds** will only appear once the passenger is onboard, and until dropoff or other terminal status.

```
{
    "event_metadata": {
                "event_time": ,
                "event_id": "Ah723gdjahsvcnsac0xr823",
                "demand_info": {
                                "demander_id":"SomeDemander",
                                "user_id": "SomeUser",
                                "app_id": "SomeApp"
                },
                "ride_id": "Jfhdus84gfjdsgr634bjdskb"
    },
    "estimated_pickup_time_seconds": {"value": 32},
    "estimated_dropoff_time_seconds": {"value": 566}
}
```


**Location Update Example:**

>**Note:** The **point** field contains the latitude and longitude values of the current vehicle location.

```
{
    "event_metadata": {
                "event_time": ,
                "event_id": "Ah723gdjahsvcnsac0xr823",
                "demand_info": {
                                "demander_id":"SomeDemander",
                                "user_id": "SomeUser",
                                "app_id": "SomeApp"
                },
                "ride_id": "Jfhdus84gfjdsgr634bjdskb"
    },
    "point": {
                "lat": 32.123123,
                "lng": 33.4444
    }
}
```


