# HERE Demand Overview #

## HERE Mobility Platform Overview ##

HERE Mobility aims to democratize the mobility ecosystem. We are creating a competitive marketplace powered by intelligent technological solutions for all mobility service providers, businesses, and consumers.

HERE's central platform is the **HERE Mobility Marketplace**, a hub for supplying and requesting mobility services, for businesses and consumers. The Marketplace enables matching up end users with suppliers who can meet their needs for transportation and delivery.

The HERE Mobility platform offers two APIs: the **Demand API**, for use by client applications serving end users (passengers), and the **Supply API**, for use by applications representing ride suppliers such as taxi dispatching stations.

The **HERE Mobility Demand API** is a REST or GRPC API that enables the customer application to request, book and cancel mobility services. Demand API requests are sent to the HERE Mobility Marketplace, which
matches up ride requests with available suppliers, and manages ride information and statuses.

## HERE Demand Packages and Interfaces ##

HERE supports several types of packages and interfaces to the Mobility Demand functionality, for both desktop and mobile clients. The table below describes these packages.

>**Note:** This guide describes the **REST and GRPC Demand APIs**. To learn about another package, please look for its documentation on the [HERE Mobility GitHub page](https://github.com/Developers-Here-Mobility).

Package | Supported Platforms/Interfaces | Description
:--------|:----------------------------|:------------
Demand **SDK** | iOS, Android | SDK for mobile devices
Demand React Native **SDK** | iOS, Android | React Native Javascript wrapper SDK for mobile devices
Demand Consumer-to-Service (C2S) **API** | REST, GRPC | API for a single user (typically used by a mobile device app)
Demand Service-to-Service (S2S) **API** | REST, GRPC | API for managing multiple users

## Introduction to the HERE Demand API ## 

The Demand API enables the calling application to request, book and cancel mobility services. Here are some examples of possible client applications:

-   A smartphone app, which a private customer uses to book a taxi ride.
-   A public kiosk device located at a business, such as a mall or hotel lobby, which provides mobility services to multiple customers.

End users can request a ride while defining any special needs they may have, such as number of passenger or suitcase storage. Users can also request to sort the ride offers by price or ETA (Estimated Time of
Arrival). They can view several ride options, choose the one they want, and book it. If the supplier's policy permits, rides may be cancelled after they're booked. Once a ride is booked, the passenger can get real-time updates about the supplier's status (on the way, at pickup location, and so on).

>**Notes**:
>-   Currently only taxi suppliers (full integration) and public transportation(planning stage) are supported.
>-   The passenger's location is stated in the ride request, and accordingly only rides from nearby suppliers are offered.

### Technical Specifications ###

The Demand API is a supported over the REST and GRPC protocols.

**REST endpoint:** [https://demand-rest.inc-stg.solo-experiments.com](https://demand-rest.inc-stg.solo-experiments.com/)

**GRPC endpoint:** [https://demand-grpc.inc-stg.solo-experiments.com](https://demand-grpc.inc-stg.solo-experiments.com/)

>**Note**: For a single client, requests to the Demand API must be limited to a rate of 50 requests per minute, and a total of no more than 1000 per day.

### The Consumer-to-Service and Service-to-Service APIs ###

HERE supports 2 versions of the Demand API:

-   **The Consumer-to-Service (C2S) API** -- meant to be called by a client application that supports a single end user, such as a mobile phone app.

-   **The Service-to-Service (S2S) API** -- meant to be called by a client application that supports multiple end users, such as a public kiosk device.

The 2 APIs are nearly identical in terms of syntax and workflow. The main difference is that the service-to-service request messages contain an additional user ID parameter, to enable managing rides for several users. Calls made to the consumer-to-service API are all assumed to refer to the same single user.
