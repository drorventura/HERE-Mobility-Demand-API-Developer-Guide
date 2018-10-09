# HERE Demand API Workflow: *Cancelling a Ride* #

You may want to cancel a ride at any stage during the ride's lifecycle, following a cancellation request from the user.

>**Notes:** 
>* Whether ride cancellation is allowed depends on the supplier's policy. If cancellation isn't allowed, the call to *CancelRide* will result in a **REJECTED** cancellation status.
>* *CancelRide* will fail if you try to cancel a ride that isn't active.
>* The *CancelRide* call is identical for the C2S and S2S APIs.
>* The processing of the *CancelRide* call is asynchronous. After you receive a successful response to *CancelRide*, you must poll the Ride object by calling *GetRide* (see the procedure below).

**To cancel a ride:**

1. Call *CancelRide*, using the **ride_id** value that you received as a response to *CreateRide*.

----
<details>
<summary><b>REST Example</b></summary>

**Request:**

    COMING SOON

**Response:**

	COMING SOON

</details>

----

<details>
<summary><b>GRPC Example</b></summary>

**Request:**

    COMING SOON


**Response:**

    COMING SOON

</details>

2. Call **GetRide** repeatedly and examine the **status** value of the **CancellationInfo** field. Its value will be one of: **PROCESSING** (cancellation is still being processed), **ACCEPTED** (the cancellation was accepted) or **REJECTED** (the cancellation was rejected). See []() to learn more about the **GetRide** call.




