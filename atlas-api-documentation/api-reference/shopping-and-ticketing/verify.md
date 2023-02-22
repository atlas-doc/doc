# Verify

### Dependency

The `search` function should be called prior to this call.

### Endpoint {% debug uid="verify_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/verify.do](https://sandbox.atriptech.com/verify.do)

### Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
*   **routingIdentifier **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The unique identifier for a particular route.

    It is got from search response.
*   **requestSource **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The tag to identify which channel does this traffic come from.

    For example: SkyScanner,Google,Oganic search,etc…
{% endtab %}

{% tab title="Samples" %}
```
{
    "cid": "XXXXXXXX",
    "routingIdentifier": "Nvm0BG9VCGJRUPzvRCF2hU1okLJgXsVU46VwnmDdMe/JgpxanH/Xja3hYaj9X/EHLiR7QMsFKwl97AMIwqGNDbcG9kV3bXzylDL2dNM3c07PTcQ67WyTJvK9ITR1HmHC2t2K1gUJztkSI4hVwhMjOGZUlo8qqzhJ8N3Bzta2M87ijqfQHCXkoLAseTdGienIy33IOIIHB6aknLdpZrvz8tCOBxWuNSYc0RRhtNsZ2n31GEmT5TthTQ\u003d\u003d"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    1: request data format error 

    2: route is forbidden

    3: unauthorized access
*   **msg **<mark style="color:blue;">**string**</mark>

    Error message
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
*   **sessionId **<mark style="color:blue;">**string**</mark>

    The unique identifier for this verification.

    It is required when you call order function to make a reservation to identify which flight and fare the client is choosing.
*   **maxSeats **<mark style="color:blue;">**int**</mark>

    Remaining seats for the fare;

    Please refer this element and prevent the end-users to choose more passengers than seat count.
*   **routing Object<**[**Routing Element**](search.md#route-element-schema)**>**

    Route and fare details. The structure is also Routing Elements, same as search response
*   **bookingRequirement**                    **Object**<[<mark style="color:blue;">**Booking**</mark>](order.md#paxticketinfo-schema)<mark style="color:blue;">**Requirement**</mark>> <mark style="color:blue;"></mark>                                                           &#x20;

    The description for booking info schema.

    * [<mark style="color:blue;">**Booking**</mark>](order.md#paxticketinfo-schema)<mark style="color:blue;">**Requirement**</mark>
      * #### <mark style="color:blue;">passenger</mark>                  Object<[PassengerRequirement](order.md#PassengerElement)>&#x20;
        *   **passengerType        Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**

            *   **type**                   <mark style="color:blue;">**int**</mark>

            &#x20;    The data type of this element
            * **required**             <mark style="color:blue;">**boolean**</mark>

            &#x20;             Identify if this element is required during booking

            * **decription** <mark style="color:blue;">**string**</mark>

            &#x20;      The remark of this element for this booking
        * **name                         Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **gender                      Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **birthday                    Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **nationality                 Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **cardType                   Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **cardNum                   Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **cardExpired              Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**
        * **cardIssuePlace         Object<**<mark style="color:blue;">**RequirementSchema**</mark>**>**    

*   **priceChange**                    **Object**<mark style="color:blue;"></mark>

    **IsPriceChange **<mark style="color:blue;">**boolean**</mark>

    true: there is price change
    
    false: there is no price change
    
    **`originalAdultPrice`  **<mark style="color:blue;">**decimal**</mark>
    
    Original adult fare price returned in search response
    
    **`originalAdultTax`  **<mark style="color:blue;">**decimal**</mark>
    
    Original adult tax returned in search response
    
    **`originalChildPrice`  **<mark style="color:blue;">**decimal**</mark>
    
    Original child fare price returned in search response
    
    **`originalChildTax`  **<mark style="color:blue;">**decimal**</mark>
    
    Original child tax returned in search response
    
    **`originalInfantPrice`  **<mark style="color:blue;">**decimal**</mark>
    
    Original infant fare price returned in search response
    
    **`originalInfantTax`  **<mark style="color:blue;">**decimal**</mark>
    
    Original infant tax returned in search response

    **`newAdultPrice`  **<mark style="color:blue;">**decimal**</mark>
    
    Adult fare with price change (if any) returned in verify response
    
    **`newAdultTax`  **<mark style="color:blue;">**decimal**</mark>
    
    Adult tax with price change (if any) returned in verify response
    
    **`newChildPrice`  **<mark style="color:blue;">**decimal**</mark>
    
    Child fare with price change (if any) returned in verify response
    
    **`newChildTax`  **<mark style="color:blue;">**decimal**</mark>
    
    Child tax with price change (if any) returned in verify response
    
    **`newInfantPrice`  **<mark style="color:blue;">**decimal**</mark>
    
    Infant fare with price change (if any) returned in verify response
    
    **`newInfantTax`  **<mark style="color:blue;">**decimal**</mark>
    
    Infant tax with price change (if any) returned in verify response
    


{% endtab %}

{% hint style="info" %}

* When there is no price change, the "original" and the "new" price and tax will always be the same.
* When there is price change, there will be some difference between the "original" and the "new" price and tax.

{% endhint %}

{% tab title="Samples" %}
```
{
  "sessionId": "9ed33691-6206-4586-b820-ea8e76f03758",
  "maxSeats": 4,
  "routing": {
    "fid": "Q2vCtW07xIVPUnvQX-odWREezxt723uFPQ5POeBo_WU_4pINKYVzHAtQSR4WZpLPJAChqCWTNynhJ8eCw2Da7kNrwrVtO8SFT1J70F_qHVk87jvEzN4gD3sEslSjY0zt5wlLhYelVYhqa5xk4NRj6oexrWBYmoYuCgU9aZznwK4.",
    "routingIdentifier": "Rqm5iD5ukR+bovhnSCODSisQqE2cBRlV8fb4cE0ZtnXjpXCeYN0x70Wi/OrrKsi4t4VBuW0zlCP2zGNFjfHBTu2cZcQlg6fOENdgkWf8ucE7LnOZ2jrdvSJw3JrV/FBARM2pCR4tMysfFHDUdrDb0cB/OhhtNjqmvT8KAoKpp9kb3odPLqY8opUnmHKCBjTR/q7l7MasA/8DkHmUNiTUmAS3hIBeWxpqofk9iO+mWKXQ+KZle5uNlqTOVPSNSn2NKl2FPJH286I3WztFF9zLvGE78mZxEhWCgcKKXw8w47gFaj8kcIBaUt8++MzFJK5iD8u6aks8uiM5P+sUopihtSUmLGyzdjNUhETrBcqUZsIb+jUFp4tMg8B/OhhtNjqmdtsDeAKOofwb3odPLqY8opA0rUoeRSqe/q7l7MasA/+aH+TiiO66c71KJXIUgAPmYhzd+riQaiygc50TSMUHVFTI4pC51fkaK8k8waz0sMc3WztFF9zLvGE78mZxEhWCgcKKXw8w47gFaj8kcIBaUt8++MzFJK5iVm9DPdnQ0eSGicjw7/l1eEBm1ty895Fx+4mCjc52lZNzB1faPWypJLsNzIq0nSXl21hDjkqUK+k=",
    "supportCreditTransPayment": "1",
    "currency": "USD",
    "adultPrice": 181.12,
    "adultTax": 0,
    "childPrice": 181.12,
    "childTax": 0,
    "infantPrice": 0,
    "infantTax": 0,
    "infantAllowed": false,
    "transactionFeePerPax": 5.98,
    "transactionFee": 2.99,
    "transactionFeeMode": "PER_TICKET",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "carrier": "5J",
        "flightNumber": "5J273",
        "depAirport": "HKG",
        "depTime": "202303040925",
        "arrAirport": "MNL",
        "arrTime": "202303041145",
        "stopCities": "",
        "duration": 140,
        "codeShare": false,
        "cabin": "PA",
        "cabinClass": 1,
        "seatCount": 4,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "GO Basic"
      },
      {
        "carrier": "5J",
        "flightNumber": "5J451",
        "depAirport": "MNL",
        "depTime": "202303050430",
        "arrAirport": "ILO",
        "arrTime": "202303050555",
        "stopCities": "",
        "duration": 85,
        "codeShare": false,
        "cabin": "PA",
        "cabinClass": 1,
        "seatCount": 4,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "GO Basic"
      }
    ],
    "retSegments": [
      {
        "carrier": "5J",
        "flightNumber": "5J448",
        "depAirport": "ILO",
        "depTime": "202303060725",
        "arrAirport": "MNL",
        "arrTime": "202303060850",
        "stopCities": "",
        "duration": 85,
        "codeShare": false,
        "cabin": "PA",
        "cabinClass": 1,
        "seatCount": 4,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "GO Basic"
      },
      {
        "carrier": "5J",
        "flightNumber": "5J112",
        "depAirport": "MNL",
        "depTime": "202303061530",
        "arrAirport": "HKG",
        "arrTime": "202303061800",
        "stopCities": "",
        "duration": 150,
        "codeShare": false,
        "cabin": "PA",
        "cabinClass": 1,
        "seatCount": 4,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "GO Basic"
      }
    ],
    "combineIndexs": [],
    "rule": {
      "hasBaggage": 0,
      "baggageElements": [
        {
          "segmentNo": 1,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 0
        },
        {
          "segmentNo": 2,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 0
        },
        {
          "segmentNo": 3,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 0
        },
        {
          "segmentNo": 4,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 0
        }
      ],
      "refundRules": [
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "CNY",
          "refNoshow": "T",
          "refNoShowCondition": 48,
          "refNoshowFee": 0,
          "ruleList": []
        },
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "CNY",
          "refNoshow": "T",
          "refNoShowCondition": 48,
          "refNoshowFee": 0,
          "ruleList": []
        }
      ],
      "changesRules": [
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "CNY",
          "revNoshow": "T",
          "revNoShowCondition": 48,
          "revNoshowFee": 0,
          "ruleList": []
        },
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "CNY",
          "revNoshow": "T",
          "revNoShowCondition": 48,
          "revNoshowFee": 0,
          "ruleList": []
        }
      ]
    },
    "ancillaryProductElements": [
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 28.16,
        "currency": "USD",
        "vendorPrice": 1544.59,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 20,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_1PC_20KG"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_32KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 63.35,
        "currency": "USD",
        "vendorPrice": 3475.32,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 32,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_1PC_32KG"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 70.38,
        "currency": "USD",
        "vendorPrice": 3861.47,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 40,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_2PC_40KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 11.23,
        "currency": "USD",
        "vendorPrice": 616,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 20,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_1PC_20KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_32KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 24.7,
        "currency": "USD",
        "vendorPrice": 1355.2,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 32,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_1PC_32KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 31.44,
        "currency": "USD",
        "vendorPrice": 1724.8,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 40,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_2PC_40KG"
      },
      {
        "segmentIndex": 3,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 11.23,
        "currency": "USD",
        "vendorPrice": 616,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 20,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_1PC_20KG"
      },
      {
        "segmentIndex": 3,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_32KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 24.7,
        "currency": "USD",
        "vendorPrice": 1355.2,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 32,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_1PC_32KG"
      },
      {
        "segmentIndex": 3,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 31.44,
        "currency": "USD",
        "vendorPrice": 1724.8,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 40,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_2PC_40KG"
      },
      {
        "segmentIndex": 4,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 22.06,
        "currency": "USD",
        "vendorPrice": 1210,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 20,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_1PC_20KG"
      },
      {
        "segmentIndex": 4,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_1PC_32KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 44.11,
        "currency": "USD",
        "vendorPrice": 2420,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 32,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_1PC_32KG"
      },
      {
        "segmentIndex": 4,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 56.14,
        "currency": "USD",
        "vendorPrice": 3080,
        "vendorCurrency": "PHP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 40,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_2PC_40KG"
      }
    ],
    "vendorFare": {
      "vendorAdultPrice": 1.2,
      "vendorAdultTax": 0.8,
      "vendorChildPrice": 1.2,
      "vendorChildTax": 0.8,
      "vendorInfantPrice": 0,
      "vendorInfantTax": 0,
      "vendorCurrency": "PHP"
    },
    "bundleOptions": [],
    "links": [],
    "separateBookings": false
  },
  "bookingRequirement": {
    "passenger": {
      "cardIssuePlace": {
        "type": "string",
        "required": false,
        "description": null
      },
      "birthday": {
        "type": "string",
        "required": true,
        "description": null
      },
      "cardNum": {
        "type": "string",
        "required": false,
        "description": null
      },
      "passengerType": {
        "type": "int",
        "required": true,
        "description": null
      },
      "nationality": {
        "type": "string",
        "required": true,
        "description": null
      },
      "gender": {
        "type": "string",
        "required": true,
        "description": null
      },
      "cardExpired": {
        "type": "string",
        "required": false,
        "description": null
      },
      "cardType": {
        "type": "string",
        "required": false,
        "description": null
      },
      "name": {
        "type": "string",
        "required": true,
        "description": null
      }
    }
  },
  "priceChange": {
    "isPriceChange": false,
    "originalAdultPrice": 181.12,
    "originalAdultTax": 0,
    "originalChildPrice": 181.12,
    "originalChildTax": 0,
    "originalInfantPrice": 0,
    "originalInfantTax": 0,
    "newAdultPrice": 181.12,
    "newAdultTax": 0,
    "newChildPrice": 181.12,
    "newChildTax": 0,
    "newInfantPrice": 0,
    "newInfantTax": 0
  },
  "status": 0,
  "msg": "success"
}
```
{% endtab %}
{% endtabs %}
