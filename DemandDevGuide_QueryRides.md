# HERE Demand API Workflow: *Querying for Rides* #

You can query for rides according to their status and the time they were last updated. 

In the query parameters, you can specify the following ride statuses:

Status | Description
:------|:-------------
PAST | Rides from the last 14 days with terminal statuses (COMPLETED, REJECTED and CANCELLED)
FUTURE	| Pre-booked rides up to 30 minutes before their start time.
ONGOING	| All active rides (with statuses other than FUTURE and PAST)
ALL	|	All rides, regardless of status


**To query for a ride by status and/or update time:**

Call *GetRideListRequest*.



