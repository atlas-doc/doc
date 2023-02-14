# Order

### Dependency

`Verify` function should be called in prior to this call.

### Endpoint {% debug uid="order_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/order.do](https://sandbox.atriptech.com/order.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
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
      *   **postcode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Contact post code.
      *   **email **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Contact email.
      *   **mobile **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          Contact mobile, please follow this format : XXXX(digital country code)-XXXXXXXX(phone number), here're the examples: 0001-87291810, 0086-13928109091, 0971-19201998
*   **requestSource **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    The tag to identify which channel does this traffic come from.
{% endtab %}

{% tab title="Samples" %}
```
{
    "cid": "XXXXXXXX",
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
        "name": "Way",
        "address": null,
        "postcode": null,
        "email": "xxxxxxxxx@xxx.com",
        "mobile": "0065-81234567"
    },
    "requestSource": ""
}
```
{% endtab %}
{% endtabs %}


{% hint style="info" %}
**VCC can also be used on round-trip itineraries combining 2 one-way fares. Check our FAQs for [<mark style="color:blue;">**Atlas API Order**</mark>](atlas-order-api.md)<mark style="color:blue;"></mark>.**


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

    Payment deadline for this order.
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

          Card issue country，IATA code of country
      *   **cardExpired **<mark style="color:blue;">**string**</mark>

          Card expire date，Format：YYYYMMDD
      *   **nationality **<mark style="color:blue;">**string**</mark>

          Nationality，IATA code of country
      *   **ticketNos Array<**<mark style="color:blue;">**string**</mark>**>**

          Ticket numbers
      *   **airlinePNRs Array<**<mark style="color:blue;">**string**</mark>**>**

          AirlinePNRs, the array count would be the same as ticketnos count
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
    "status":0,
    "msg":"success",
    "sessionId":"20e00a95-0eb1-44a4-b45c-ed358b12dc8a",
    "orderNo":"TBASP20220123212500763",
    "totalPrice":176.15,
    "totalTransactionFee":6.38,
    "currency":"CNY",
    "vendorTotalPrice":1411.24,
    "vendorCurrency":"PHP",
    "tktLimitTime":"2022-01-23 22:15:00",
    "pnrCode":"YO76ZF",
    "includeExtraBaggage":0,
    "paxTicketInfos":[
        {
            "name":"ZHAN/SAN LI",
            "passengerType":0,
            "birthday":"19731012",
            "gender":"M",
            "cardNum":"E00000000",
            "cardType":"PP",
            "cardIssuePlace":"HK",
            "cardExpired":"20240123",
            "nationality":"HK",
            "ticketNos":[

            ],
            "airlinePNRs":[

            ],
            "ancillaries":[

            ]
        }
    ],
    "routing":{
        "routingIdentifier":"fZLZw029cBVRUPzvRCF2hU1okLJgXsVUsFwV4I1Nrx0+IeBLujvH1Tviid634fozLt0sb7UwGvV/kRoSwhvTKJDn+QcARQ1JbBBBJK0aJ6FDZTnby0lKiPRJWJeAdVaqUxJV6TF0R3w4dtruLPIzETfWaFUbztP2R/Ld4H/wb88PYq34aqXFZDviid634fozLt0sb7UwGvV/kRoSwhvTKEDDCgG0Q21a16y8UbmfYUnBcsZk1oPoWGqjrFpf56gF",
        "supportCreditTransPayment":"0",
        "currency":"CNY",
        "adultPrice":103.14,
        "adultTax":73.01,
        "childPrice":103.14,
        "childTax":73.01,
        "InfantPrice":0,
        "InfantTax":0,
        "transactionFeePerPax":6.38,
        "nationalityType":0,
        "nationality":"",
        "suitAge":"",
        "PaxType":"ADT",
        "fromSegments":[
            {
                "carrier":"DG",
                "flightNumber":"DG6925",
                "depAirport":"CEB",
                "depTime":"202201251230",
                "arrAirport":"BXU",
                "arrTime":"202201251335",
                "stopCities":"",
                "duration":65,
                "codeShare":false,
                "cabin":"",
                "cabinClass":1,
                "seatCount":4,
                "aircraftCode":"AT7",
                "depTerminal":"",
                "arrTerminal":"",
                "operatingCarrier":"",
                "operatingFlightnumber":""
            }
        ],
        "retSegments":[

        ],
        "combineIndexs":[

        ],
        "rule":{
            "hasBaggage":0,
            "baggageElements":[
                {
                    "segmentNo":1,
                    "passengerType":0,
                    "baggagePiece":0,
                    "baggageWeight":0
                }
            ],
            "refundRules":[
                {
                    "refundType":0,
                    "refundStatus":"T",
                    "refundFee":0,
                    "currency":"CNY",
                    "refNoshow":"T",
                    "refNoShowCondition":48,
                    "refNoshowFee":0,
                    "ruleList":[

                    ]
                }
            ],
            "changesRules":[
                {
                    "changesType":0,
                    "changesStatus":"T",
                    "changesFee":0,
                    "currency":"CNY",
                    "revNoshow":"T",
                    "revNoShowCondition":48,
                    "revNoshowFee":0,
                    "ruleList":[

                    ]
                }
            ]
        },
        "ancillaryProductElements":[
            {
                "segmentIndex":1,
                "productCode":"BAG_DG_PH-PH_1_1P_20KG",
                "productName":"Baggage",
                "productType":1,
                "canPurchaseWithTicket":1,
                "canPurchasePostTicket":0,
                "price":59.51,
                "currency":"CNY",
                "auxBaggageElement":{
                    "piece":1,
                    "weight":20,
                    "isAllWeight":true
                }
            }
        ],
        "vendorFare":null
    }
}j
```
{% endtab %}
{% endtabs %}

#### Error codes

| Error code | Description         |
| ---------- | ------------------- |
| **`310`**  | Infant not allowed. |
