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
    
    **originalAdultPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Original adult fare price returned in search response
    
    **originalAdultTax  **<mark style="color:blue;">**decimal**</mark>
    
    Original adult tax returned in search response
    
    **originalChildPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Original child fare price returned in search response
    
    **originalChildTax  **<mark style="color:blue;">**decimal**</mark>
    
    Original child tax returned in search response
    
    **originalInfantPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Original infant fare price returned in search response
    
    **originalInfantTax  **<mark style="color:blue;">**decimal**</mark>
    
    Original infant tax returned in search response

    **newAdultPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Adult fare with price change (if any) returned in verify response
    
    **newAdultTax  **<mark style="color:blue;">**decimal**</mark>
    
    Adult tax with price change (if any) returned in verify response
    
    **newChildPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Child fare with price change (if any) returned in verify response
    
    **newChildTax  **<mark style="color:blue;">**decimal**</mark>
    
    Child tax with price change (if any) returned in verify response
    
    **newInfantPrice  **<mark style="color:blue;">**decimal**</mark>
    
    Infant fare with price change (if any) returned in verify response
    
    **newInfantTax  **<mark style="color:blue;">**decimal**</mark>
    
    Infant tax with price change (if any) returned in verify response
    
{% hint style="info" %}

* When there is no price change, the "original" and the "new" price and tax will always be the same.
* When there is price change, there will be some difference between the "original" and the "new" price and tax.

{% endhint %}

{% endtab %}

{% tab title="Samples" %}
```
{
  "sessionId": "0f6910f8-c783-42f4-ac67-4751906dde25",
  "maxSeats": 4,
  "routing": {
    "fid": "E96Zg5Lr4XQxVimN0_rhFeZULZ_HVT5DXZo6cPTdQrVod3ISQRlb4thdb239v6gV",
    "routingIdentifier": "IMBJh2LCiGucW/2fPoF4vPMRYyg0zjCX46VwnmDdMe+jn0SjHfR2nG/JWOkMaBeWWIsuVjYLsQv13xKhBeLbwE+OXtZXPvGMcbZEyIAKEd5pLXkmEaA9RxxXgWMbFa51MbEoePQk+F98JWr+FZCMlvI1JfshB/COpA0pnET4vO6Q+ktZg054ffXhZ6XpCo+Xt//s2/Y+Gbmh1LfPd2+Th74lI3vzTq1WH22pZxHygsDsb9b6JP7TXUWOt8lGShg1XJv7Jub9r1Y9TKsg3AR+JBuzgqA3FKthJURHwnVOil1Ia8nu9EbyIN+JHhhjzxyG",
    "supportCreditTransPayment": "0",
    "currency": "USD",
    "adultPrice": 28.59,
    "adultTax": 16.17,
    "childPrice": 28.59,
    "childTax": 16.17,
    "infantPrice": 0,
    "infantTax": 0,
    "infantAllowed": false,
    "transactionFeePerPax": 1,
    "transactionFee": 1,
    "transactionFeeMode": "PER_PAX",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "carrier": "EC",
        "flightNumber": "EC7846",
        "depAirport": "STN",
        "depTime": "202304151930",
        "arrAirport": "AMS",
        "arrTime": "202304152135",
        "stopCities": "",
        "duration": 65,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 4,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "Standard"
      }
    ],
    "retSegments": [],
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
          "ruleList": [
            {
              "rowId": 1383,
              "gmtCreate": "Feb 17, 2023 11:33:21 AM",
              "gmtModified": "Feb 17, 2023 11:33:21 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "EC",
              "ruleType": "self_refund",
              "ruleName": "self_refund_EC_1_Qpg6I7",
              "ruleKey": "self_refund_EC_202302171133201",
              "priority": 10,
              "validBeginTime": "Oct 8, 2019 12:00:00 AM",
              "validEndTime": "Jun 9, 2333 11:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": null,
              "arrCountry": null,
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": 120,
              "timeRight": 360,
              "ruleExtend": {
                "ruleKey": "self_refund_EC_202302171133201",
                "canRefund": "N",
                "canChange": null,
                "canRefundTax": "N",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": null,
                "amountCurrency": null,
                "pricePercent": null,
                "priceItem": null,
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            }
          ]
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
        }
      ]
    },
    "ancillaryProductElements": [
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "CBOL_1PC_56*45*25CM",
        "productName": "CabinBaggageOverheadLocker",
        "productType": 3,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 16.16,
        "currency": "USD",
        "vendorPrice": 12.99,
        "vendorCurrency": "GBP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 0,
          "isAllWeight": true,
          "size": "56*45*25cm"
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "CabinBaggageOverheadLocker",
        "ancillaryCode": "CBOL_1PC_56*45*25CM"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_15KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 29.84,
        "currency": "USD",
        "vendorPrice": 23.99,
        "vendorCurrency": "GBP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 15,
          "isAllWeight": false,
          "size": ""
        },
        "offerId": null,
        "maxQty": 3,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_15KG"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_23KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 36.05,
        "currency": "USD",
        "vendorPrice": 28.99,
        "vendorCurrency": "GBP",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 23,
          "isAllWeight": false,
          "size": ""
        },
        "offerId": null,
        "maxQty": 3,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_23KG"
      }
    ],
    "vendorFare": null,
    "bundleOptions": [],
    "links": [
      {
        "kind": "terms",
        "link": "",
        "description": "Carrier terms and conditions"
      }
    ],
    "separateBookings": false
  },
  "bookingRequirement": {
    "passenger": {
      "birthday": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "cardIssuePlace": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "cardNum": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "passengerType": {
        "type": "int",
        "required": true,
        "description": null,
        "maxLength": null
      },
      "gender": {
        "type": "string",
        "required": true,
        "description": null,
        "maxLength": null
      },
      "nationality": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "cardExpired": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "name": {
        "type": "string",
        "required": true,
        "description": null,
        "maxLength": null
      },
      "cardType": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      }
    }
  },
  "priceChange": {
    "isPriceChange": false,
    "originalAdultPrice": 28.59,
    "originalAdultTax": 16.17,
    "originalChildPrice": 28.59,
    "originalChildTax": 16.17,
    "originalInfantPrice": 32.8,
    "originalInfantTax": 0,
    "newAdultPrice": 28.59,
    "newAdultTax": 16.17,
    "newChildPrice": 28.59,
    "newChildTax": 16.17,
    "newInfantPrice": 0,
    "newInfantTax": 0
  },
  "status": 0,
  "msg": "success"
}
```
{% endtab %}
{% endtabs %}
