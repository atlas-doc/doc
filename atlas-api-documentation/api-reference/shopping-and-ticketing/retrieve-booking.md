# Retrieve Booking

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="queryOrderDetails_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/queryOrderDetails.do](https://sandbox.atriptech.com/queryOrderDetails.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo": "ZNMKU20220119160129691"
}             
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: success

    2: System error
*   **msg **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Error message
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number
*   **orderStatus **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: Unpaid

    1: Ticketing-in-Process

    2: Ticketed
    
    \-3: Cancelled(When the booking is failed due to the request information)
*   **ticketStatus **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: Ticket not issued

    1: Ticket issued
*   **ticketErrorCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    It's only available when orderStatus = -3.&#x20;

    Please check the definition of ticketErrorCode [**here**](../overview/errors.md#ticket-error-codes)****
*   **ticketErrorMessage **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    It's only available when orderStatus = -3.&#x20;

    Error message
*   **totalPrice **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total fare of this order in the currency TheAtlas settled with you.
*   **totalTransactionFee **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total technical fees for this order in the currency TheAtlas settled with you.
*   **currency **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The currency TheAtlas settled with you.
*   **vendorTotalPrice **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total fare of this order in the vendor's currency, reference for you to generate the specific credit card.
*   **vendorTotalAncillaryPrice **<mark style="color:blue;">**decimal**</mark>** 

    Total ancillary fare of this order in the vendor's currency.
*   **vendorCurrency **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Vendor's currency.
*   **supportPaymentMethod **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    1: Prepayment Only

    3: Both Credit Card Payment and Prepayment Available
*   **tktLimitTime **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Payment deadline for this order. This time will be displayed in SGT (GMT +8)
*   **paxTicketInfos Array<**[**PAXTicketInfo**](order.html#paxticketinfo-schema/)**> **<mark style="color:green;">**Required**</mark>

    Ticket information for passengers, the same format as the PAXTicketInfo in order response.
*   **routing Object<**[**RouteElement**](search.html#route-element-schema/)**> **<mark style="color:green;">**Required**</mark>

    Route and fare details. The structure is the same format as "Routing Element" in search response.
*   **airlineBookings Array<**[**ManageBookingElement**](broken-reference/)**> **<mark style="color:green;">**Required**</mark>

    Booking information for airline.    
    
{% endtab %}

{% tab title="Samples" %}
```
{
  "orderNo": "AUASC20240105124643947",
  "pnrCode": "EROERL",
  "orderStatus": "2",
  "ticketStatus": "1",
  "paxTicketInfos": [
    {
      "name": "PLAKHUTIN/PAVEL",
      "passengerType": 0,
      "birthday": "19830630",
      "gender": "M",
      "cardNum": "761223505",
      "cardType": "PP",
      "cardIssuePlace": "RU",
      "cardExpired": "20290730",
      "nationality": "RU",
      "ticketNos": [
        "AQTBLW"
      ],
      "airlinePNRs": [
        "AQTBLW"
      ],
      "contactEmails": [
        "booking@clickavia.ru"
      ],
      "contactPhones": [
        "0007-4953747238"
      ],
      "ancillaries": [
        {
          "productCode": "SCI_BAG_15KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 13.18,
          "currency": "USD",
          "vendorPrice": 450,
          "vendorCurrency": "THB"
        }
      ]
    },
    {
      "name": "BOLSHAKOVA/ELENA",
      "passengerType": 0,
      "birthday": "19811223",
      "gender": "F",
      "cardNum": "764307091",
      "cardType": "PP",
      "cardIssuePlace": "RU",
      "cardExpired": "20310409",
      "nationality": "RU",
      "ticketNos": [
        "AQTBLW"
      ],
      "airlinePNRs": [
        "AQTBLW"
      ],
      "contactEmails": [
        "booking@clickavia.ru"
      ],
      "contactPhones": [
        "0007-4953747238"
      ],
      "ancillaries": [
        {
          "productCode": "SCI_BAG_15KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 13.18,
          "currency": "USD",
          "vendorPrice": 450,
          "vendorCurrency": "THB"
        }
      ]
    },
    {
      "name": "PLAKHUTIN/SERGEI",
      "passengerType": 0,
      "birthday": "20101020",
      "gender": "M",
      "cardNum": "766146418",
      "cardType": "PP",
      "cardIssuePlace": "RU",
      "cardExpired": "20311210",
      "nationality": "RU",
      "ticketNos": [
        "AQTBLW"
      ],
      "airlinePNRs": [
        "AQTBLW"
      ],
      "contactEmails": [
        "booking@clickavia.ru"
      ],
      "contactPhones": [
        "0007-4953747238"
      ],
      "ancillaries": [
        {
          "productCode": "SCI_BAG_15KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 13.18,
          "currency": "USD",
          "vendorPrice": 450,
          "vendorCurrency": "THB"
        }
      ]
    }
  ],
  "totalPrice": 232.77,
  "currency": "USD",
  "tktLimitTime": "2024-01-05 13:17:00",
  "vendorTotalPrice": null,
  "vendorTotalAncillaryPrice": null,
  "vendorCurrency": null,
  "adultTotalFare": 64.41,
  "childTotalFare": 64.41,
  "infantTotalFare": 0,
  "totalAncillaryPrice": 39.54,
  "totalTransactionFee": 4.5,
  "paymentFee": null,
  "supportPaymentMethod": 1,
  "supportPaymentMethods": [
    1,
    5
  ],
  "paymentMethod": 1,
  "routing": {
    "fid": "VTzCwR8iVdfTROQQOFc2gaSUs8cvAhhAPlzSTLnQOpu3o0ig8TwDWg..",
    "routingIdentifier": "MCxtl389GyrTSlnSN4jJXcsCtQweCS6KBTt9KkxsGo2Gmde2LeogQc0+mmXr60ifi2cmq5ZoD+875G7obwQf8wPELefpLcU2MCxtl389GyrTSlnSN4jJXcsCtQweCS6Kb+/fn97jQDRz/EhUHAhIrW8JIeYWuh/oa/RMHFGbBeoe/K8qmG98aeoG7eFOUM+mZGt2/3Sx+lLNPppl6+tIn4tnJquWaA/vO+Ru6G8EH/MhnTF2jV3NS+XT11EC/yfyX5nk43fqbjWhKrewARjdvs7Q1RfYtITfW3iItlLNNUhgd/U62DnWm1Zuj1kLywZ9b8II8Vbv7Vxb0Cf4lEcfCt+JHhhjzxyG",
    "supportCreditTransPayment": "0",
    "supportPaymentMethods": [
      1,
      5
    ],
    "currency": "USD",
    "adultPrice": 57.46,
    "adultTax": 6.95,
    "childPrice": 57.46,
    "childTax": 6.95,
    "infantPrice": 0,
    "infantTax": 0,
    "infantAllowed": false,
    "transactionFeePerPax": 1.5,
    "transactionFee": 1.5,
    "transactionFeeMode": "PER_PAX",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "segmentIndex": 1,
        "carrier": "DD",
        "flightNumber": "DD525",
        "depAirport": "HKT",
        "depTime": "202401111125",
        "arrAirport": "DMK",
        "arrTime": "202401111250",
        "stopCities": "",
        "duration": 85,
        "codeShare": false,
        "cabin": "V",
        "cabinClass": 1,
        "seatCount": 3,
        "aircraftCode": "738",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "NOK LITE"
      }
    ],
    "retSegments": [],
    "combineIndexs": [],
    "rule": {
      "hasBaggage": 1,
      "baggageElements": [
        {
          "segmentNo": 1,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 0,
          "baggageSize": ""
        },
        {
          "segmentNo": 1,
          "baggageType": "CabinBaggageOverheadLocker",
          "passengerType": 0,
          "baggagePiece": 1,
          "baggageWeight": 7,
          "baggageSize": "56*50*23cm"
        }
      ],
      "refundRules": [
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "USD",
          "refNoshow": "T",
          "refNoShowCondition": 0,
          "refNoshowFee": 0,
          "ruleDetailList": [],
          "ruleList": []
        }
      ],
      "changesRules": [
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "USD",
          "revNoshow": "T",
          "revNoShowCondition": 0,
          "revNoshowFee": 0,
          "ruleList": [],
          "ruleDetailList": []
        }
      ],
      "serviceElements": [
        {
          "hasFreeSeat": 0,
          "hasFreeMeal": 0
        }
      ]
    },
    "ancillaryProductElements": [
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_15KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 13.18,
        "currency": "USD",
        "vendorPrice": 450,
        "vendorCurrency": "THB",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 15,
          "isAllWeight": true,
          "size": ""
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_BAG_15KG",
        "auxSeatElement": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 14.65,
        "currency": "USD",
        "vendorPrice": 500,
        "vendorCurrency": "THB",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 20,
          "isAllWeight": true,
          "size": ""
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_BAG_20KG",
        "auxSeatElement": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_25KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 18.46,
        "currency": "USD",
        "vendorPrice": 630,
        "vendorCurrency": "THB",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 25,
          "isAllWeight": true,
          "size": ""
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_BAG_25KG",
        "auxSeatElement": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_30KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 29.29,
        "currency": "USD",
        "vendorPrice": 1000,
        "vendorCurrency": "THB",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 30,
          "isAllWeight": true,
          "size": ""
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_BAG_30KG",
        "auxSeatElement": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 35.15,
        "currency": "USD",
        "vendorPrice": 1200,
        "vendorCurrency": "THB",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 40,
          "isAllWeight": true,
          "size": ""
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_BAG_40KG",
        "auxSeatElement": null
      }
    ],
    "vendorFare": null,
    "bundleOptions": [],
    "links": null,
    "separateBookings": false,
    "refreshTime": null,
    "displayFare": null
  },
  "airlineBookings": [
    {
      "airlineCode": "DD",
      "airlineName": "Nok Air",
      "airlinePnr": "AQTBLW",
      "airlineWebSiteAddress": "https://www.nokair.com",
      "mmbEmail": "booking@clickavia.ru",
      "tailDigitsOfPaymentCard": null,
      "extras": [
        {
          "name": "email",
          "remark": "email",
          "value": "booking@clickavia.ru"
        }
      ]
    }
  ],
  "itineraryDownload": "https://api-sg.atriptech.com/itineraryDownload.do?orderNo=FtJs/8hfjlFZvedQEDnLooV3pGpEDoOm",
  "contact": {
    "name": "PLAKHUTIN/PAVEL",
    "address": null,
    "postcode": null,
    "email": "booking@clickavia.ru",
    "mobile": "0007-4953747238"
  },
  "ancillaryBuyMethod": "0",
  "errorCode": null,
  "errorMessage": null,
  "airlineMessage": null,
  "locale": "",
  "status": 0,
  "msg": "success"
}
```
{% endtab %}
{% endtabs %}
