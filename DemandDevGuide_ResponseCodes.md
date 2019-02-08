# Here Demand API Response Codes #

## Introduction ##

While working with one of the HERE API or SDK packages, you may receive error responses from the HERE Server. The following sections describe the error structures, codes and messages you may receive.

<a name="GRPCErrorStructure"></a>
## GRPC Error Structures ##

In error situations, all endpoints return a GRPC Status object as defined below.

    type Status struct {
        // The error code (a value from the google.rpc.Code enum)
        Code int32
        // A textual, informative, English-language error message
        Message string
        // A list of messages describing the error details
        Details []*google_protobuf.Any
    }

>**NOTE**: If the GRPC-gateway fails to identify the server error, it creates a new GRPC error with an UNKNOWN error code (which is mapped to the HTTP 500 Internal Server Error).

The **Details** field of the **Status** structure contains the following nested structure:

    type ExternalError struct {
       // The external error code
       Code int32 `protobuf:"varint,1,opt,name=code" json:"code,omitempty"`
       // Locale code (see http://www.rfc-editor.org/rfc/bcp/bcp47.txt)
       // Note: currently the only supported Locale is "en-US". 
       Locale string `protobuf:"bytes,1,opt,name=locale" json:"locale,omitempty"`
       // The error message, localized by locale.
       // The Message string is the same as the message string in the Status structure.
       Message string `protobuf:"bytes,2,opt,name=message" json:"message,omitempty"`
    }

## RESTful JSON Error Structure ##

The GRPC error is translated to its RESTful JSON representation automatically by the GRPC-gateway package. The JSON body contains the error code, locale and message values from the Status structure shown above.

Here is an example of a JSON-formatted error:

    Header Code: 404
    Body:
    {
        "code": 40400,
        "locale: "en-US"
        "message": "Requested item not found"
    }
 
The GRPC error code is translated to an HTTP header status code, according to the mapping in the following table:

GRPC Error Code	| HTTP Error Code
:---------------|:----------------
InvalidArgument	|StatusBadRequest (400)
OutOfRange	|StatusBadRequest (400)
PermissionDenied	|StatusForbidden (403)
Unauthenticated	|StatusUnauthorized (401)
NotFound	|StatusNotFound (404)
AlreadyExists	|StatusConflict (409)
FailedPrecondition	|StatusPreconditionFailed (412)
Internal	|StatusInternalServerError (500)
Unimplemented	|StatusNotImplemented (501)
Unknown	|StatusInternalServerError (500)
 
## Error Categories ##

All external errors have one of the categories described in the following table:

Error Category	| Description
:---------------|:------------
**Input**	|	Error in request input.<br/><br/>Possible GRPC codes:<br/><br/>InvalidArgument(3) – missing, malformed or otherwise invalid argument<br/><br/>OutOfRange(11) – value has the correct type but is out of the valid range
**Permissions**|Authorization or authentication error.<br/><br/>Possible GRPC codes:<br/><br/>**PermissionDenied(7)** – attempt to perform an action for which the user has no permissions<br/><br/>**Unauthenticated(16)** – the user failed to be authenticated
**Communication** | Connection error or timeout when accessing other services.<br/><br/>Possible GRPC codes:<br/><br/>**Unavailable(14)** – the service is unavailable
**Business Logic** | The request or its data is incompatible with the current server state.<br/><br/>Possible GRPC codes:<br/><br/>**NotFound(5)** – requested item was not found (for example, a ride ID)<br/><br/>**AlreadyExists(6)** – attempt to create an entity that already exists<br/><br/>**FailedPrecondition(9)** – the request does not meet a required condition (for example, a delete was requested when delete is not allowed)<br/><br/>**Internal(13)** – other error in business logic
**Other** 	|	Miscellaneous errors.<br/><br/>Possible GRPC codes:<br/><br/>**Internal(13)** – error in business logic<br/><br/>**Unimplemented(12)** - the endpoint is not implemented yet.

## Error Codes ##

The following table describes the error codes that Here API clients can receive:

Domain|	Error|	Code
:-----|:-----|:------
Request	Ride | Invalid request |	400000
Request Ride | Route missing from ride request | 400001
Request Ride | Pickup location missing from ride request | 400002
Request Ride | Geo-location missing from ride request | 400003
Request Ride | Invalid latitude in ride request (should be between -90 and 90) | 400004
Request Ride | Invalid longitude in ride request (should be between -90 and 90) | 400005
Request Ride | Dropoff location missing from ride request | 400007
Request Ride | Pickup time missing from ride request | 400009
Request Ride | Pickup time is too far in the future | 400010
Request Ride | Pickup time has passed | 400011
Request Ride | Invalid maximum walking distance value | 400016
Request Ride | Maximum number of transit changes exceeded | 400017
Request	Ride | Requested item not found|	404000
Request	Ride | Request timeout|	408000
Request	Ride | Failed dependency	|424000
Create Ride  | Attempt to book a ride whose offer has timed out | 404001
Get Ride     | Requested ride not found | 404002
Cancel Ride  | Attempt to cancel a ride whose ID can't be found | 400018
Cancel Ride  | Invalid reason category format | 400019
Cancel Ride  | Invalid reason category value | 400020
Get Ride Offer |Missing or invalid offer ID | 400021
Get Ride Offer |Missing or invalid demander ID | 400023
Connection	   |Too many requests|	429000
Authorization  |Permission denied	|403000
Authentication |Invalid token|	401001
Authentication |Token expired	|401002
General        |Missing user ID | 400022
General	       |Internal server error|	500000
General	       |Not Implemented|	501000

## References ##

[https://cloud.google.com/apis/design/errors](https://cloud.google.com/apis/design/errors)

[https://github.com/grpc/grpc-go/tree/master/examples/rpc_errors](https://github.com/grpc/grpc-go/tree/master/examples/rpc_errors)

[https://jbrandhorst.com/post/grpc-errors](https://jbrandhorst.com/post/grpc-errors)
