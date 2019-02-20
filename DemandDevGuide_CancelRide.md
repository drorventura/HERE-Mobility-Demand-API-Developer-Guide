# HERE Demand API Workflow: *Cancelling a Ride* #

You may want to cancel a ride at any stage during the ride's lifecycle, following a cancellation request from the user.

>**Notes:** 
>* Whether ride cancellation is allowed depends on the supplier. If cancellation isn't allowed, either for the specific ride or as a general policy, the call to *CancelRide* will result in a **REJECTED** cancellation status.
>* *CancelRide* will fail if you try to cancel a ride that isn't active.
>* See [More Information Ride Cancellation](https://github.com/Developers-Here-Mobility/HERE-Mobility-Demand-API-Developer-Guide/blob/master/DemandDevGuide_RideCancellationDetails.md) to learn more about cancellation policies and cancellation reasons.

**To cancel a ride:**

Call *CancelRide*, using the **ride_id** value that you received as a response to *CreateRide*.
You will receive a response with a CancellationInfo.status of ACCEPTED or REJECTED.








