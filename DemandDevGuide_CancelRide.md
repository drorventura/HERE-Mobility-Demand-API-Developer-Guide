# HERE Demand API Workflow: *Cancelling a Ride* #

You may want to cancel a ride at any stage during the ride's lifecycle, following a cancellation request from the user.

>**Notes:** 
>* Whether ride cancellation is allowed depends on the supplier. If cancellation isn't allowed, either for the specific ride or as a general policy, the call to *CancelRide* will result in a **REJECTED** cancellation status.
>* *CancelRide* will fail if you try to cancel a ride that isn't active.
>* The processing of the *CancelRide* call is asynchronous. After you receive a successful response to *CancelRide*, you must poll the Ride object by calling *GetRide* (see the procedure below).
>* See [More Information Ride Cancellation](https://github.com/Developers-Here-Mobility/HERE-Mobility-Demand-API-Developer-Guide/blob/master/DemandDevGuide_RideCancellationDetails.md) to learn more about cancellation policies and cancellation reasons.

**To cancel a ride:**

1. Call *CancelRide*, using the **ride_id** value that you received as a response to *CreateRide*.

----
<details>
<summary><b>REST C2S Example</b></summary>

**Request:**

    COMING SOON

**Response:**

	COMING SOON

</details>

----

<details>
<summary><b>REST S2S Example</b></summary>

**Request:**

    COMING SOON

**Response:**

	COMING SOON

</details>

----

<details>
<summary><b>GRPC C2S Example</b></summary>

**Request:**

    COMING SOON


**Response:**

    COMING SOON

</details>

----

<details>
<summary><b>GRPC S2S Example</b></summary>

**Request:**

    COMING SOON


**Response:**

    COMING SOON

</details>

----

2. Call **GetRide** repeatedly and examine the **status** value of the **CancellationInfo** field. Its value will be one of: **PROCESSING** (cancellation is still being processed), **ACCEPTED** (the cancellation was accepted) or **REJECTED** (the cancellation was rejected). See [Getting a Ride Object](https://github.com/Developers-Here-Mobility/HERE-Mobility-Demand-API-Developer-Guide/blob/master/DemandDevGuide_GetRide.md) to learn more about the **GetRide** call.





