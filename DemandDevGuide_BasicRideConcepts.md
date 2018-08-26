# Basic Ride Concepts #

<a name="RideAndRideLocation"></a>
## Ride Object vs. RideLocation Object ##

The **Ride** object contains all the ride information *except* for location information. This includes details such as the ride ID, user ID, route, ride constraints, and so on. Almost all the Ride object fields contain details that don't change throughout the ride. (The exception to this is the **Status** field, which changes over the ride's lifetime.)

The RideLocation object contains the following dynamic, frequently updated information:

- Location (latitude/longitude pair)
- Estimated pickup time
- Estimated dropoff time
- Last update time (of location details)

See [Here Mobility Demand API Reference](https://github.com/Developers-Here-Mobility/Here-Mobility-Demand-API-REST) to learn more about the Ride and RideLocation objects.

## Immediate Rides vs. Future Bookings ##

When you request ride offers, you can specify whether the ride should start immediately (or as soon as possible), or whether you're making a reservation for a future ride. If you populate the **prebook_pickup_time** field with a value, this indicates a future ride; leaving the field empty indicates an immediate ride.

>**Note:** The value of **prebook_pickup_time** must be at least 30 minutes from the time the ride offers request is made.

## Driver Assignment ##

For an immediate ride, usually a driver is assigned shortly after a booking request is made, and the driver doesn't change throughout the ride's lifetime. However, it is possible that the driver may change, if the original driver who accepted the booking cancels for any reason.

In the case of a future booking, the driver is only assigned close to the ride time, and not immediately after receiving a booking request. Therefore, after booking a future ride, you'll see that the ride status is ACCEPTED until just before the ride time, and then it will change to DRIVER_ASSIGNED. 


## Ride Cancellation ##

Whether ride cancellation is allowed depends on the supplier's cancellation policy. 
If the policy does not allow for cancellation and a user cancels anyway, the user will have to pay a certain amount for the cancellation.

