# HERE Demand API Workflow: *Cancelling a Ride* #

You may want to cancel a ride after it was booked, following a cancellation request from the user.

>**Notes:** 
>* Whether ride cancellation is allowed depends on the supplier's policy. If cancellation isn't allowed, the call to *CancelRide* will fail. 
>* *CancelRide* will also fail if you try to cancel a ride that isn't active.

**To cancel a ride after it was booked:**

Call *CancelRide*, using the **ride_id** value that you received as a response to *CreateRide*.

>**Notes:** 
>* This call is identical for the C2S and S2S APIs.
>* The processing of the *CancelRide* call is asynchronous. After you receive a successful response to *CancelRide*, you must poll the Ride object by calling *GetRide*. Examine the **status** value of the **CancellationInfo** field. Its value will be one of: **PROCESSING** (cancellation is being processed), **ACCEPTED** (the cancellation was accepted) or **REJECTED** (the cancellation was rejected).

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




