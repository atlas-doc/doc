{% coverImg src="./.gitbook/assets/ATL_002_Gitbook-headers_Atlas_Quick-Start.png" %}
{% endcoverImg %}


# Quick Start

This guide shows you how Atlas API instantly connects you to over 200 LCCs — opening up new markets for your business.

The integration is a simple four-step process:

![](./.gitbook/assets/FlowChart_1_QuickStart.png)

Let’s get you started!

## Get Atlas Sandbox credentials

The Sandbox API credentials or the API key can be created by yourself via ATRIP. Access the "Profile" section and then in "My Profile", click on the "Customer Information" tab. The "Generate" button should be clicked and the sandbox credentials will be automatically created. The API credentials or key contain two items: **x-atlas-client-id** and **x-atlas-client-secret**.

The API Key is used to authenticate your API requests. Any request that doesn't include an API key will return an error.

Please add them to the header of each post request.



> **Tip**: We've put together a Postman Collection that contains all of the requests you'll need to follow along with this guide; please download it 
 [here](./.gitbook/assets/Atlas UAT Test Shopping & Ticketing Services Only Postman Collection.zip).

{% hint style="info" %}
Please right click on the above link and click "Open link in new window". The file will start downloading.
{% endhint %}



## Issue a Ticket

As a travel seller, your goal is to help your customers find the best flight routes at affordable prices. So, let’s look at how Atlas API can help you achieve this with minimal development to your existing booking and reservation system.

The booking process is relatively simple, as illustrated:

![](./.gitbook/assets/FlowChart_2_IssueTicket.png)

## 1. Search

Create an order request to search for flights.

To build an order, you'll need to provide passenger information and itinerary details. Your customers need to enter information such as the number of passengers, origin, destination and travel dates. The ticket fare for passengers under 12 is different, so you need to mention the number of infants or child passengers below 12. 

Once the request is submitted, we send the search parameters to our robust search cache. The cache will respond with real-time offers in <0.5 sec for partner airlines operating flights between the source and destination cities on the requested date. Atlas algorithm can process over 5000 queries per second (QPS). Currently, you cannot filter the number of search results by airlines. We are working to add this feature so our partner agencies can limit the search results to include only their preferred airlines.

Here's how the function works:

- [Search](./atlas-api-documentation/api-reference/shopping-and-ticketing/search.md)


Please record the `routingIdentifier` for each routing offer.

## 2. Verify

The offers returned as a result of the search query will have detailed information about the flight, such as departure and arrival time, the number of layovers, flight number, and fare. Once the user selects a flight of their choice, the fare and flight information are verified.

Obtain the `routingIdentifier` for the selected routing and send it with the verification request.

- [Verify](./atlas-api-documentation/api-reference/shopping-and-ticketing/verify.md)


## 3. Order

The user is now one step away from making a booking with you. They need to enter their full name, gender, birth date, nationality, credit card details and billing address. 

Reference the `sessionId` recorded from the verification response and send it along with the order request with passenger details and ancillary selections with `productCode` of each `ancillaryProductElement`.



As soon as they submit their details, they will see the detailed itinerary and ancillary information, PNR number, and information on cancellation, change and refunds.

- [Order](./atlas-api-documentation/api-reference/shopping-and-ticketing/order.md)

## 4. Pay

Atlas supports two options for payment:

* Atlas to settle payment with the airline (deposit)
* You can directly pay the airline (VCC pass-through)

If you choose the first option, you pay the total ticket amount plus the technical service fee to Atlas, and Atlas will settle the payment with the airlines on your behalf.

If you choose the second option, we will send your credit card information along with the `IssueTicket` request to the airline. In this case, we will deduct the technical service fee from your account with Atlas. Several airlines support the pass-through option, for which we have added the `supportCreditTransPayment` function in the routing element.

Reference the `orderNo` from the order response when sending the payment request.

- [Payment](./atlas-api-documentation/api-reference/shopping-and-ticketing/payment.md)

{% hint style="info" %}
Please note that the Atlas Fare Guarantee is only applicable for the transactions done "deposit" mode of payment. The Atlas Fare Guarantee is not applicable for VCC pass-through mode of payment. For transactionsusing the customer VCC pass-through, since we do not provide fare guarantee, we may fail booking in some cases. The error codes related to the failed bookings can be found [here] (.atlas-api-documentation/api-reference/overview/errors.md)

{% endhint %}

## 5. Ticket Notification Webhook

Atlas uses webhooks to automatically notify partner agencies when there is a change in flight schedule for any of their orders. You can then inform your customers of the change.

Please follow the steps [here](./atlas-api-documentation/api-reference/notifications-by-webhook/) to register your webhooks and start receiving notifications.

In case of any changes, you will receive `order.ticketed` notification on your server. You can process this information and act on it as needed.

- [Ticketing Complete Notification](./atlas-api-documentation/api-reference/notifications-by-webhook/ticketing-complete-notification.md)
