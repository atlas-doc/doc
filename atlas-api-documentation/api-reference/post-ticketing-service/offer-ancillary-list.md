# Search Ancillary

### Dependency

No preceding function needs to be carried out.
The order should be ticketed and the departure date should be in the future.

### Endpoint {% debug uid="searchAncillary_1.0" %}{% enddebug %}


[https://sandbox.atriptech.com/postBookingAncillarySearch.do](https://sandbox.atriptech.com/postBookingAncillarySearch.do)

{% hint style="info" %}
Please note the below "Rules & Restrictions" while initiating a post-ticketing transaction.

1. Check-in baggage and Carry-on baggage can be added to an order either in the booking flow or the post-booking flow. This can be only once throughout the whole flow. This rule aims to simplify the baggage booking flow for customers by sending the query only 1 time to book multiple baggage.

2. "Product code" contains various baggage offerings in aspects of baggage pieces and weights for each airline.

3. Baggage ancillary is not allowed to be booked for infant passenger.

4. It is not allowed to add the same type of post-booking baggage to a ticketed order the second time unless the first purchase fails in payment. Please refer to the below scenarios:

	a. When the post-booking order is in "ticket-in-process" and "ticketed" status, it's not allowed to order another one. If any query is called, API will respond with an error message.

	b. When the post-booking order is in "cancelled" status, the customer can create another order.

	c. When the post-booking order is in "unpaid" status, the customer can create another order. However, if one of the orders completes the payment and moves to "ticketing-in-process" status, the other orders will stop processing the payment.

5. In case the air ticket order already contains free baggage, it’s subject to airline’s ancillary policy whether additional baggage is allowed to be purchase either at the booking flow or the post-booking flow.

6. Same “product code” for baggage is mandatory to be added to each segment in connecting flights. If the "product code" is different for each of the segment (in the same direction)  or not added for all the sectors, the API will respond with an error message.

7. Rule No.6 doesn't work for round trip flights. This means that the customer can purchase baggage only for one of the directions (either outbound or inbound) in round trip.

8. The details of only the passenger for whom the ancillary needs to be added must be sent in the API RQ.
{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It is the original order number.

*   **ancillaryCategory **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Ancillary Category. Different categories of ancillaries need to be separately requested. Currently we only support "BAGGAGE".

*   **displayCurrency array **Optional

The alternative currency in which the fare and taxes amount needs to be displayed. The 3-letter currency code should be entered. 
    
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "xxxxxxxxxx",
    "ticketOrderNo": "TESTM20240520171341468",
    "ancillaryCategory": "BAGGAGE",
    "displayCurrency": "CNY"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **msg **<mark style="color:blue;">**string**</mark>

    The 'msg' element is for the description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    2: System error

*   **sessionId **<mark style="color:blue;">**int**</mark>

    The unique identifier for this search.

    It is required when you call order function to make a reservation to identify which ancillary the client is choosing.

*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>

    Order number. It is the original order number.
    
*   **supportCreditTransPayment **<mark style="color:blue;">**int**</mark>

    This tag is used to identify if the fare needs to be paid using the client's credit card.

    0: The credit card details will not be passed through and only pre-payment is allowed.

    1: The API will allow you to pass through client’s credit card details for payment. The customer can also use pre-payment as a method of payment.
    
*   **currency **<mark style="color:blue;">**string**</mark>

    The currency in which Atlas settles transactions with you.

*   **fromSegment Array **<mark style="color:blue;">**AncillaryElement**</mark>

    For outbound segments. Same elements as search response.

*   **retSegment Array **<mark style="color:blue;">**AncillaryElement**</mark>

    For inbound segments. Same elements as search response.

*   **ancillaries Array **<mark style="color:blue;">**AncillaryElement**</mark>

    Ancillary list provided for this order

    * **AncillaryProductElements**
      *   **segmentIndex **<mark style="color:blue;">**int**</mark>

          Segment sequence. It starts from 1. If it is round trip, the outbound and inbound sequence would be together.

      *   **endSegmentIndex **<mark style="color:blue;">**int**</mark>

          The last segment for which this information is applicable.

      *   **productCode **<mark style="color:blue;">**string**</mark>

          Unique identifier for the ancillary product.
      *   **productName **<mark style="color:blue;">**string**</mark>

          Ancillary product name.

          Options:
          
          StandardCheckInBaggage

          CabinBaggageOverheadLocker
      *   **productType **<mark style="color:blue;">**string**</mark>

          Ancillary product type.

          1: Standard Check-in baggage
          
          3: Cabin Baggage Overhead Locker
          
          6: Seat

          Currently only "Standard Check-in Baggage" and "Cabin Baggage Overhead Locker" are available.

      *   **canPurchaseWithTicket **<mark style="color:blue;">**int**</mark>

          This ancillary product can be purchased during the booking flow.

          1=Yes

          0=No

      *   **canPurchasePostTicket **<mark style="color:blue;">**int**</mark>

          This ancillary product can be purchased in the post-ticketing flow.

          1=Yes

          0=No
          
      *   **price **<mark style="color:blue;">**string**</mark>

          Price for this ancillary.
      *   **currency **<mark style="color:blue;">**string**</mark>

          Currency for this ancillary price.

      *   **vendorPrice **<mark style="color:blue;">**string**</mark>

          The price charged by the vendor for the ancillary.  Only when supportCreditTransPayment=1, there is a value.

      *   **vendorCurrency **<mark style="color:blue;">**string**</mark>

          The currency in which the vendor charges for the ancillary.

      *   **offerId **<mark style="color:blue;">**string**</mark>

          Reserved field, temporarily null
          
      *   **maxQty **<mark style="color:blue;">**int**</mark>

          Maximum purchase quantity per product
  
      *   **minQty **<mark style="color:blue;">**int**</mark>

          Minimum purchase quantity per product
          
      *   **categoryCode **<mark style="color:blue;">**string**</mark>

          Ancillary category code.
          
      *   **categoryCode **<mark style="color:blue;">**string**</mark>

          Ancillary code.

     * **`auxBaggageElement` Object<**[**AuxBaggageElement**](search.md#10.-auxbaggage-element-schema)**>**
       
     * **`auxBaggageElement` includes the following parameters**
       
    *   **`piece`  **<mark style="color:blue;">**int**</mark>

        0：No Limitation about piece;

        \>0：Maximum pieces
        
    *   **`weight`  **<mark style="color:blue;">**int**</mark>

        Value mentions maximum weight for ancillary baggage; this should be greater than 0.
        
    *   **`isAllWeight`  **<mark style="color:blue;">**boolean**</mark>

        True：The weight is for all the pieces

        False：The weight is for each piece
        
    *   **`size`  **<mark style="color:blue;">**string**</mark>

        Maximum size for ancillary baggage

    *   **`maxQty`  **<mark style="color:blue;">**string**</mark>

        Maximum purchase quantity per product

    *   **`minQty`  **<mark style="color:blue;">**string**</mark>

        Starting purchase quantity per product

    *   **`ancillaryCode`  **<mark style="color:blue;">**string**</mark>

    The code for this ancillary option. This will be identical to the `productCode`.  

{% endtab %}

{% tab title="Samples" %}
```json
{
    "status": 0,
    "msg": "success",
    "sessionId": "cde38a72-d7fa-4e5b-9ba5-08b6929143c8",
    "ticketOrderNo": "TESTM20240520171341468",
    "supportCreditTransPayment": "0",
    "currency": "USD",
    "fromSegments": [
        {
            "segmentIndex": 1,
            "carrier": "G9",
            "flightNumber": "G9101",
            "depAirport": "SHJ",
            "depTime": "202405230810",
            "arrAirport": "BAH",
            "arrTime": "202405230820",
            "stopCities": "",
            "duration": 70,
            "codeShare": false,
            "cabin": "",
            "cabinClass": 1,
            "seatCount": 2,
            "aircraftCode": "320",
            "depTerminal": "",
            "arrTerminal": "",
            "operatingCarrier": "G9",
            "operatingFlightnumber": "",
            "fareFamily": "Value"
        }
    ],
    "retSegments": [
        {
            "segmentIndex": 2,
            "carrier": "G9",
            "flightNumber": "G9104",
            "depAirport": "BAH",
            "depTime": "202405291750",
            "arrAirport": "SHJ",
            "arrTime": "202405292000",
            "stopCities": "",
            "duration": 70,
            "codeShare": false,
            "cabin": "",
            "cabinClass": 1,
            "seatCount": 2,
            "aircraftCode": "320",
            "depTerminal": "",
            "arrTerminal": "",
            "operatingCarrier": "G9",
            "operatingFlightnumber": "",
            "fareFamily": "lowest"
        }
    ],
    "ancillaryProductElements": [
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "AD_SCI_1PC_19KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 85.51,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 19,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 0,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "AD_SCI_1PC_19KG",
            "auxSeatElement": null,
            "displayPrice": 617.88,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "AD_SCI_2PC_38KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 171.01,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 38,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 0,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "AD_SCI_2PC_38KG",
            "auxSeatElement": null,
            "displayPrice": 1235.76,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "AD_SCI_3PC_57KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 256.52,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 57,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 0,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "AD_SCI_3PC_57KG",
            "auxSeatElement": null,
            "displayPrice": 1853.63,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "AD_SCI_1PC_19KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 85.51,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 19,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 0,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "AD_SCI_1PC_19KG",
            "auxSeatElement": null,
            "displayPrice": 617.88,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "AD_SCI_2PC_38KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 171.01,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 38,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 0,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "AD_SCI_2PC_38KG",
            "auxSeatElement": null,
            "displayPrice": 1235.76,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "AD_SCI_3PC_57KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 256.52,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 57,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 0,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "AD_SCI_3PC_57KG",
            "auxSeatElement": null,
            "displayPrice": 1853.63,
            "displayCurrency": "CNY"
        }
    ]
}
```
{% endtab %}
{% endtabs %}


