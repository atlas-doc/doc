# Search Ancillary

### Dependency

No preceding function needs to be carried out.
The order should be ticketed and the departure date should be in the future.

### Endpoint {% debug uid="searchAncillary_1.0" %}{% enddebug %}


[https://sandbox.atriptech.com/postBookingAncillarySearch.do](https://sandbox.atriptech.com/postBookingAncillarySearch.do)

{% hint style="info" %}
Please note the below "Rules & Restrictions" while initiating a post-ticketing transaction.

1. **Single Booking Limit:** Check-in baggage and Carry-on baggage can be added to the segment of passenger either in-booking or post-booking phase altogether or separately, but each type of baggage can only be added one time for the given segment throughout the whole flow. This rule aims to simplify the baggage booking flow for customers by sending the query only one time to book multiple baggages.

2. **Product Code:** "Product code" contains various baggage offerings in aspects of baggage pieces and weights for each airline.

3. **Restrictions for Infants:** Baggage ancillary is not allowed to be booked for infant passenger.

4. ** Post-Booking Baggage Additions:**
   It is not allowed to add the same type of post-booking baggage to a ticketed order the second time unless the first purchase fails in payment. Please refer to the below scenarios:

	a. When the post-booking order is in "ticket-in-process" and "ticketed" status, it's not allowed to order another one. If any query is called, API will respond with an error message.

	b. When the post-booking order is in "cancelled" status, the customer can create another order.

	c. When the post-booking order is in "unpaid" status, the customer can create another order. However, if one of the orders completes the payment and moves to "ticketing-in-process" status, the other orders will stop processing the payment.

5. **Existing Baggage Policies:** In case the air ticket order already contains free baggage, it’s subject to airline’s ancillary policy whether additional baggage is allowed to be purchase either at the booking flow or the post-booking flow.

6. **Consistent Product Codes in Connecting Flights:** Same “product code” for baggage is mandatory to be added to each segment in connecting flights. If the "product code" is different for each of the segment (in the same direction)  or not added for all the sectors, the API will respond with an error message.

7. **Round-Trip Baggage Rule:** Rule No.6 doesn't work for round trip flights. This means that the outbound and inbound segments can have different product codes. For example, outbound journey may have a product code of 1PC and 10KG while the inbound journey may have a product code of 20KG. This is allowed.

8. **API Request Information:** The details of only the passenger for whom the ancillary needs to be added must be sent in the API RQ.
{% endhint %}

**For "Order" status, please refer to the the response of the "queryOrderDetails.do" API.**

## Request

{% tabs %}
{% tab title="Schema" %}
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It is the original order number.
*   **airlinePNR **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    The record locator of the airline.
*   **carrier **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    2 character IATA airline code.
*   **ancillaryCategory **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Ancillary Category. Different categories of ancillaries need to be separately requested. Currently we only support "BAGGAGE".
*   **displayCurrency ** <mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

The alternative currency in which the fare and taxes amount needs to be displayed. The 3-letter currency code should be entered. 
    
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "xxxxxxxxxx",
    "ticketOrderNo": "TESTA20240618162411631",
    "airlinePNR": "S74883",
    "carrier": "MM",
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
    "sessionId": "90223f62-fd87-45b4-9a32-68f03f9f85c8",
    "ticketOrderNo": "TESTA20240618162411631",
    "supportCreditTransPayment": "0",
    "currency": "USD",
    "fromSegments": [
        {
            "segmentIndex": 1,
            "carrier": "5F",
            "flightNumber": "5F617",
            "depAirport": "RMO",
            "depTime": "202408200810",
            "arrAirport": "LTN",
            "arrTime": "202408200940",
            "stopCities": "",
            "duration": 210,
            "codeShare": false,
            "cabin": "",
            "cabinClass": 1,
            "seatCount": 4,
            "aircraftCode": "",
            "depTerminal": "",
            "arrTerminal": "",
            "operatingCarrier": "5F",
            "operatingFlightnumber": "",
            "fareFamily": "LOYAL"
        }
    ],
    "retSegments": [
        {
            "segmentIndex": 2,
            "carrier": "5F",
            "flightNumber": "5F618",
            "depAirport": "LTN",
            "depTime": "202408251040",
            "arrAirport": "RMO",
            "arrTime": "202408251550",
            "stopCities": "",
            "duration": 190,
            "codeShare": false,
            "cabin": "",
            "cabinClass": 1,
            "seatCount": 4,
            "aircraftCode": "",
            "depTerminal": "",
            "arrTerminal": "",
            "operatingCarrier": "5F",
            "operatingFlightnumber": "",
            "fareFamily": "LOYAL"
        }
    ],
    "ancillaryProductElements": [
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_1PC_10KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 22.88,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 10,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_1PC_10KG",
            "auxSeatElement": null,
            "displayPrice": 165.89,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_1PC_20KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 46.20,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 20,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_1PC_20KG",
            "auxSeatElement": null,
            "displayPrice": 335.08,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_1PC_30KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 34.54,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 30,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_1PC_30KG",
            "auxSeatElement": null,
            "displayPrice": 250.48,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_2PC_20KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 74.58,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 2,
                "weight": 20,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_2PC_20KG",
            "auxSeatElement": null,
            "displayPrice": 540.86,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_2PC_40KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 49.81,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 2,
                "weight": 40,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_2PC_40KG",
            "auxSeatElement": null,
            "displayPrice": 361.21,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_2PC_60KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 124.11,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 2,
                "weight": 60,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_2PC_60KG",
            "auxSeatElement": null,
            "displayPrice": 900.09,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_30KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 105.16,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 3,
                "weight": 30,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_3PC_30KG",
            "auxSeatElement": null,
            "displayPrice": 762.70,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_60KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 132.01,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 3,
                "weight": 60,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_3PC_60KG",
            "auxSeatElement": null,
            "displayPrice": 957.38,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_90KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 184.19,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 3,
                "weight": 90,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_3PC_90KG",
            "auxSeatElement": null,
            "displayPrice": 1335.90,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 1,
            "endSegmentIndex": null,
            "productCode": "COL_BAG_1PC_10KG",
            "productName": "Cabin Baggage Overhead Lock",
            "productType": 3,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 22.71,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 10,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "CabinBaggageOverheadLocker",
            "ancillaryCode": "COL_BAG_1PC_10KG",
            "auxSeatElement": null,
            "displayPrice": 164.71,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_1PC_10KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 43.48,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 10,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_1PC_10KG",
            "auxSeatElement": null,
            "displayPrice": 315.33,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_1PC_20KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 39.93,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 20,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_1PC_20KG",
            "auxSeatElement": null,
            "displayPrice": 289.59,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_1PC_30KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 44.09,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 30,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_1PC_30KG",
            "auxSeatElement": null,
            "displayPrice": 319.73,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_2PC_20KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 89.28,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 2,
                "weight": 20,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_2PC_20KG",
            "auxSeatElement": null,
            "displayPrice": 647.49,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_2PC_40KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 81.05,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 2,
                "weight": 40,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_2PC_40KG",
            "auxSeatElement": null,
            "displayPrice": 587.84,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_2PC_60KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 141.74,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 2,
                "weight": 60,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_2PC_60KG",
            "auxSeatElement": null,
            "displayPrice": 1027.97,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_30KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 138.97,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 3,
                "weight": 30,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_3PC_30KG",
            "auxSeatElement": null,
            "displayPrice": 1007.90,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_60KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 98.49,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 3,
                "weight": 60,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_3PC_60KG",
            "auxSeatElement": null,
            "displayPrice": 714.30,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "SCI_BAG_3PC_90KG",
            "productName": "Standard Check-in Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 272.31,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 3,
                "weight": 90,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "StandardCheckInBaggage",
            "ancillaryCode": "SCI_BAG_3PC_90KG",
            "auxSeatElement": null,
            "displayPrice": 1974.96,
            "displayCurrency": "CNY"
        },
        {
            "segmentIndex": 2,
            "endSegmentIndex": null,
            "productCode": "COL_BAG_1PC_10KG",
            "productName": "Cabin Baggage Overhead Lock",
            "productType": 3,
            "canPurchaseWithTicket": 0,
            "canPurchasePostTicket": 1,
            "price": 22.04,
            "currency": "USD",
            "vendorPrice": null,
            "vendorCurrency": null,
            "clientTechnicalServiceFee": 0.00,
            "clientTechnicalServiceFeeMode": "PER_PAX",
            "auxBaggageElement": {
                "piece": 1,
                "weight": 10,
                "isAllWeight": true,
                "size": ""
            },
            "offerId": null,
            "maxQty": 1,
            "minQty": 1,
            "categoryCode": "CabinBaggageOverheadLocker",
            "ancillaryCode": "COL_BAG_1PC_10KG",
            "auxSeatElement": null,
            "displayPrice": 159.83,
            "displayCurrency": "CNY"
        }
    ]
}
```
{% endtab %}
{% endtabs %}


