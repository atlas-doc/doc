# Order

### Dependency

`Verify` function should be called in prior to this call.

### Endpoint {% debug uid="order_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/order.do](https://sandbox.atriptech.com/order.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **sessionId **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of the revalidation, got from revalidation response.
*   **passengers Array<**<mark style="color:blue;">**PassengerElement**</mark>**> **<mark style="color:green;">**Required**</mark>

    Passengers' information.

    * #### <mark style="color:blue;">**PassengerElement**</mark>
      *   **name **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          LastName/FirstName MiddleName.
      *   **passengerType **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

          0 ADT

          1 CHD
          
          2 INF
      *   **birthday **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Birthday, Format: YYYYMMDD
      *   **gender **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          M : Male

          F : Female
      *   **gender **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          M : Male

          F : Female
      *   **cardNum **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Passenger id card number
      *   **cardType **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Passenger id card type：

          PP - Passport

          GA - Hong Kong Macau Pass for China mainland citizens

          TW - Taiwan Pass for China mainland citizens

          TB - China mainland pass for Taiwanese

          HY - International Seaman's Certificate
      *   **cardIssuePlace **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Card issue country，IATA code of country
      *   **cardExpired **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Card expire date，Format：YYYYMMDD
      *   **nationality **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Nationality，IATA code of country
      *   **ancillaries Array<**<mark style="color:blue;">**AncillaryElement**</mark>**> **<mark style="color:green;">**Required**</mark>

          Ancillaries selection for the specific passenger

          * <mark style="color:blue;">**AncillaryElement**</mark>
            *   **productCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

                Ancillary product code;

                Got from routing element in the search/revalidation response.
            *   **segmentIndex **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

                Segment sequence
            *   **offerId **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

                unique identifier for this ancillary's offer.
*   **contact Object<**<mark style="color:blue;">**ContactElement**</mark>**> **<mark style="color:green;">**Required**</mark>

    Contact's information.

    * <mark style="color:blue;">**ContactElement**</mark>
      *   **name **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Contact name, please follow this format : LastName/FirstName MiddleName
      *   **address **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Contact address.
      *   **postcode **<mark style="color:orange;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

          Contact post code.
      *   **email **<mark style="color:orange;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

          Contact email.
      *   **mobile **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Contact mobile, please follow this format : XXXX(digital country code)-XXXXXXXX(phone number), here're the examples: 0001-87291810, 0086-13928109091, 0971-19201998
*   **requestSource **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    The tag to identify which channel does this traffic come from.
    
*   **useAtlasMailForContact **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    The tag denoting whether to use Atlas email id for contact information.
    
    true: Use Atlas email as contact email.
    
    false: Use customer email as contact email.
    
{% endtab %}

{% tab title="Samples" %}
```
{
    "sessionId": "43c3c07e-2b05-4fc9-8832-29a71075a097",
    "passengers": [
        {
            "name": "TEST/ONE",
            "passengerType": 0,
            "birthday": "19900101",
            "gender": "M",
            "cardNum": "00000001",
            "cardType": "PP",
            "cardIssuePlace": "SG",
            "cardExpired": "20301231",
            "nationality": "SG",
            "ancillaries":[ 
                { 
                "productCode":"BAG_5J_PH-PH_1_1P_20KG", 
                "segmentIndex":1 
                } 
            ]
        },
        {
            "name": "YAO/SAHA",
            "passengerType": 1,
            "birthday": "20140101",
            "gender": "F",
            "cardNum": "00000001",
            "cardType": "PP",
            "cardIssuePlace": "SG",
            "cardExpired": "20301231",
            "nationality": "SG",
            "ancillaries": []
        }
    ],
    "contact": {
        "name": "Way/Su",
        "address": null,
        "postcode": null,
        "email": "xxxxxxxxx@xxx.com",
        "mobile": "0065-81234567"
    },
    "requestSource": ""
    "useAtlasMailForContact":false
}
```
{% endtab %}
{% endtabs %}


