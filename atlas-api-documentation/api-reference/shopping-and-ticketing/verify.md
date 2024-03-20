# Verify

### Dependency

The `search` function should be called prior to this call.

### Endpoint {% debug uid="verify_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/verify.do](https://sandbox.atriptech.com/verify.do)

### Request

{% tabs %}
{% tab title="Schema" %}
*   **routingIdentifier **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The unique identifier for a particular route.

    This is received from search response.

    Validity: 6 hrs

    **displayCurrency array **Optional

The alternative currency in which the fare and taxes amount needs to be displayed. The 3-letter currency code should be entered. Please refer to the "Highlights" section in fare search menu for further information.
*   **requestSource **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The tag to identify which channel does this traffic come from.

    For example: SkyScanner,Google,Oganic search,etc…
{% endtab %}

{% tab title="Samples" %}
```
{
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
  "sessionId": "e1ee90f2-6e38-4423-b018-081e7a0a877f",
  "maxSeats": 9,
  "routing": {
    "fid": "NNQPjln9io_VkVCLML-tV4uTWB1-bYVbwEbgbq1gwbbyIGmv3IQjvGArLc-kVkfqqonjuSrhTmd6q9tCSQ5JdEbgsLbAG9YqlESmEgnTm4P1GEmT5TthTQ..",
    "routingIdentifier": "EXsU8XSpfLYTSaQTVCjrJMJvG/ysDtKYfq1WIi9iKV3RuKGQWRYoLHwlk3d3nfx3CfcndJLEJ0OelZh4CJOznF9aTBiw3WJrCv1w5tPrnLqsrzEwGf6LU4JnimIHlZ8g9Mbw9o1UAsRxu28yDTH1sxCUiQXhe9aQqCnWwMFh28gA/nj6IKNh5/yz0GWbBL6s1yDekyABUkLWmuWriKG76AcSFeTleOVJEjXfFd3mUvpZJe1wsRs5TI/Nma2Sz/cOdhAjhrTIFnOMJEKInVplSW3JYquYRVlKPNaFSuoF5K7IHGWlTR0X2vJysOfDQQZWR7Qv1wj0wUrE1kfV4vUrurLMbC/8XlxjYBc7iz9giHkbTb9r/K5/eabN+BX2cuBjtcmNH0T9SwZdxpCXnsjGxdC6wjGifmzacvdkADFsgfWzqaR6+aEfwt4jQKkit64X8IoXcz9XqDadvtpoFyrQz1tXYb6UK8+doiventK1gdc8oJQnVwpWZPELvPlBkk4NAyGgJvlATBKELGGnovqHmndI9ffItZth6YPlLhv9P5f1GEmT5TthTQ==",
    "supportCreditTransPayment": "1",
    "currency": "USD",
    "adultPrice": 60.97,
    "adultTax": 20.68,
    "childPrice": 60.97,
    "childTax": 20.68,
    "infantPrice": 77.46,
    "infantTax": 0,
    "infantAllowed": true,
    "transactionFeePerPax": 0.65,
    "transactionFee": 0.65,
    "transactionFeeMode": "PER_TICKET",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "segmentIndex": 1,
        "carrier": "W6",
        "flightNumber": "W65001",
        "depAirport": "KRK",
        "depTime": "202403260600",
        "arrAirport": "LTN",
        "arrTime": "202403260735",
        "stopCities": "",
        "duration": 155,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 9,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "W6",
        "operatingFlightnumber": "",
        "fareFamily": "Basic"
      }
    ],
    "retSegments": [
      {
        "segmentIndex": 2,
        "carrier": "W6",
        "flightNumber": "W62002",
        "depAirport": "LTN",
        "depTime": "202404230815",
        "arrAirport": "KRK",
        "arrTime": "202404231140",
        "stopCities": "",
        "duration": 145,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 9,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "W6",
        "operatingFlightnumber": "",
        "fareFamily": "Basic"
      }
    ],
    "combineIndexs": [],
    "rule": {
      "hasBaggage": 1,
      "baggageElements": [
        {
          "segmentNo": 1,
          "baggageType": "CabinBaggageUnderSeat",
          "passengerType": 0,
          "baggagePiece": 1,
          "baggageWeight": -1,
          "baggageSize": "40*30*20cm"
        },
        {
          "segmentNo": 1,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 0,
          "baggageSize": ""
        },
        {
          "segmentNo": 2,
          "baggageType": "CabinBaggageUnderSeat",
          "passengerType": 0,
          "baggagePiece": 1,
          "baggageWeight": -1,
          "baggageSize": "40*30*20cm"
        },
        {
          "segmentNo": 2,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 0,
          "baggageSize": ""
        }
      ],
      "refundRules": [
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "EUR",
          "refNoshow": "T",
          "refNoShowCondition": 0,
          "refNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 2988,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 20160,
              "amount": 65,
              "currency": "EUR"
            },
            {
              "ruleId": 2990,
              "status": "H",
              "startMinute": 20160,
              "endMinute": 180,
              "amount": 85,
              "currency": "EUR"
            },
            {
              "ruleId": 2993,
              "status": "T",
              "startMinute": 180,
              "endMinute": 0,
              "amount": 0,
              "currency": "EUR"
            },
            {
              "ruleId": 2996,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "EUR"
            }
          ]
        },
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "EUR",
          "refNoshow": "T",
          "refNoShowCondition": 0,
          "refNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 2988,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 20160,
              "amount": 65,
              "currency": "EUR"
            },
            {
              "ruleId": 2990,
              "status": "H",
              "startMinute": 20160,
              "endMinute": 180,
              "amount": 85,
              "currency": "EUR"
            },
            {
              "ruleId": 2993,
              "status": "T",
              "startMinute": 180,
              "endMinute": 0,
              "amount": 0,
              "currency": "EUR"
            },
            {
              "ruleId": 2996,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "EUR"
            }
          ]
        }
      ],
      "changesRules": [
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "EUR",
          "revNoshow": "T",
          "revNoShowCondition": 0,
          "revNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 10153,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 43200,
              "amount": 40,
              "currency": "EUR"
            },
            {
              "ruleId": 10155,
              "status": "H",
              "startMinute": 43200,
              "endMinute": 10080,
              "amount": 45,
              "currency": "EUR"
            },
            {
              "ruleId": 10157,
              "status": "H",
              "startMinute": 10080,
              "endMinute": 180,
              "amount": 50,
              "currency": "EUR"
            },
            {
              "ruleId": 10160,
              "status": "T",
              "startMinute": 180,
              "endMinute": 0,
              "amount": 0,
              "currency": "EUR"
            },
            {
              "ruleId": 10163,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "EUR"
            }
          ]
        },
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "EUR",
          "revNoshow": "T",
          "revNoShowCondition": 0,
          "revNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 10153,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 43200,
              "amount": 40,
              "currency": "EUR"
            },
            {
              "ruleId": 10155,
              "status": "H",
              "startMinute": 43200,
              "endMinute": 10080,
              "amount": 45,
              "currency": "EUR"
            },
            {
              "ruleId": 10157,
              "status": "H",
              "startMinute": 10080,
              "endMinute": 180,
              "amount": 50,
              "currency": "EUR"
            },
            {
              "ruleId": 10160,
              "status": "T",
              "startMinute": 180,
              "endMinute": 0,
              "amount": 0,
              "currency": "EUR"
            },
            {
              "ruleId": 10163,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "EUR"
            }
          ]
        }
      ],
      "serviceElements": [
        {
          "hasFreeSeat": 0,
          "hasFreeMeal": 0
        },
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
        "productCode": "SCI_1PC_10KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 59.32,
        "currency": "USD",
        "vendorPrice": 235,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 10,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_10KG",
        "auxSeatElement": null,
        "displayPrice": 3316.95,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 90.62,
        "currency": "USD",
        "vendorPrice": 359,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 20,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_20KG",
        "auxSeatElement": null,
        "displayPrice": 5067.17,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 189.05,
        "currency": "USD",
        "vendorPrice": 749,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 40,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_40KG",
        "auxSeatElement": null,
        "displayPrice": 10571.89,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_3PC_60KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 289.76,
        "currency": "USD",
        "vendorPrice": 1148,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 3,
          "weight": 60,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_3PC_60KG",
        "auxSeatElement": null,
        "displayPrice": 16203.64,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_4PC_80KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 391.73,
        "currency": "USD",
        "vendorPrice": 1552,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 4,
          "weight": 80,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_4PC_80KG",
        "auxSeatElement": null,
        "displayPrice": 21905.97,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_5PC_100KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 495.97,
        "currency": "USD",
        "vendorPrice": 1965,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 5,
          "weight": 100,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_5PC_100KG",
        "auxSeatElement": null,
        "displayPrice": 27735.32,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_6PC_120KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 603.74,
        "currency": "USD",
        "vendorPrice": 2392,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 6,
          "weight": 120,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_6PC_120KG",
        "auxSeatElement": null,
        "displayPrice": 33762.29,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_26KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 92.89,
        "currency": "USD",
        "vendorPrice": 368,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 26,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_26KG",
        "auxSeatElement": null,
        "displayPrice": 5194.2,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_52KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 193.85,
        "currency": "USD",
        "vendorPrice": 768,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 52,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_52KG",
        "auxSeatElement": null,
        "displayPrice": 10840.07,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_3PC_78KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 297.08,
        "currency": "USD",
        "vendorPrice": 1177,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 3,
          "weight": 78,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_3PC_78KG",
        "auxSeatElement": null,
        "displayPrice": 16612.97,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_4PC_104KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 401.57,
        "currency": "USD",
        "vendorPrice": 1591,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 4,
          "weight": 104,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_4PC_104KG",
        "auxSeatElement": null,
        "displayPrice": 22456.44,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_5PC_130KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 508.34,
        "currency": "USD",
        "vendorPrice": 2014,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 5,
          "weight": 130,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_5PC_130KG",
        "auxSeatElement": null,
        "displayPrice": 28426.94,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_6PC_156KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 618.38,
        "currency": "USD",
        "vendorPrice": 2450,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 6,
          "weight": 156,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_6PC_156KG",
        "auxSeatElement": null,
        "displayPrice": 34580.94,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_32KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 96.67,
        "currency": "USD",
        "vendorPrice": 383,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 32,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_32KG",
        "auxSeatElement": null,
        "displayPrice": 5405.92,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_64KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 201.42,
        "currency": "USD",
        "vendorPrice": 798,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 64,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_64KG",
        "auxSeatElement": null,
        "displayPrice": 11263.51,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_3PC_96KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 308.44,
        "currency": "USD",
        "vendorPrice": 1222,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 3,
          "weight": 96,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_3PC_96KG",
        "auxSeatElement": null,
        "displayPrice": 17248.13,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_4PC_128KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 416.46,
        "currency": "USD",
        "vendorPrice": 1650,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 4,
          "weight": 128,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_4PC_128KG",
        "auxSeatElement": null,
        "displayPrice": 23289.2,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_5PC_160KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 526.76,
        "currency": "USD",
        "vendorPrice": 2087,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 5,
          "weight": 160,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_5PC_160KG",
        "auxSeatElement": null,
        "displayPrice": 29457.31,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_6PC_192KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 640.59,
        "currency": "USD",
        "vendorPrice": 2538,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 6,
          "weight": 192,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_6PC_192KG",
        "auxSeatElement": null,
        "displayPrice": 35823.03,
        "displayCurrency": "PHP"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "CBOL_1PC_10KG",
        "productName": "CabinBaggageOverheadLocker",
        "productType": 3,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 29.79,
        "currency": "USD",
        "vendorPrice": 118,
        "vendorCurrency": "PLN",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
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
        "ancillaryCode": "CBOL_1PC_10KG",
        "auxSeatElement": null,
        "displayPrice": 1665.54,
        "displayCurrency": "PHP"
      }
    ],
    "vendorFare": {
      "vendorAdultPrice": 241.53,
      "vendorAdultTax": 81.94,
      "vendorChildPrice": 241.53,
      "vendorChildTax": 81.94,
      "vendorInfantPrice": 306.88,
      "vendorInfantTax": 0,
      "vendorCurrency": "PLN"
    },
    "bundleOptions": [],
    "links": [
      {
        "kind": "terms",
        "link": "https://wizzair.com/en-gb/legal/general-conditions-of-carriage-for-passengers-and-baggage",
        "description": "Carrier terms and conditions"
      }
    ],
    "separateBookings": false,
    "refreshTime": null,
    "displayFare": {
      "currency": "PHP",
      "exchangeRate": 14.1146661,
      "adultPrice": 3408.69,
      "adultTax": 1156.24,
      "childPrice": 3408.69,
      "childTax": 1156.24,
      "infantPrice": 4330.77,
      "infantTax": 0
    }
  },
  "bookingRequirement": {
    "passenger": {
      "cardIssuePlace": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "birthday": {
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
      "nationality": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "gender": {
        "type": "string",
        "required": true,
        "description": null,
        "maxLength": null
      },
      "cardExpired": {
        "type": "string",
        "required": false,
        "description": null,
        "maxLength": null
      },
      "cardType": {
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
      }
    }
  },
  "priceChange": {
    "isPriceChange": false,
    "originalAdultPrice": 60.97,
    "originalAdultTax": 20.68,
    "originalChildPrice": 60.97,
    "originalChildTax": 20.68,
    "originalInfantPrice": 77.46,
    "originalInfantTax": 0,
    "newAdultPrice": 60.97,
    "newAdultTax": 20.68,
    "newChildPrice": 60.97,
    "newChildTax": 20.68,
    "newInfantPrice": 77.46,
    "newInfantTax": 0
  },
  "status": 0,
  "msg": "success"
}
```
{% endtab %}
{% endtabs %}
