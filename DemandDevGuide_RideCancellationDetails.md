# More Information Ride Cancellation #

A ride may be cancelled either by the passenger or by the supplier/driver, at any stage after the passenger requests to book it.

If the passenger requests to cancel a ride, your demand-side application must call the [*CancelRide* API](https://github.com/Developers-Here-Mobility/HERE-Mobility-Demand-API-Developer-Guide/blob/master/DemandDevGuide_CancelRide.md).

If the supplier or driver cancels a ride, it's the supply-side application's responsibility to change the ride's status to **CANCELLED**. The next time your demand-side application calls *GetRide*, the **Ride** object's **Status** value will be **CANCELLED**, and your application must handle this situation appropriately.

See [Cancellation Information in the Ride Object](#InfoInRideObject) to learn about additional cancellation information in the **Ride** object.

## Cancellation Policy ##

Different suppliers have different cancellation policies. Some allow cancellations with no fine or fee, and some do not. Each ride offer has a **CancellationPolicy** field, whose value you can test to see whether cancellation is allowed for the specific ride offer or not. This field also appears in the **Ride** object.

If a request to cancel a ride is rejected, this means that the supplier's policy does not allow cancellations, and in this case the passenger may have to pay the full fee, even if he or she doesn't actually take the ride.

<a name="InfoInRideObject"></a>
## Cancellation Information in the Ride Object ##

The **Ride** object contains several fields related to cancellation, most of which are only populated when a cancellation occurs. The table below summarizes these fields.

Field | Type | Description
:-----|:-----|:-----------
cancellation_policy | RideOffer.CancellationPolicy | The supplier's cancellation policy. Possible values are: **UNKNOWN_CANCEL_POLICY**, **ALLOWED**, **NOT_ALLOWED**
cancellation_info | CancellationInfo | Optional. When a cancellation occurs, this field contains information about the cancellation. See more details below.
cancellation_info.cancelling_party | CancellationInfo.Party | Which party canceled the ride. Possible values are: **UNKNOWN**, **DEMANDER**, **SUPPLIER**.
cancellation_info.cancel_reason | string | A free-text cancellation reason entered by the cancelling party.
cancellation_info.request_time_ms | uint64 | The time the cancellation was requested.
cancellation_info.status | CancellationInfo.Status | Possible values are: **PROCESSING**, **ACCEPTED**, **REJECTED**.
cancellation_info.cancel_reason_category | CancellationInfo.CancelReasonCategory | An enumerated type for cancellation reasons. See below.
cancellation_request_received_but_not_allowed | bool | A boolean flag. If true, this indicates that the cancellation request was received but rejected due to cancellation policy.

## Cancellation Reasons ##

The following table describes the values that  the **cancellation_info.cancel_reason_category** field of the **Ride** object can have.

Value | Cancelling Party | Description
:-----|:-----------------|:------------
UNKNOWN_CANCEL_REASON_CATEGORY | Unknown | Unknown cancellation reason
DRIVER_NO_SHOW | Passenger | The driver didn't arrive at the pickup location.
PRICE_CHANGED | Passenger | The passenger cancelled because the ride price changed.
ETA_CHANGED | Passenger | The passenger cancelled because the ride ETA changed.
UNSUITABLE_VEHICLE | Passenger | The passenger cancelled because the vehicle did not meet requirements.
DRIVER_BEHAVED_INAPPROPRIATELY | Passenger | The passenger cancelled because the driver behaved inappropriately.
CHANGED_MY_PLANS | Passenger | The passenger cancelled because of a change in his/her plans.
DRIVERS_UNAVAILABLE | Supplier | The supplier cancelled because no drivers were available.
PASSENGER_NO_SHOW | Supplier | The supplier cancelled because the passenger did not arrive at the pickup location.
PASSENGER_REQUESTED_TO_CANCEL | Supplier | The supplier cancelled because the passenger spoke to the driver and requested a cancellation.
VEHICLE_MALFUNCTION | Supplier | The supplier cancelled because of a malfunction in the vehicle.
HEAVY_TRAFFIC | Supplier | The supplier cancelled because heavy traffic is preventing the driver from arriving.
OTHER_CANCEL_REASON_CATEGORY | Passenger or Supplier | Either the passenger or the supplier cancelled for any reason other than the above.<br/><br/>**Note:** If you use the OTHER cancellation reason, we recommend filling the free-text **cancellation_info.cancel_reason** field with a user-defined entry.