{% hint style="info" %}
**VCC can also be used on round-trip itineraries combining 2 one-way fares. Check our FAQs for <mark style="color:blue;">**[Atlas API Order](../../faqs/atlas-order-api.md)**<mark style="color:blue;"></mark>**


{% endhint %}


## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    2: System error

    6: Price change
*   **msg **<mark style="color:blue;">**string**</mark>

    Error message
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
*   **sessionId **<mark style="color:blue;">**string**</mark>

    Same value got from order request
*   **duplicateOrders **<mark style="color:blue;">**string**</mark>

    Order number with which this order is a duplicate of. Please note that only orders created in the last 10 days will be checked for duplicate information.
*   **orderNo **<mark style="color:blue;">**string**</mark>

    Order number
*   **totalPrice **<mark style="color:blue;">**decimal**</mark>

    Total fare of this order in the currency TheAtlas settled with you.
*   **totalTransactionFee **<mark style="color:blue;">**decimal**</mark>

    Total technical fees for this order in the currency TheAtlas settled with you.
*   **currency **<mark style="color:blue;">**string**</mark>

    The currency TheAtlas settled with you.
*   **vendorTotalPrice **<mark style="color:blue;">**decimal**</mark>

    Total fare of this order in the vendor's currency, reference for you to generate the specific credit card.
*   **vendorCurrency **<mark style="color:blue;">**string**</mark>

    Vendor's currency.
*   **tktLimitTime **<mark style="color:blue;">**string**</mark>

    Payment deadline for this order. This time will be displayed in SGT (GMT +8)
*   **pnrCode **<mark style="color:blue;">**string**</mark>
    
    The pnrCode is the single reference for the booking. This is the Atlas PNR. 
