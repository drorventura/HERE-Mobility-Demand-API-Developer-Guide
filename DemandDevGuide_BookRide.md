# HERE Demand API Workflow: *Requesting and Booking a Ride* #

To book a ride, the client first requests ride offers according to the required ride details. The user can then select one of the offers returned.

**To request and book a ride:**

1.  Call *RideOffersRequest*. In the call parameters, the client specifies the passenger details, pickup and dropoff locations, and optionally the number of suitcases the ride must accommodate. Optionally, the client can specify a future pickup time, a desired price range and a sort order for the returned ride offers.

>**Note:** Both calls in this procedure are nearly identical for the C2S and S2S APIs, but in the S2S calls the **user_id** is passed. In the C2S calls, the user for whom the authentication token was created is assumed implicitly for all calls.

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

    curl "http://mobility-marketplace-test.here.com/demand.v1.s2s/offers?user_id=1&route.pickup.point.lat=32.1981&route.pickup.point.lng=34.8824&route.pickup.address=zarhin%2013&route.destination.point.lat=32.1981&route.destination.point.lng=34.8824&route.destination.address=zarhin%2013&constraints.passengers_no=1&constraints.suitcases_no=1&constraints.wheelchair=false&constraints.childs_seats=0&price_range.from_amount=10&price_range.to_amount=20&price_range.currency_code=USD&sort_type=1" -H "Authorization: Bearer eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzdWIiOiIxIiwiaXNzIjoicmVzdC1hc3N1cmVkIiwiZXhwIjoxNjQ0ODM4MTM2fQ."


**Response:**

    {
        "offers": [
            {
                "offer_id": "5a8c48479b1d4c0001bf20cd",
                "supplier": {
                    "english_name": "tentacruel",
                    "local_name": "tentacruel",
                    "phone_number": "+9720516219186",
                  },
                "estimated_pickup_time": "2018-02-20T16:13:31Z",
                "estimated_price_range": {
                    "range": {
                        "from_amount": "11",
                        "to_amount": "97",
                        "currency_code": "EUR"
                    }
                },
                "offer_expiration_time": "2018-02-20T16:14:43Z",
                "cancellation_policy": "NOT_ALLOWED"
            },
            {
                "offer_id": "5a8c48479b1d4c0001bf20ca",
                "supplier": {
                    "english_name": "shellder",
                    "local_name": "shellder",
                    "phone_number": "+9720538136208",
                 },
                "estimated_pickup_time": "2018-02-20T16:13:36Z",
                "estimated_price_range": {
                    "range": {
                        "from_amount": "45",
                        "to_amount": "88",
                        "currency_code": "NIS"
                    }
                },
                "offer_expiration_time": "2018-02-20T16:14:43Z",
                "cancellation_policy": "ALLOWED"
            }
        ]
    }

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

2.  Receive a **RideOffersResponse** object. This is a list of **RideOffer** objects, containing details such as supplier ID, price, ETA and cancellation policy. If a sort order was specified in the request, the offer list is sorted by the order requested (lowest to highest price, or soonest to latest ETA).

3.  The passenger selects one of the offers.

4.  Call *CreateRideRequest*, passing the ID of the chosen offer. If successful, this call returns a **Ride** object.

>**Note**: This workflow may be repeated as necessary, if a booking request fails.

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


    curl http://mobility-marketplace-test.here.com/demand.v1.s2s/rides -X POST -H "Content-Type: application/json" -d '{ "offer_id": "5a8c48479b1d4c0001bf20ca", "user_id": "123456", "passenger": { "name": "asdasdasdasd", "phone_number": "+9725326589","photo_url": "http://asdasdasdasdasd"},"passenger_note": "north side of road" }'  -H "Authorization: Bearer eyJhbGciOiJub25lIiwidHlwIjoiSldUIn0.eyJzdWIiOiIxIiwiaXNzIjoicmVzdC1hc3N1cmVkIiwiZXhwIjoxNjQ0ODM4MTM2fQ."

**Response:**

	{
	    "user_id": "1",
	    "ride_id": "5a8c484836bb08000157c180",
	    "booking_estimated_price": {
	        "range": {
	            "from_amount": "11",
	            "to_amount": "97",
	            "currency_code": "EUR"
	        }
	    },
	    "status_log": {
	 		"create_time": "2018-02-20T16:00:36Z",
	 		"last_update_time": "2018-02-20T16:13:36Z",
	        	"current_status": "PROCESSING"
	    },
	    "passenger": {
	        "name": "asdasdasdasd",
	        "phone_number": "+9725326589",
	        "photo_url": "http://asdasdasdasdasd"
	    },
	    "passenger_note": "north side of the road"
	}

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

