# Add Ancillaries

Currently, Atlas API only supports checked-in baggage service. We are looking to add more ancillaries soon.  

![](../../.gitbook/assets/FlowChart\_3\_AddAncillaries.png)

### 1. Get order details

The first step to adding ancillaries to an existing flight reservation is to request order details such as flight information, passenger details, fare and ancillary services (if bought at the time of booking). Ancillary services offered will vary depending on the airlines. Some of them may not even offer check-in baggage service. We will assume that the airline allows passengers to buy extra baggage service for this guide. 

EndPoint ：  [https://sandbox.atlaslovestravel.com/queryOrderDetails.do](https://sandbox.atlaslovestravel.com/queryOrderDetails.do)

Method : Post

Header:

```
x-atlas-client-id ： <Your clientid>
x-atlas-client-secret : <Your client secretid>
Content-Type: application/json
Accept-Encoding: gzip
```

{% tabs %}
{% tab title="Request" %}
```
{
    "cid": "XXXXXXXXX",
    "orderNo": "WNTND20220120210457331"
}
```


{% endtab %}

{% tab title="Response" %}
```
{
    "status": 0,
    "msg": "success",
    "orderNo": "WNTND20220120210457331",
    "pnrCode": "DMYCSX",
    "orderStatus": "2",
    "ticketStatus": "1",
    "paxTicketInfos": [
        {
            "name": "ZHANG/LU",
            "passengerType": 0,
            "birthday": "19920513",
            "gender": "M",
            "cardNum": "E12345678",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20201206",
            "nationality": "CN",
            "ticketNos": ["XIKJKR"],
            "airlinePNRs": ["XIKJKR"],
            "ancillaries": [
                {
                    "productCode": "SCI_BAG_5J_20KG_WULKSI",
                    "segmentIndex": 1,
                    "buyMethod": null,
                    "offerId": null
                }
            ]
        }
    ],
    "totalPrice": 31.49,
    "currency": "USD",
    "tktLimitTime": "2022-01-20 21:54:57",
    "vendorTotalPrice": 1550.76,
    "vendorCurrency": "PHP",
    "adultTotalFare": 31.49,
    "childTotalFare": 31.49,
    "totalTransactionFee": 8.00,
    "supportPaymentMethod": 3,
    "routing": {
        "routingIdentifier": "rSFlKG9ikyxRUPzvRCF2hU1okLJgXsVUGLICoNRk9jIQT+bahOw8GZFqz9jMd9Ty7J5nMreH0NQhzhRuhHZ/u60hZShvYpMsUVD870QhdoVNaJCyYF7FVIBYxaTAcvY4v49ZvrUyGhsuUjULPOhZvq3EoGJbhg7Nc+agmtqRchzQCfyHhHf3NQ+uno9Tp3T+PjbmgWB+nQYlgJXs7UOmuK6IbTFbCcnXkz/AGoWnjMwQr5TwVZmRMQ==",
        "supportCreditTransPayment": "1",
        "currency": "USD",
        "adultPrice": 16.46,
        "adultTax": 10.97,
        "childPrice": 16.46,
        "childTax": 10.97,
        "InfantPrice": 0,
        "InfantTax": 0,
        "transactionFeePerPax": 8.00,
        "nationalityType": 0,
        "nationality": "",
        "suitAge": "",
        "PaxType": "ADT",
        "fromSegments": [
            {
                "carrier": "5J",
                "flightNumber": "5J576",
                "depAirport": "CEB",
                "depTime": "202201251445",
                "arrAirport": "MNL",
                "arrTime": "202201251620",
                "stopCities": "",
                "duration": 95,
                "codeShare": false,
                "cabin": "",
                "cabinClass": 1,
                "seatCount": 4,
                "aircraftCode": "32Q",
                "depTerminal": "",
                "arrTerminal": "",
                "operatingCarrier": "",
                "operatingFlightnumber": ""
            }
        ],
        "retSegments": [],
        "combineIndexs": [],
        "rule": {
            "hasBaggage": 0,
            "baggageElements": [
                {
                    "segmentNo": 1,
                    "passengerType": 0,
                    "baggagePiece": 0,
                    "baggageWeight": 0
                }
            ],
            "refundRules": [
                {
                    "refundType": 0,
                    "refundStatus": "T",
                    "refundFee": 0.0,
                    "currency": "CNY",
                    "refNoshow": "T",
                    "refNoShowCondition": 48,
                    "refNoshowFee": 0.0,
                    "ruleList": []
                }
            ],
            "changesRules": [
                {
                    "changesType": 0,
                    "changesStatus": "T",
                    "changesFee": 0.0,
                    "currency": "CNY",
                    "revNoshow": "T",
                    "revNoShowCondition": 48,
                    "revNoshowFee": 0.0,
                    "ruleList": []
                }
            ]
        },
        "ancillaryProductElements": [
            {
                "segmentIndex": 1,
                "productCode": "SCI_BAG_5J_20KG_WULKSI",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 1,
                "price": 4.06,
                "currency": "USD",
                "auxBaggageElement": {
                    "piece": 0,
                    "weight": 20,
                    "isAllWeight": true
                },
                "offerId": null
            },
            {
                "segmentIndex": 1,
                "productCode": "SCI_BAG_5J_10KG_WULKSI",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 1,
                "price": 2.03,
                "currency": "USD",
                "auxBaggageElement": {
                    "piece": 0,
                    "weight": 10,
                    "isAllWeight": true
                },
                "offerId": null
            },
            {
                "segmentIndex": 1,
                "productCode": "SCI_BAG_5J_5KG_WULKSI",
                "productName": "StandardCheckInBaggage",
                "productType": 1,
                "canPurchaseWithTicket": 1,
                "canPurchasePostTicket": 1,
                "price": 1.02,
                "currency": "USD",
                "auxBaggageElement": {
                    "piece": 0,
                    "weight": 5,
                    "isAllWeight": true
                },
                "offerId": null
            }
        ],
        "vendorFare": {
            "vendorAdultPrice": 1350.76,
            "vendorAdultTax": 0,
            "vendorChildPrice": 1350.76,
            "vendorChildTax": 0,
            "vendorCurrency": "PHP"
        }
    },
    "itineraryDownload": "https://sandbox.atlaslovestravel.com/itineraryDownload.do?orderNo=m8iEobNffVcMxc0hFzJuXWQBp0V2yOzK"
}
```


{% endtab %}
{% endtabs %}

### 2. Get quotation for ancillaries&#x20;

Once your users have retrieved their order details, we can send the `orderNo` in the `searchAncillary` request  to fetch the complete list of ancillary services available. Currently, as we offer extra baggage only, the following example will mention `Baggage` as the `Product`**.** Please record the ancillary information with the `offerId` as the unique identifier.&#x20;

EndPoint ： [https://sandbox.atlaslovestravel.com/searchAncillary.do](https://sandbox.atlaslovestravel.com/searchAncillary.do)

Method : Post

Header:

```
x-atlas-client-id ： <Your clientid>
x-atlas-client-secret : <Your client secretid>
Content-Type: application/json
Accept-Encoding: gzip
```

{% tabs %}
{% tab title="Request" %}
```
{
    "cid": "XXXXXXXXX",
    "orderNo": "WNTND20220120210457331"
}
```


{% endtab %}

{% tab title="Response" %}
```
{
    "status": 0,
    "msg": "success",
    "orderNo": "PSTEV20220119165629057",
    "ancillaries": [
        {
            "segmentIndex": 1,
            "productCode": "SCI_BAG_5J_20KG_WULKSI",
            "productName": "Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 1,
            "canPurchasePostTicket": 1,
            "price": 4.06,
            "currency": "USD",
            "auxBaggageElement": {
                "piece": 0,
                "weight": 20,
                "isAllWeight": true
            },
            "offerId": "bf5072f01f694a0dae30b5554a795ff9"
        },
        {
            "segmentIndex": 1,
            "productCode": "SCI_BAG_5J_10KG_WULKSI",
            "productName": "Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 1,
            "canPurchasePostTicket": 1,
            "price": 2.03,
            "currency": "USD",
            "auxBaggageElement": {
                "piece": 0,
                "weight": 10,
                "isAllWeight": true
            },
            "offerId": "305833c8cfa445cb892df2bd2a21b464"
        },
        {
            "segmentIndex": 1,
            "productCode": "SCI_BAG_5J_5KG_WULKSI",
            "productName": "Baggage",
            "productType": 1,
            "canPurchaseWithTicket": 1,
            "canPurchasePostTicket": 1,
            "price": 1.02,
            "currency": "USD",
            "auxBaggageElement": {
                "piece": 0,
                "weight": 5,
                "isAllWeight": true
            },
            "offerId": "647b5c28808d4f52ac058e38eb3a908d"
        }
    ]
}
```


{% endtab %}
{% endtabs %}

### 3. Add extra bags&#x20;

Each ancillary service has a unique ID described as `offerId` and the `productCode` mentions the extra baggage weight selected. Add all chosen ancillaries and send the related `offerIds` and `productCode` along with order details. The `totalPrice` is the amount payable. The totalPrice is set to USD by default, but the amount owed is converted into the currency we settle with you, which is described by `vendorCurrency` and displayed to your customers.  &#x20;

EndPoint ： [https://sandbox.atlaslovestravel.com/orderAncillary.do](https://sandbox.atlaslovestravel.com/orderAncillary.do)

Method : Post

Header:

```
x-atlas-client-id ： <Your clientid>
x-atlas-client-secret : <Your client secretid>
Content-Type: application/json
Accept-Encoding: gzip
```

{% tabs %}
{% tab title="Request" %}
```
{
    "cid": "XXXXXXXX",
    "orderNo": "PSTEV20220119165629057",
    "passengers": [
        {
            "name": "ZHANG/LU",
            "passengerType": 0,
            "birthday": "19920513",
            "gender": "M",
            "cardNum": "E12345678",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20201206",
            "nationality": "CN",
            "ancillaries": [
                {
                    "segmentIndex": 1,
                    "offerId":"305833c8cfa445cb892df2bd2a21b464"
                }
            ]
        }
    ],
    "contact": {
        "name": "AA",
        "address": "shanghai",
        "postcode": "200120",
        "email": "",
        "mobile": "02181596986"
    },
    "baggagePiece": 0,
    "baggageWeight": 0
}
```


{% endtab %}

{% tab title="Response" %}
```
{
    "status": 0,
    "msg": null,
    "sessionId": null,
    "orderNo": "PSTEV20220119165629057ADCF",
    "originalOrderNo": "PSTEV20220119165629057",
    "totalPrice": 20.03,
    "totalTransactionFee": 0,
    "currency": "USD",
    "vendorTotalPrice": 1000.00,
    "vendorCurrency": "PHP",
    "tktLimitTime": "2022-01-23 18:59:45",
    "pnrCode": "B4WZFJ",
    "includeExtraBaggage": 0,
    "paxTicketInfos": [
        {
            "name": "ZHANG/LU",
            "passengerType": 0,
            "birthday": "19920513",
            "gender": "M",
            "cardNum": "E12345678",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20201206",
            "nationality": "CN",
            "ticketNos": [],
            "airlinePNRs": [],
            "ancillaries": [
                {
                    "productCode": "SCI_BAG_5J_10KG_WULKSI",
                    "segmentIndex": 1,
                    "buyMethod": null,
                    "offerId": null
                }
            ]
        }
    ],
    "routing": null
}
```


{% endtab %}
{% endtabs %}

### 4. Pay

When your customer confirms the card details and proceeds with payment, you need to send the new `orderNo` in your request to process payment for the ancillary purchase transaction. 

EndPoint ： [https://sandbox.atlaslovestravel.com/pay.do](https://sandbox.atlaslovestravel.com/pay.do)

Method : Post

Header:

```
x-atlas-client-id ： <Your clientid>
x-atlas-client-secret : <Your client secretid>
Content-Type: application/json
Accept-Encoding: gzip
```

{% tabs %}
{% tab title="Request" %}
```
{
    "cid": "XXXXXXXX",
    "orderNo": "PSTEV20220119165629057AWAD",
    "supportCreditTransPayment": "2"
}
```


{% endtab %}

{% tab title="Response" %}
```
{
    "status": 0,
    "msg": "success"
}
```


{% endtab %}
{% endtabs %}

### 5. Addon order complete notification &#x20;

With Atlas, you can configure webhooks to automatically receive notifications about changes to any booking made by your customers. Adding ancillary services post reservation is one of the events for which you will receive the notification. Once you receive an `order.addonCompleted` event notification on your server, you can process and act on it as needed. &#x20;

EndPoint : The URL you configured to receive notifications&#x20;

Method : Post

{% tabs %}
{% tab title="Samples" %}
```
{
    "cid": "XXXXXXXX",
    "type": "order.addonComplete",
    "data":
    {
        "orderNo": "PSTEV20220119165629057AWAD",
        "orderStatus": "2",
        "paxTicketInfos": [
            {
                "name": "ZHANG/LU",
                "passengerType": 0,
                "birthday": "19920513",
                "gender": "M",
                "cardNum": "E12345678",
                "cardType": "PP",
                "cardIssuePlace": "CN",
                "cardExpired": "20201206",
                "nationality": "CN",
                "ticketNos": [],
                "airlinePNRs": [],
                "ancillaries": [
                    {
                        "productCode": "SCI_BAG_5J_5KG_WULKSI",
                        "segmentIndex": 1,
                        "buyMethod": null,
                        "offerId": null,
                        "ancillaryEMD": "XIKJKR" 
                    }
                ]
            }
        ]
    }  
}
```


{% endtab %}
{% endtabs %}