*   **paxTicketInfos Array<**[**PAXTicketInfo**](order.md#paxticketinfo-schema)**>**

    Ticket information for passengers

    * #### [**PAXTicketInfo**](order.md#paxticketinfo-schema)
      *   **name **<mark style="color:blue;">**string**</mark>

          LastName/FirstName MiddleName.
      *   **passengerType **<mark style="color:blue;">**int**</mark>

          0 ADT

          1 CHD
          
          2 INF
      *   **birthday **<mark style="color:blue;">**string**</mark>

          Birthday, Format: YYYYMMDD
      *   **gender **<mark style="color:blue;">**string**</mark>

          M : Male

          F : Female
      *   **cardNum **<mark style="color:blue;">**string**</mark>

          Passenger id card number
      *   **cardType **<mark style="color:blue;">**string**</mark>

          Passenger id card type：

          PP - Passport

          GA - Hong Kong Macau Pass for China mainland citizens

          TW - Taiwan Pass for China mainland citizens

          TB - China mainland pass for Taiwanese

          HY - International Seaman's Certificate
      *   **cardIssuePlace **<mark style="color:blue;">**string**</mark>

          Card issue country，ISO code of country
      *   **cardExpired **<mark style="color:blue;">**string**</mark>

          Card expire date，Format：YYYYMMDD
      *   **nationality **<mark style="color:blue;">**string**</mark>

          Nationality，IATA code of country
      *   **ticketNos Array<**<mark style="color:blue;">**string**</mark>**>**

          Ticket numbers
      *   **airlinePNRs Array<**<mark style="color:blue;">**string**</mark>**>**

          AirlinePNRs. The array count would be the same as ticketnos count
      *   **ancillaries Array<**<mark style="color:blue;">**AncillaryElement**</mark>**>**

          Ancillaries selection for the specific passenger

          * [**AncillaryElement**](order.md#undefined)
            *   **productCode **<mark style="color:blue;">**string**</mark>

                Ancillary product code;

                Got from routing element in the search/revalidation response.
            *   **segmentIndex **<mark style="color:blue;">**int**</mark>

                Segment sequence
            *   **offerId **<mark style="color:blue;">**string**</mark>

                unique identifier for this ancillary's offer.
*   **routing Object<**[**RouteElement**](broken-reference/)**>**

    Route and fare details. The structure is also Routing Elements, same as search response
{% endtab %}

{% tab title="Samples" %}
```
{
    "sessionId": "57f7b429-bc89-40a6-af0a-af167c43a82a",
    "orderNo": "TESTJ20230825173736982",
    "originalOrderNo": null,
    "ticketOrderNo": null,
    "totalPrice": 30.48,
    "totalTransactionFee": 0.00,
    "currency": "USD",
    "vendorTotalPrice": 1.00,
    "vendorCurrency": "EUR",
    "tktLimitTime": "2023-08-25 18:27:37",
    "pnrCode": "KBAYFJ",
    "includeExtraBaggage": 0,
    "paxTicketInfos": [
        {
            "name": "shao/tingjun",
            "passengerType": 0,
            "birthday": "19910105",
            "gender": "M",
            "cardNum": "330226199101051272",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20220413",
            "nationality": "CN",
            "ticketNos": [],
            "airlinePNRs": [],
            "contactEmails": [
                "manuelafellingerfx@msbzt.com"
            ],
            "contactPhones": [
                "8615951711432"
            ],
            "ancillaries": []
        }
    ],
    "routing": {
        "fid": "UDkKJsajo9XeFOvIRI14RT95DeziNq3cn_J4LnfyL5kdu6x7i9Q_99hdb239v6gV",
        "routingIdentifier": "kAPir1gptfa5xmCdsTZkH0e0L9cI9MFKGLICoNRk9jLIVGY3uE7U493/BiSYU2lYCYz/vMhBJjNHxx29YKKVnhlP5EWT/YXfkAPir1gptfa5xmCdsTZkH0e0L9cI9MFKUr1HOLYbauVYHwhoJ64w9UbbRSb2DZWlomLeKoQjf3ruSK5qf8AFyAIvhcka7oKSgAEHSN0RzE2FAziTj5sTU3UVadMgeF6WNFV2qOZBL4neI0CpIreuFy0NtPb3+ogO2o5sQPlp/zC+QM0Tm/GivEWod/a+C7OjcFGi7UK0QapcR/CmLEcSQLDq2GUlevjzRSOPPgKYH2Qj8m9aeuwE1ABD6GWL+Qiy",
        "supportCreditTransPayment": "0",
        "supportPaymentMethods": [
            1
        ],
        "currency": "USD",
        "adultPrice": 30.05,
        "adultTax": 0.43,
        "childPrice": 30.05,
        "childTax": 0.43,
        "infantPrice": 38.12,
        "infantTax": 0.00,
        "infantAllowed": true,
        "transactionFeePerPax": 0.00,
        "transactionFee": 0.00,
        "transactionFeeMode": "PER_PAX",
        "nationalityType": 0,
        "nationality": "",
        "suitAge": "",
        "PaxType": "ADT",
        "fromSegments": [
            {
                "segmentIndex": 1,
                "carrier": "W4",
                "flightNumber": "W42849",
                "depAirport": "VIE",
                "depTime": "202309230605",
                "arrAirport": "NCE",
                "arrTime": "202309230755",
                "stopCities": "",
                "duration": 110,
                "codeShare": false,
                "cabin": "",
                "cabinClass": 1,
                "seatCount": 4,
                "aircraftCode": "",
                "depTerminal": "",
                "arrTerminal": "",
                "operatingCarrier": "",
                "operatingFlightnumber": "",
                "fareFamily": "Basic"
            }
        ],
        "retSegments": [],
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
                }
            ],
            "refundRules": [
                {
                    "refundType": 0,
                    "refundStatus": "T",
                    "refundFee": 0.0,
                    "currency": "EUR",
                    "refNoshow": "T",
                    "refNoShowCondition": 0,
                    "refNoshowFee": 0.0,
                    "ruleDetailList": [
                        {
                            "ruleId": 3036,
                            "status": "H",
                            "startMinute": 525600,
                            "endMinute": 20160,
                            "amount": 65.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3038,
                            "status": "H",
                            "startMinute": 20160,
                            "endMinute": 180,
                            "amount": 85.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3041,
                            "status": "T",
                            "startMinute": 180,
                            "endMinute": 0,
                            "amount": 0.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3044,
                            "status": "T",
                            "startMinute": 0,
                            "endMinute": -525600,
                            "amount": 0.0,
                            "currency": "EUR"
                        }
                    ],
                    "ruleList": null
                }
            ],
            "changesRules": [
                {
                    "changesType": 0,
                    "changesStatus": "T",
                    "changesFee": 0.0,
                    "currency": "EUR",
                    "revNoshow": "T",
                    "revNoShowCondition": 0,
                    "revNoshowFee": 0.0,
                    "ruleList": null,
                    "ruleDetailList": [
                        {
                            "ruleId": 3047,
                            "status": "H",
                            "startMinute": 525600,
                            "endMinute": 43200,
                            "amount": 35.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3049,
                            "status": "H",
                            "startMinute": 43200,
                            "endMinute": 10080,
                            "amount": 40.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3051,
                            "status": "H",
                            "startMinute": 10080,
                            "endMinute": 180,
                            "amount": 45.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3054,
                            "status": "T",
                            "startMinute": 180,
                            "endMinute": 0,
                            "amount": 0.0,
                            "currency": "EUR"
                        },
                        {
                            "ruleId": 3057,
                            "status": "T",
                            "startMinute": 0,
                            "endMinute": -525600,
                            "amount": 0.0,
                            "currency": "EUR"
                        }
                    ]
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
                "price": 40.22,
                "currency": "USD",
                "vendorPrice": 36.93,
                "vendorCurrency": "EUR",
                "clientTechnicalServiceFee": 0,
                "clientTechnicalServiceFeeMode": null,
                "auxBaggageElement": {
                    "piece": 1,
                    "weight": 10,
                    "isAllWeight": false,
                    "size": ""
                },
                "offerId": null,
                "maxQty": 1,
                "minQty": 1,
                "categoryCode": "StandardCheckInBaggage",
                "ancillaryCode": "SCI_1PC_10KG",
                "auxSeatElement": null
            },
            {
                "segmentIndex": 1,
                "endSegmentIndex": null,
                "productCode": "SCI_1PC_20KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 0,
                "price": 66.24,
                "currency": "USD",
                "vendorPrice": 60.82,
                "vendorCurrency": "EUR",
                "clientTechnicalServiceFee": 0,
                "clientTechnicalServiceFeeMode": null,
                "auxBaggageElement": {
                    "piece": 1,
                    "weight": 20,
                    "isAllWeight": false,
                    "size": ""
                },
                "offerId": null,
                "maxQty": 6,
                "minQty": 1,
                "categoryCode": "StandardCheckInBaggage",
                "ancillaryCode": "SCI_1PC_20KG",
                "auxSeatElement": null
            },
            {
                "segmentIndex": 1,
                "endSegmentIndex": null,
                "productCode": "SCI_2PC_40KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 0,
                "price": 132.47,
                "currency": "USD",
                "vendorPrice": 121.64,
                "vendorCurrency": "EUR",
                "clientTechnicalServiceFee": 0,
                "clientTechnicalServiceFeeMode": null,
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
                "ancillaryCode": "SCI_2PC_40KG",
                "auxSeatElement": null
            },
            {
                "segmentIndex": 1,
                "endSegmentIndex": null,
                "productCode": "SCI_1PC_26KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 0,
                "price": 68.42,
                "currency": "USD",
                "vendorPrice": 62.83,
                "vendorCurrency": "EUR",
                "clientTechnicalServiceFee": 0,
                "clientTechnicalServiceFeeMode": null,
                "auxBaggageElement": {
                    "piece": 1,
                    "weight": 26,
                    "isAllWeight": false,
                    "size": ""
                },
                "offerId": null,
                "maxQty": 6,
                "minQty": 1,
                "categoryCode": "StandardCheckInBaggage",
                "ancillaryCode": "SCI_1PC_26KG",
                "auxSeatElement": null
            },
            {
                "segmentIndex": 1,
                "endSegmentIndex": null,
                "productCode": "SCI_2PC_52KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 0,
                "price": 136.84,
                "currency": "USD",
                "vendorPrice": 125.66,
                "vendorCurrency": "EUR",
                "clientTechnicalServiceFee": 0,
                "clientTechnicalServiceFeeMode": null,
                "auxBaggageElement": {
                    "piece": 2,
                    "weight": 52,
                    "isAllWeight": true,
                    "size": ""
                },
                "offerId": null,
                "maxQty": 1,
                "minQty": 1,
                "categoryCode": "StandardCheckInBaggage",
                "ancillaryCode": "SCI_2PC_52KG",
                "auxSeatElement": null
            },
            {
                "segmentIndex": 1,
                "endSegmentIndex": null,
                "productCode": "SCI_1PC_32KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 0,
                "price": 71.61,
                "currency": "USD",
                "vendorPrice": 65.76,
                "vendorCurrency": "EUR",
                "clientTechnicalServiceFee": 0,
                "clientTechnicalServiceFeeMode": null,
                "auxBaggageElement": {
                    "piece": 1,
                    "weight": 32,
                    "isAllWeight": false,
                    "size": ""
                },
                "offerId": null,
                "maxQty": 6,
                "minQty": 1,
                "categoryCode": "StandardCheckInBaggage",
                "ancillaryCode": "SCI_1PC_32KG",
                "auxSeatElement": null
            },
            {
                "segmentIndex": 1,
                "endSegmentIndex": null,
                "productCode": "SCI_2PC_64KG",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 0,
                "price": 143.22,
                "currency": "USD",
                "vendorPrice": 131.52,
                "vendorCurrency": "EUR",
                "clientTechnicalServiceFee": 0,
                "clientTechnicalServiceFeeMode": null,
                "auxBaggageElement": {
                    "piece": 2,
                    "weight": 64,
                    "isAllWeight": true,
                    "size": ""
                },
                "offerId": null,
                "maxQty": 1,
                "minQty": 1,
                "categoryCode": "StandardCheckInBaggage",
                "ancillaryCode": "SCI_2PC_64KG",
                "auxSeatElement": null
            }
        ],
        "vendorFare": null,
        "bundleOptions": [],
        "links": [],
        "separateBookings": false,
        "refreshTime": null
    },
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}

#### Error codes

| Error code | Description         |
| ---------- | ------------------- |
| **`310`**  | Infant not allowed. |


Here is the API document formatted in a tabular format:

*API Document*
| Property | Type | Description |
| --- | --- | --- |
|<img width=200/>|<img width=200/>|<img width=500/>|
| cid | string | Unique identifier of the passenger |
| sessionId | string (uuid) | Session ID for tracking and monitoring |

### Passengers
| Property | Type | Description |
| --- | --- | --- |
|<img width=200/>|<img width=200/>|<img width=500/>|
| name | string | Passenger name |
| passengerType | integer | Passenger type: 0 = adult, 1 = child |
| birthday | string (date format) | Passenger birthday |
| gender | string (M/F) | Passenger gender |
| cardNum | string | Card number: bank card or credit card |
| cardType | string | Card type |
| cardIssuePlace | string | Location where the card was issued |
| cardExpired | string (date format) | Card expiration date |
| nationality | string (CN, US, EU) | Passenger nationality |
| ancillaries | array | Array of ancillary objects: |

### Ancillaries
| Property | Type | Description |
| --- | --- | --- |
|<img width=200/>|<img width=200/>|<img width=500/>|
| productCode | string | Ancillary product code |
| segmentIndex | integer | Segment index |

### Contact Information
| Property | Type | Description |
| --- | --- | --- |
|<img width=200/>|<img width=200/>|<img width=500/>|
| name | string | Contact name |
| address | null|string | Contact address |
| postcode | null|string | Contact postcode |
| email | string (email format) | Contact email |
| mobile | string (+86-XXXXX pattern) | Contact mobile phone number |

### Baggage Information
| Property | Type | Description |
| --- | --- | --- |
|<img width=200/>|<img width=200/>|<img width=500/>|
| baggagePiece | integer | Number of checked baggage pieces |
| baggageWeight |
