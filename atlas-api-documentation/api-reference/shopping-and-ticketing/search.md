---
description: Create an order request to search for flights.
---

# Search

### Dependency

No preceding function needs to be called before `Search`.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/search.do](https://sandbox.atriptech.com/search.do)

{% hint style="info" %}
## Multi-currency Account
**To use a multi-currency account, you need to enter the "currency" tag in the "Search.do" API request.**

* "currency" is not mandatory. By default, the system will use the first currency set by the customer as the default quotation and settlement currency.
* In order to obtain quotes, issue tickets, and settle in currency you want, customers need to specify the currency at the beginning of the inquiry (search).
* There are no changes to the request parameters of other interfaces such as price verification, order generation, and payment. In the corresponding response content, the relevant settlement amount will be displayed in the currency specified by the customer.
* Transaction Fee Conversion: The transaction fee will be converted to the "settlement currency" as per the timestamp of the verify response as the verify response is the stage when the ticket price is quoted. 
* When using multiple currencies, you will receive statements and invoices separately for each currency. Please refer to the [Multi-currency account](https://resources.atriptech.com/popular-topics/payments/multi-currency-account) link for details.

{% endhint %}

{% hint style="info" %}
## Merchant of Record (MoR)

Unlike the traditional VCC pass-through system where an airline acts as the merchant to handle transactions, the Atlas MoR solution stands as the merchant on record. This means that Atlas directly processes credit card transactions, effectively managing the acquisition and providing our B2B clients with a seamless payment capability. This innovative service offers several key benefits:
- Enable credit card payments for deposit airlines
- Allow card payments as an alternative when deposit balances are insufficient

### Supported Currencies

The primary currencies our system collectively handles are USD, EUR, GBP, and SGD.

### Card types accepted by Atlas

- Amex
- Visa
- Mastercard
- JCB
- Discover
- DinersClub

### Fees for Atlas Merchant of Record (MoR)

|Item|Fees|
|----|----|
|Handling Fees for Card Acceptance - (Non-Amex) Corporate cards|3%|
|Handling Fees for Card Acceptance - (Amex) Corporate cards|5%|

### Points to note

- For MoR, Atlas will use the customer's default contract currency as the settlement currency for quoting.
- If customer's default contract currency is not supported by MOR, customer can request Atlas to config the currency they want to use for MOR transactions.
- “currency” cannot be arbitrarily specified. For example, if payment is made through deposit method, it must be in the currency of contract; If MOR is used, it must be the currency that Atlas is willing to collect from the customer's card.
- For MoR, Atlas limits the range of acquiring currencies for internal fund management purposes. It does not mean that customers can only use cards of the corresponding currency for payment.

For further information, please refer to the [Merchant of Record (MoR)](https://resources.atriptech.com/copy-of-capability/atlas-pay) document.

{% endhint %}

### Request

{% tabs %}
{% tab title="Schema" %}

**`tripType`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

1: Oneway

2: Return Trip

**`adultNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Adult passenger count, the number can be 1-9

**`childNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Child passenger count, the number can be 0-8

**`infantNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Infant passenger count, no more than the number of adult

**`fromCity`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

IATA Code of departure city or airport

**`toCity`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

IATA Code of arrival city or airport

**`fromDate`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Departure date, the format is YYYYMMDD

**`retDate`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Return date, the format is YYYYMMDD

Must not be earlier than fromDate. And it can be blank if tripType=1.

**`airlines`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

An array of IATA Codes of airlines. The result will only contain the airlines specified in the search request. A maximum of 5 airline codes can be added.

**`fromFlightNumbers`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Search for specified departure flights. Each element represents one flight. Connecting flight numbers are separated by "," (comma).

["FR123", "FR456,FR789"]

["FR123"]: A direct flight

["FR456,FR789"]: A connecting flight

**`retFlightNumbers`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Search for specified return flights. Each element represents one flight. Connecting flight numbers are separated by "," (comma).

["FR123", "FR456,FR789"]

["FR123"]: A direct flight

["FR456,FR789"]: A connecting flight

**`includeMultipleFareFamily`  **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Search only for the lowest fare or for the Fare Families.

False: lowest fare (default)

True: include fare families

**`currency`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

This is the settlement currency. The 3-letter currency code should be entered. This field is optional, and when you want to settle with Atlas in different currencies (especially when you have opened multiple deposit accounts in different currencies in Atlas), you need to use this parameter.

**`requestSource`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Identify the source of the search traffic, E.g. Google Flights, Oganic Search, SkyScanner.

{% endtab %}

{% tab title="Samples" %}
```
{
  "tripType": "2",
  "adultNum": 1,
  "childNum": 0,
  "infantNum": 0,
  "fromCity": "KRK",
  "toCity": "LTN",
  "fromDate": "20240326",
  "retDate": "20240423",
  "airlines": ["FR", "W6", "F9"],
  "fromFlightNumbers": ["FR123", "FR456"],
  "retFlightNumbers": ["FR123", "FR456"],
  "includeMultipleFareFamily": true
  "currency": "GBP",
  "requestSource": "Organic"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
**`status`  **<mark style="color:blue;">**int**</mark>

0: success

1: request data format error

2: route is forbidden

3: unauthorized access

**`msg`  **<mark style="color:blue;">**string**</mark>

Error message

The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to        check the result.

**`routings` Array <**[**Routing Element**](search.md#route-element-schema)**>**

The array of the routings include suitable flights and fares. Click [<mark style="color:red;">here</mark> ](search.md#route-element-schema)to check the schema.

{% endtab %}

{% tab title="Samples" %}
```
{
    "routings": [
        {
            "fid": "YFMzE-205XxX4bq6fXVMQGrqI6xEKfnKYp9yfgLMz2Yt50X935e_zV31cA29Wz4h",
            "routingIdentifier": "TE9OX1RDSV8xXzIwMjUwNzA3X18xXzBfMHxmb25scjY3MTY4fDF8MTY4LjI5XzE2OC4yOV8yNS4yMF8xLjMwXzM2My4wOF9HQlB8TE9OX1RDSV8xXzIwMjUwNzA3X18xXzBfMF5TVE4tTFMxNjg5LS1URlMtMjAyNTA3MDcwNjAwLTIwMjUwNzA3MTAzMC1sb3ctMS1eMTY4LjI5XzE2OC4yOV8yNS4yMF8xLjMwXzM2My4wOF5BTFNBUElfQUxTXl5BTFMxTE9OVENJMjAwMjAyNTA3MDdeR0JQXjE2Ny4wMF4xNjcuMDBeMjUuMDB8MXwyMDI1MDUwNjExNTMxOXwwfDE3NDY1MDM1OTkwODZNT1pwaHx8fHx8MS4zMHw0fDB8fA==.wbuMz/oG9erz+sQxKmBnyhDPDvqLc+1kTCI74IoASdo=",
            "supportCreditTransPayment": "1",
            "supportPaymentMethods": [
                1,
                3
            ],
            "currency": "GBP",
            "adultPrice": 168.19,
            "adultTax": 0.10,
            "adultDetails": [
                {
                    "code": "farePrice",
                    "type": "base",
                    "amount": 168.19,
                    "description": ""
                },
                {
                    "code": "tax",
                    "type": "tax",
                    "amount": 0.10,
                    "description": ""
                }
            ],
            "childPrice": 168.19,
            "childTax": 0.10,
            "childDetails": [
                {
                    "code": "farePrice",
                    "type": "base",
                    "amount": 168.19,
                    "description": ""
                },
                {
                    "code": "tax",
                    "type": "tax",
                    "amount": 0.10,
                    "description": ""
                }
            ],
            "infantPrice": 25.20,
            "infantTax": 0.00,
            "infantDetails": [
                {
                    "code": "farePrice",
                    "type": "base",
                    "amount": 25.20,
                    "description": ""
                },
                {
                    "code": "tax",
                    "type": "tax",
                    "amount": 0.00,
                    "description": ""
                }
            ],
            "infantAllowed": true,
            "transactionFeePerPax": 1.30,
            "transactionFee": 1.30,
            "transactionFeeMode": "PER_BOOKING",
            "nationalityType": 0,
            "nationality": "",
            "suitAge": "",
            "PaxType": "ADT",
            "fromSegments": [
                {
                    "segmentIndex": 1,
                    "carrier": "LS",
                    "flightNumber": "LS1689",
                    "depAirport": "STN",
                    "depTime": "202507070600",
                    "arrAirport": "TFS",
                    "arrTime": "202507071030",
                    "stopCities": "",
                    "duration": 270,
                    "codeShare": false,
                    "cabin": "",
                    "cabinClass": 1,
                    "seatCount": 2,
                    "aircraftCode": "",
                    "depTerminal": "",
                    "arrTerminal": "",
                    "operatingCarrier": "",
                    "operatingFlightnumber": "",
                    "fareFamily": "low"
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
                        "baggageWeight": 10,
                        "baggageSize": "56*45*25cm"
                    }
                ],
                "refundRules": [
                    {
                        "refundType": 0,
                        "refundStatus": "T",
                        "refundFee": 0.0,
                        "currency": "GBP",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 31451,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 31452,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "GBP"
                            }
                        ]
                    }
                ],
                "changesRules": [
                    {
                        "changesType": 0,
                        "changesStatus": "T",
                        "changesFee": 0.0,
                        "currency": "GBP",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 38876,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 300,
                                "amount": 40.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 38877,
                                "status": "T",
                                "startMinute": 300,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 38878,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "GBP"
                            }
                        ]
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
                    "productCode": "SCI_BAG_1PC_22KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 0,
                    "price": 40.82,
                    "currency": "GBP",
                    "vendorPrice": 40.50,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 22,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_22KG",
                    "auxSeatElement": null,
                    "displayPrice": null,
                    "displayCurrency": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_2PC_44KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 0,
                    "price": 81.63,
                    "currency": "GBP",
                    "vendorPrice": 81.00,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 2,
                        "weight": 44,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_2PC_44KG",
                    "auxSeatElement": null,
                    "displayPrice": null,
                    "displayCurrency": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_3PC_66KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 0,
                    "price": 122.44,
                    "currency": "GBP",
                    "vendorPrice": 121.50,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 3,
                        "weight": 66,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_3PC_66KG",
                    "auxSeatElement": null,
                    "displayPrice": null,
                    "displayCurrency": null
                }
            ],
            "vendorFare": {
                "vendorAdultPrice": 166.90,
                "vendorAdultTax": 0.10,
                "vendorChildPrice": 166.90,
                "vendorChildTax": 0.10,
                "vendorInfantPrice": 25.00,
                "vendorInfantTax": 0.00,
                "vendorCurrency": "GBP"
            },
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2025-05-06T00:20:23Z",
            "expireTime": "2025-05-06T03:53:19Z",
            "displayFare": null,
            "ancillarySupported": [
                "luggage"
            ],
            "cardChargeList": null
        },
        {
            "fid": "c37JvwiS0jOC91ssjHf3OsukxyXaya7VYp9yfgLMz2aizuCSAyKTrCxPN2bL4Lvk",
            "routingIdentifier": "TE9OX1RDSV8xXzIwMjUwNzA3X18xXzBfMHxmb25scjY3MTY4fDF8MTM5LjA3XzEzOS4wN18yNS4yMF8xLjMwXzMwNC42NF9HQlB8TE9OX1RDSV8xXzIwMjUwNzA3X18xXzBfMF5TVE4tTFMxNjYzLS1URlMtMjAyNTA3MDcxNTQwLTIwMjUwNzA3MjAwNS1sb3ctMS1eMTM5LjA3XzEzOS4wN18yNS4yMF8xLjMwXzMwNC42NF5BTFNBUElfQUxTXl5BTFMxTE9OVENJMjAwMjAyNTA3MDdeR0JQXjEzOC4wMF4xMzguMDBeMjUuMDB8MXwyMDI1MDUwNjExNTMxOXwwfDE3NDY1MDM1OTkwODZNT1pwaHx8fHx8MS4zMHw0fDB8fA==.o47oDBJ6WJj0FQW+DowgqR9MK/NiVDx54/zoh32l/xg=",
            "supportCreditTransPayment": "1",
            "supportPaymentMethods": [
                1,
                3
            ],
            "currency": "GBP",
            "adultPrice": 138.96,
            "adultTax": 0.11,
            "adultDetails": [
                {
                    "code": "farePrice",
                    "type": "base",
                    "amount": 138.96,
                    "description": ""
                },
                {
                    "code": "tax",
                    "type": "tax",
                    "amount": 0.11,
                    "description": ""
                }
            ],
            "childPrice": 138.96,
            "childTax": 0.11,
            "childDetails": [
                {
                    "code": "farePrice",
                    "type": "base",
                    "amount": 138.96,
                    "description": ""
                },
                {
                    "code": "tax",
                    "type": "tax",
                    "amount": 0.11,
                    "description": ""
                }
            ],
            "infantPrice": 25.20,
            "infantTax": 0.00,
            "infantDetails": [
                {
                    "code": "farePrice",
                    "type": "base",
                    "amount": 25.20,
                    "description": ""
                },
                {
                    "code": "tax",
                    "type": "tax",
                    "amount": 0.00,
                    "description": ""
                }
            ],
            "infantAllowed": true,
            "transactionFeePerPax": 1.30,
            "transactionFee": 1.30,
            "transactionFeeMode": "PER_BOOKING",
            "nationalityType": 0,
            "nationality": "",
            "suitAge": "",
            "PaxType": "ADT",
            "fromSegments": [
                {
                    "segmentIndex": 1,
                    "carrier": "LS",
                    "flightNumber": "LS1663",
                    "depAirport": "STN",
                    "depTime": "202507071540",
                    "arrAirport": "TFS",
                    "arrTime": "202507072005",
                    "stopCities": "",
                    "duration": 265,
                    "codeShare": false,
                    "cabin": "",
                    "cabinClass": 1,
                    "seatCount": 2,
                    "aircraftCode": "",
                    "depTerminal": "",
                    "arrTerminal": "",
                    "operatingCarrier": "",
                    "operatingFlightnumber": "",
                    "fareFamily": "low"
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
                        "baggageWeight": 10,
                        "baggageSize": "56*45*25cm"
                    }
                ],
                "refundRules": [
                    {
                        "refundType": 0,
                        "refundStatus": "T",
                        "refundFee": 0.0,
                        "currency": "GBP",
                        "refNoshow": "T",
                        "refNoShowCondition": 0,
                        "refNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 31451,
                                "status": "T",
                                "startMinute": 525600,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 31452,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "GBP"
                            }
                        ]
                    }
                ],
                "changesRules": [
                    {
                        "changesType": 0,
                        "changesStatus": "T",
                        "changesFee": 0.0,
                        "currency": "GBP",
                        "revNoshow": "T",
                        "revNoShowCondition": 0,
                        "revNoshowFee": 0.0,
                        "ruleDetailList": [
                            {
                                "ruleId": 38876,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": 300,
                                "amount": 40.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 38877,
                                "status": "T",
                                "startMinute": 300,
                                "endMinute": 0,
                                "amount": 0.0,
                                "currency": "GBP"
                            },
                            {
                                "ruleId": 38878,
                                "status": "T",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 0.0,
                                "currency": "GBP"
                            }
                        ]
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
                    "productCode": "SCI_BAG_1PC_22KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 0,
                    "price": 40.82,
                    "currency": "GBP",
                    "vendorPrice": 40.50,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 1,
                        "weight": 22,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_1PC_22KG",
                    "auxSeatElement": null,
                    "displayPrice": null,
                    "displayCurrency": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_2PC_44KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 0,
                    "price": 81.63,
                    "currency": "GBP",
                    "vendorPrice": 81.00,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 2,
                        "weight": 44,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_2PC_44KG",
                    "auxSeatElement": null,
                    "displayPrice": null,
                    "displayCurrency": null
                },
                {
                    "segmentIndex": 1,
                    "endSegmentIndex": null,
                    "productCode": "SCI_BAG_3PC_66KG",
                    "productName": "StandardCheckInBaggage",
                    "productType": 1,
                    "canPurchaseWithTicket": 1,
                    "canPurchasePostTicket": 0,
                    "price": 122.44,
                    "currency": "GBP",
                    "vendorPrice": 121.50,
                    "vendorCurrency": "GBP",
                    "clientTechnicalServiceFee": 0,
                    "clientTechnicalServiceFeeMode": null,
                    "auxBaggageElement": {
                        "piece": 3,
                        "weight": 66,
                        "isAllWeight": true,
                        "size": ""
                    },
                    "offerId": null,
                    "maxQty": 1,
                    "minQty": 1,
                    "categoryCode": "StandardCheckInBaggage",
                    "ancillaryCode": "SCI_BAG_3PC_66KG",
                    "auxSeatElement": null,
                    "displayPrice": null,
                    "displayCurrency": null
                }
            ],
            "vendorFare": {
                "vendorAdultPrice": 137.90,
                "vendorAdultTax": 0.10,
                "vendorChildPrice": 137.90,
                "vendorChildTax": 0.10,
                "vendorInfantPrice": 25.00,
                "vendorInfantTax": 0.00,
                "vendorCurrency": "GBP"
            },
            "bundleOptions": [],
            "links": null,
            "separateBookings": false,
            "refreshTime": "2025-05-06T00:20:23Z",
            "expireTime": "2025-05-06T03:53:19Z",
            "displayFare": null,
            "ancillarySupported": [
                "luggage"
            ],
            "cardChargeList": null
        }
    ],
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
**The search results will include a lot of items. Some highlights are:**

* The returned currency is by configuration according to the business agreement between you and Atlas.
* The total cost to purchase for a single adult passenger is: `adultPrice` + `adultTax` + `transactionFeePerPax`
* For the airlines which support pass through payment method, we would set `supportCreditTransPayment` to `1` and present the vendor's fare in the `vendorFare` element. Alternatively, if the airline doesn't support pass through payment method, we would set `supportCreditTransPayment` to `0` and the `vendorFare` element will be `null`.
* You can choose to show or hide `ancillaryProductElements` in search response, according to the configuration of each client in the backend system.
* The 'links' element will have the link to the terms and conditions of the airlines.
{% endhint %}

### Route Element Schema

{% tabs %}
{% tab title="Schema" %}
**`routingIdentifier`  **<mark style="color:blue;">**string**</mark>

This unique string identifier is used to verify requests for a particular route.

**`supportCreditTransPayment`  **<mark style="color:blue;">**string**</mark>

This tag is used to identify if the fare needs to be paid using the client's credit card. 

0: The credit card details will not be passed through and only pre-payment is allowed.

1: The API will allow you to pass through client’s credit card details for payment. The customer can also use pre-payment as a method of payment. 

**`supportPaymentMethods`  **<mark style="color:blue;">**string**</mark>

List of supported payment method identifiers.

Valid values:
  - 1: Deposit
  - 3: VCC Passthrough
  - 5: MOR 

**`currency`  **<mark style="color:blue;">**string**</mark>

The currency in which Atlas settles transactions with you.

**`adultPrice` **<mark style="color:blue;">**decimal**</mark>

Adult fare per passenger.

**`adultTax`  **<mark style="color:blue;">**decimal**</mark>

Adult tax per passenger.

**`adultDetails ` Array<**[**Price Details Element**]

Details of the adult price composition 

**`code`  **<mark style="color:blue;">**string**</mark>

Price detail code.

Valid values:

fareprice

tax

fee 

**`type`  **<mark style="color:blue;">**string**</mark>

Specific types of price detail, a price detail code has multiple types. 

**`amount`  **<mark style="color:blue;">**string**</mark>

Price detail amount. 

**`description`  **<mark style="color:blue;">**string**</mark>

Supplementary explanation for price details. 

**`childPrice`  **<mark style="color:blue;">**decimal**</mark>

Child fare per passenger.

**`childTax`  **<mark style="color:blue;">**decimal**</mark>

Child tax per passenger.

**`childDetails ` Array<**[**Price Details Element**]

Details of the adult price composition 

**`code`  **<mark style="color:blue;">**string**</mark>

Price detail code.

Valid values:

fareprice

tax

fee 

**`type`  **<mark style="color:blue;">**string**</mark>

Specific types of price detail, a price detail code has multiple types. 

**`amount`  **<mark style="color:blue;">**string**</mark>

Price detail amount. 

**`description`  **<mark style="color:blue;">**string**</mark>

Supplementary explanation for price details. 

**`InfantPrice`  **<mark style="color:blue;">**decimal**</mark>

Infant fare per passenger.

**`InfantTax`  **<mark style="color:blue;">**decimal**</mark>

Infant tax per passenger.

**`infantAllowed`  **<mark style="color:blue;">**boolean**</mark>

Infant passenger allowed for that airline.

**`infantDetails ` Array<**[**Price Details Element**]

Details of the adult price composition 

**`code`  **<mark style="color:blue;">**string**</mark>

Price detail code.

Valid values:

fareprice

tax

fee 

**`type`  **<mark style="color:blue;">**string**</mark>

Specific types of price detail, a price detail code has multiple types. 

**`amount`  **<mark style="color:blue;">**string**</mark>

Price detail amount. 

**`description`  **<mark style="color:blue;">**string**</mark>

Supplementary explanation for price details. 

**`transactionFeePerPax`  **<mark style="color:blue;">**decimal**</mark>

Technical service fee per passenger as per the signed contract.

**`transactionFee`  **<mark style="color:blue;">**decimal**</mark>

Technical service fee as per "transactionFeeMode".

**`transactionFeeMode`  **<mark style="color:blue;">**string**</mark>

The criteria of calculating the transaction fee as per the contractual agreement.

Transactio Fee Mode values:

PER_SEGMENT: Each segment of an itinerary (per passenger)

PER_TICKET: No. of tickets in a booking

PER_PAX: Per passenger

PER_BOOKING: Per atlas booking (order #)

**`nationalityType`  **<mark style="color:blue;">**int**</mark>

Nationality limitation values

0 No Limitation (optional)

1 Allowed (required)

2 Forbidden (not to be entered)

**`nationality`  **<mark style="color:blue;">**string**</mark>

This is the nationality of the passenger. Pass the IATA country code and use a comma if there is more than one country.

**`suitAge`  **<mark style="color:blue;">**string**</mark>

Deprecated Field. Ignore it.

**`paxType`  **<mark style="color:blue;">**string**</mark>

Currently, only ADT fare is available.

**`fromSegments` Array<**[**Segment Element**](search.md#3.-segment-element-schema)**>**

For outbound segments, click [<mark style="color:red;">**here**</mark> ](search.md#segment-element-schema)to check the schema.

**`retSegments` Array<**[**Segment Element**](search.md#3.-segment-element-schema)**>**

For inbound segments, click [<mark style="color:red;">**here**</mark> ](search.md#segment-element-schema)to check the schema.

**`rule` Object<**[**Rule Element**](search.md#5.-rule-element-schema)**>**

Pass `RuleElement` info for every booking to include the standard details such as baggage allowance, refund rules , change rules and service for the selected airline. Click [<mark style="color:red;">**here**</mark> ](search.md#rule-element-schema)to check the schema.

**`ancillaryProductElements` Array<**[**Ancillary Product Element**](search.md#9.-ancillaryproduct-element-schema)**>**

Currently only checked-in and cabin baggage are available in ancillaries.

**`ancillaryProductElements` includes the following parameters:**

*   **`segmentIndex`  **<mark style="color:blue;">**int**</mark>

Segment sequence. Starts from 1. If it is return trip, sequence for outbound trip and inbound trip would be together.
    
*   **`endSegmentIndex`  **<mark style="color:blue;">**int**</mark>

The last segment for which this information is applicable.
    
*   **`productCode`  **<mark style="color:blue;">**string**</mark>

Unique identifier for the ancillary product. It would be used in the order request.
*   **`productName`  **<mark style="color:blue;">**string**</mark>

Ancillary product name.
*   **`productType`  **<mark style="color:blue;">**int**</mark>

Ancillary product type

1: Check-in baggage

3: Cabin Baggage Overhead Locker

Currently, only baggage is available.
    
*   **`canPurchaseWithTicket`  **<mark style="color:blue;">**int**</mark>

This ancillary product can be purchased during the booking flow. 
    
1=Yes; 0=No  
    
*   **`canPurchasePostTicket`  **<mark style="color:blue;">**int**</mark>

This ancillary product can be purchased in the post-ticketing flow. 
    
1=Yes; 0=No  
    
*   **`price`  **<mark style="color:blue;">**decimal**</mark>

Price for this ancillary.
    
*   **`currency`  **<mark style="color:blue;">**string**</mark>

The currency in which Atlas settles transactions with you.
    
*   **`vendorPrice`  **<mark style="color:blue;">**decimal**</mark>

The price charged by the vendor for the ancillary.
    
*   **`vendorCurrency`  **<mark style="color:blue;">**string**</mark>

The currency in which the vendor charges for the ancillary.
    
*   **`clientTechnicalServiceFee`  **<mark style="color:blue;">**decimal**</mark>

The service fee charged by Atlas for the purchase of the ancillary.
    
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
        
*   **`offerId`  **<mark style="color:blue;">**string**</mark>

The identifier of the offer of ancillary product. This will be "null" in the booking flow but will have an id in the post-ticketing flow.

*   **`maxQty`  **<mark style="color:blue;">**string**</mark>

Maximum purchase quantity per product

*   **`minQty`  **<mark style="color:blue;">**string**</mark>

Starting purchase quantity per product

*   **`ancillaryCode`  **<mark style="color:blue;">**string**</mark>

The code for this ancillary option. This will be identical to the `productCode`.

**`vendorFare` Object<**[**VendorFare Element**](search.md#4.-vendorfare-element-schema)**>**

To identify the vendor’s fare with vendor’s currency. It is only available when `supportCreditTransPayment` = 1.

[**VendorFare Element**](file://api-reference/shopping-and-ticketing/search#4.-vendorfare-element-schema)

*   **`vendorAdultPrice`  **<mark style="color:blue;">**decimal**</mark>

Adult fare per passenger in vendor’s currency.
*   **`vendorAdultTax`  **<mark style="color:blue;">**decimal**</mark>

Adult tax per passenger in vendor’s currency.
*   **`vendorChildPrice`  **<mark style="color:blue;">**decimal**</mark>

Child fare per passenger in vendor’s currency.
*   **`vendorChildTax`  **<mark style="color:blue;">**decimal**</mark>

Child tax per passenger in vendor’s currency.
*   **`vendorCurrency`  **<mark style="color:blue;">**string**</mark>

This is the currency in which your customers will do transaction with you.

**`separateBookings`  **<mark style="color:blue;">**boolean**</mark>

When the outbound and inbound of round trip need to be booked separately, it will be true.

**`expireTime`  **<mark style="color:blue;">**string**</mark>

Cache expiration time (UTC time). Please note that this time is estimated, which means Atlas may refresh the cache before or after that time. The format is: yyyy-MM-dd'T'HH: mm: ss-Z '

{% endtab %}
{% endtabs %}

### Segment Element Schema

{% tabs %}
{% tab title="Schema" %}
**`carrier`  **<mark style="color:blue;">**string**</mark>

IATA code of airline.

**`flightNumber`  **<mark style="color:blue;">**string**</mark>

Value denotes flight number. The format is: CA123 or TR021 or FR1290, the letters denote the carrier and the three/four-digit number that follows is the flight number.

**`depAirport`  **<mark style="color:blue;">**string**</mark>

IATA code of departure airport.

**`depTime`  **<mark style="color:blue;">**string**</mark>

Departure time of the flight. The format is ：yyyyMMddHHmm, 202203100300 means 10MAR2022 03:00

**`arrAirport`  **<mark style="color:blue;">**string**</mark>

IATA code of arrival airport.

**`arrTime`  **<mark style="color:blue;">**string**</mark>

Arrival time of the flight. The format is ：yyyyMMddHHmm, 202203100300 means 10MAR2022 03:00

**`stopCities`  **<mark style="color:blue;">**string**</mark>

Name of cities from where the passengers will take connecting flights. Include IATA code of cities and use a comma in case of multiple cities to separate transfer airports count is higher than 1. For example: CGK, SUB. Blank means non-stop flight.

**`duration`  **<mark style="color:blue;">**int**</mark>

The flying duration in minutes.

**`codeShare`  **<mark style="color:blue;">**boolean**</mark>

True : code share

False : Not code share

**`cabin`  **<mark style="color:blue;">**string**</mark>

Booking code for the fare. For the LCCs which do not provide cabin options, the cabin string will be blank.

**`cabinClass`  **<mark style="color:blue;">**int**</mark>

Service grade of the fare

1 : Economy

2 : Business

3 : First Class

4: Premium Economy

**`seatCount`  **<mark style="color:blue;">**int**</mark>

Remaining seats for the fare.

**`aircraftCode`  **<mark style="color:blue;">**string**</mark>

This value identifies the aircraft model, which is the IATA aircraft code. For example, Airbus A380 = 388, Airbus A350 = 351.

**`depTerminal`  **<mark style="color:blue;">**string**</mark>

Departure terminal.

**`arrTerminal`  **<mark style="color:blue;">**string**</mark>

Arrival terminal.

**`operatingCarrier`  **<mark style="color:blue;">**string**</mark>

Operating carrier. It is blank when `codeshare=false`

\`\`

**`operatingFlightnumber`  **<mark style="color:blue;">**string**</mark>

Operating flight number. It is blank when `codeshare=false`

**`fareFamily`  **<mark style="color:blue;">**string**</mark>

Fare Family as per the information received from the airline.

\`\`
{% endtab %}
{% endtabs %}

### Rule Element Schema

{% tabs %}
{% tab title="Schema" %}
**`hasBaggage`  **<mark style="color:blue;">**int**</mark>

This tag is used to identify if the fare includes free checked-in or cabin baggage.

0: Not included

1: Included

**`BaggageElements` Array<**<mark style="color:blue;">**BaggageElement**</mark>**>**

Free checked-in or cabin baggage information included in the fare.

[BaggageElement](file://api-reference/shopping-and-ticketing/search#6.-baggage-element-schema)

**`segmentNo`  **<mark style="color:blue;">**int**</mark>

Segment sequence, start from 1.

If it is roundtrip, sequence outbound and inbound will be together.

**`baggageType`  **<mark style="color:blue;">**string**</mark>

There are 4 options for baggage:

StandardCheckInBaggage: Standard Check-in Baggage.

CabinBaggage: Usually refers to the Cabin Baggage Overhead Locker. Transition value. It will gradually transition to CabinBaggageOverheadLocker.

CabinBaggageOverheadLocker: Cabin Baggage Overhead Locker.

CabinBaggageUnderSeat: Cabin Baggage Under Seat. Usually refers to the personal item.

**`passengerType` **<mark style="color:blue;">**int**</mark>**</mark>

0: ADT

1: CHD

2: INF

If search or verify requested for ADT only, then only ADT is returned.

If search or verify requested for ADT+CHD, then ADT and CHD are returned.

**`baggagePiece` **<mark style="color:blue;">**int**</mark>

Baggage pieces:

0: No limitation on the number of pieces

\>0: Maximum pieces

**`baggageWeight` **<mark style="color:blue;">**int**</mark>

Baggage Weight, in KGs is mentioned if the airline offers free baggage.

0 : No free baggage

-1: No limitation on weight. 

**`baggageSize` **<mark style="color:blue;">**string**</mark>

Baggage Size: 

length＊width＊height and units. eg. "56＊36＊23cm", "18＊14＊8inch". 

Or Total dimensions (length + width + height) of each piece. eg. "L+W+H<=158cm". 

Empty means no limitation.

**`refundRules` Array<**<mark style="color:blue;">**refundRules**</mark>**>**

This function is used to fetch the change rules of the selected airline. 

There is only one array for one way, and two arrays for round-trip.

The first array is for the outbound, and the second array is for the inbound.


**`refundType` **<mark style="color:blue;">**int**</mark>

0: Wholly unused ticket

1: Partially used ticket (For example, when the passenger has used an outbound flight and wants to refund an inbound flight.)

**`refundStatus` s**<mark style="color:blue;">**string**</mark>

Refund rule types (for the most restrictive condition):

T: Non refundable

H: Refundable with restrictions

F: Free for refund

**`refundFee` **<mark style="color:blue;">**decimal**</mark>

Refund fee (for the most restrictive condition):

If refundStatus = H, it should not be null

If refundStatus = T/F, it can be null

**`currency` **<mark style="color:blue;">**string**</mark>

The currency of airline's rule, if refundStatus = H, it should not be "null".

**`refNoshow` **<mark style="color:blue;">**string**</mark>

Refund status (for the most restrictive condition):

T: Non refundable

H: Refundable with restrictions

F: Free for refund

**`refNoShowCondition` **<mark style="color:blue;">**string**</mark>

Time before scheduled flight departure.

**`refNoshowFee` **<mark style="color:blue;">**string**</mark>

Total refund fee (for the most restrictive condition):

If refNoshow = H, it should not be "null".

This value includes the refund fee and no-show penalty

**`ruleList` Array<ruleList>**

For internal use only.

**`ruleDetailList` Array<ruleList>**

List of all rules. Inside the ruleList are detailed airline rules for time periods, while outside the ruleList are the strictest rules before and after Noshow.

**`ruleId` **<mark style="color:blue;">**int**</mark>

For internal use only. 

**`status` **<mark style="color:blue;">**string**</mark>

Refund rule types:

T: Non refundable

H: Refundable with restrictions

F: Free Refund 

**`startMinute` **<mark style="color:blue;">**int**</mark>

Starting time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.

**`endMinute` **<mark style="color:blue;">**int**</mark>

Ending time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.

**`amount` **<mark style="color:blue;">**decimal**</mark>

Refund fee.

**`currency` **<mark style="color:blue;">**string**</mark>

The currency of airline's rule. If refundStatus = H, it should not be "null".


**`changesRules` Array<**<mark style="color:blue;">**rchangesRules**</mark>**>**

This function is used to fetch the change rules of the selected airline. 

There is only one array for one way, and two arrays for round-trip.

The first array is for the outbound, and the second array is for the inbound.


**`changesType` **<mark style="color:blue;">**int**</mark>

Change flight type

0: Wholly unused ticket

1: Partially used ticket (For example. When the passenger has used an outbound flight and wants to change an inbound flight)

**`changesStatus` **<mark style="color:blue;">**string**</mark>

Change flight rule type (for the most restrictive condition):

T: Non changeable

H: Changeable with restrictions

F: Free flight change 

**`changesFee` **<mark style="color:blue;">**decimal**</mark>

Change flight fee (for the most restrictive condition):

If changesStatus = H, it should not be "null"

If changesStatus = T/F, it can be "null"

**`currency` **<mark style="color:blue;">**string**</mark>

The currency of airline's rule.

If changesStatus = H, it should not be "null"

**`revNoshow` **<mark style="color:blue;">**string**</mark>

Change flight rule (for the most restrictive condition):

T: Non changeable

H: Changeable with restrictions

F: Free flight change

**`revNoShowCondition` **<mark style="color:blue;">**int**</mark>

Time before scheduled flight departure.

**`revNoshowFee` **<mark style="color:blue;">**string**</mark>

The total fee charged to change flight in case of no show.

If revNoshow = H, it should not be "null."

This value includes the change flight fee and no-show penalty.

**`ruleList` Array<ruleList>**

For internal use only.

**`ruleDetailList` Array<ruleList>**

List of all rules. Inside the ruleList are detailed airline rules for time periods, while outside the ruleList are the strictest rules before and after Noshow.

**`ruleId` **<mark style="color:blue;">**int**</mark>

For internal use only.

**`status` **<mark style="color:blue;">**string**</mark>

Change flight rule type

T: Non changeable

H: Changeable with restrictions

F: Free flight change

**`starMinute` **<mark style="color:blue;">**int**</mark>

Starting time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.

**`endMinute` **<mark style="color:blue;">**int**</mark>

Ending time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.

**`amount` **<mark style="color:blue;">**decimal**</mark>

Change flight fee

**`currency` **<mark style="color:blue;">**string**</mark>

The currency of airline's rule, if refundStatus = H, it should not be "null".

**`serviceElements` Array<**<mark style="color:blue;">**serviceElements**</mark>**>**

This function is used to fetch the other service rules of the selected airline. 

There is only one array for one way, and two arrays for round-trip.

The first array is for the outbound, and the second array is for the inbound.

**`hasFreeSeat` **<mark style="color:blue;">**int**</mark>

0: Not included

1: All included

2：Part included

**`hasFreeMeal` **<mark style="color:blue;">**int**</mark>

0: Not included

1: Included

{% endtab %}
{% endtabs %}

## How to ......

### 1. How to search for Oneway or Roundtrip flights?

If you want to search for oneway flights, please set `tripType` as 1 and keep `retDate` blank

```json
{
    "tripType": "1",
    "fromDate": "20220125",
    "retDate": "",
}
```

In the response, the `retSegments` of each routing will be empty

```json
"routings": [
    {
        "fromSegments": [
            {...}
        ],
        "retSegments": []
    },
    {
        "fromSegments": [
            {...}
        ],
        "retSegments": []
    },
    ...
]
```

If you want to search for roundtrip flights, please set `tripType` as 2 and input `retDate`

```css
{
    "tripType": "2",
    "fromDate": "20220125",
    "retDate": "20220128",
}
```

In the response, the <mark style="color:green;">`retSegments`</mark> of each routing will be empty

```json
"routings": [
    {
        "fromSegments": [
            {...}
        ],
        "retSegments": [
            {...}
        ]
    },
    {
        "fromSegments": [
            {...}
        ],
        "retSegments": [
            {...}
        ]
    },
    ...
]
```

### 2. How to identify direct or connection flights

Regarding direct flights, there will be only one segment in `fromSegments` or `retSegments`

```javascript
 {
 "fromSegments": [
                {
                    ...
                }
            ],
 "retSegments": [
                {
                    ...
                }
            ]
}
```

Regarding connection flights, there will be multiple segments in `fromSegments` or `retSegments`

```json
 {
 "fromSegments": [
                {
                    ...
                },
                {
                    ...
                }
            ],
 "retSegments": [
                {
                    ...
                },
                {
                    ...
                },
                {
                    ...
                }
            ]
}
```

### 3. Where is the baggage allowance mentioned?

#### 3.1. Free checked-in or cabin baggage

The free checked-in or cabin baggage allowance for each fare is available within both `search` and the `verify` response.

{% tabs %}
{% tab title="Schema" %}
**Baggage Element**

*   **segmentNo **<mark style="color:blue;">**int**</mark>

    Segment sequence, start from 1.

    If it is roundtrip, sequence outbond and inbound together.
    
*   **baggageType **<mark style="color:blue;">**string**</mark>

    There are 4 options for baggage:

    StandardCheckInBaggage: Standard Check-in Baggage.

    CabinBaggage: Usually refers to the Cabin Baggage Overhead Locker. Transition value. It will gradually transition to CabinBaggageOverheadLocker.

    CabinBaggageOverheadLocker: Cabin Baggage Overhead Locker.

    CabinBaggageUnderSeat: Cabin Baggage Under Seat. Usually refers to the personal item.
*   **passengerType **<mark style="color:blue;">**string**</mark>

    0: ADT

    1: CHD

    2: INF

    If search or verify for ADT only, then only ADT is returned;

    If search or verify for ADT+CHD, then ADT and CHD are returned.
*   **baggagePiece **<mark style="color:blue;">**int**</mark>

    Baggage pieces：

    0 No limitation

    \>0 Maximum pieces
*   **baggageWeight **<mark style="color:blue;">**int**</mark>

    Baggage Weight, with the unit of KG

    0 means No Free baggage 
    -1 meas No limitation on weight. 

*   **baggageSize **<mark style="color:blue;">**string**</mark>

    Baggage Size: 
    
    length＊width＊height and units. eg. "56＊36＊23cm", "18＊14＊8inch". 
    
    Or Total dimensions (length + width + height) of each piece. eg. "L+W+H<=158cm". 
    
    Empty means no limitation.

{% endtab %}

{% tab title="Samples" %}
```json
{
...,
"rule": {
        "hasBaggage": 0,
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
            "segmentNo": 2,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 0,
            "baggageWeight": 0,
            "baggageSize": "40*25*20cm"
          }
        ],
                "refundRules": [{...}],
                "changesRules":[{...}]
            }
...
}jso
```
{% endtab %}
{% endtabs %}

#### 3.2. Extra baggage offering

The details of the extra baggage offering are available in the `ancillaryProductElements` within both “search” and the “verify” response

{% tabs %}
{% tab title="Schema" %}
**ancillaryProductElement**

*   **`segmentIndex`  **<mark style="color:blue;">**int**</mark>

Segment sequence. Starts from 1. If it is return trip, sequence for outbound trip and inbound trip would be together.
    
*   **`endSegmentIndex`  **<mark style="color:blue;">**int**</mark>

The last segment for which this information is applicable.
    
*   **`productCode`  **<mark style="color:blue;">**string**</mark>

Unique identifier for the ancillary product. It would be used in the order request.
*   **`productName`  **<mark style="color:blue;">**string**</mark>

Ancillary product name.
*   **`productType`  **<mark style="color:blue;">**int**</mark>

Ancillary product type

1: Check-in baggage

3: Cabin Baggage Overhead Locker

Currently, only baggage is available.
    
*   **`canPurchaseWithTicket`  **<mark style="color:blue;">**int**</mark>

This ancillary product can be purchased during the booking flow. 
    
1=Yes; 0=No  
    
*   **`canPurchasePostTicket`  **<mark style="color:blue;">**int**</mark>

This ancillary product can be purchased in the post-ticketing flow. 
    
1=Yes; 0=No  
    
*   **`price`  **<mark style="color:blue;">**decimal**</mark>

Price for this ancillary.
    
*   **`currency`  **<mark style="color:blue;">**string**</mark>

The currency in which Atlas settles transactions with you.
    
*   **`vendorPrice`  **<mark style="color:blue;">**decimal**</mark>

The price charged by the vendor for the ancillary.
    
*   **`vendorCurrency`  **<mark style="color:blue;">**string**</mark>

The currency in which the vendor charges for the ancillary.
    
*   **`clientTechnicalServiceFee`  **<mark style="color:blue;">**decimal**</mark>

The service fee charged by Atlas for the purchase of the ancillary.
    
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
        
*   **`offerId`  **<mark style="color:blue;">**string**</mark>

The identifier of the offer of ancillary product. This will be "null" in the booking flow but will have an id in the post-ticketing flow.

*   **`maxQty`  **<mark style="color:blue;">**string**</mark>

Maximum purchase quantity per product

*   **`minQty`  **<mark style="color:blue;">**string**</mark>

Starting purchase quantity per product

*   **`ancillaryCode`  **<mark style="color:blue;">**string**</mark>

The code for this ancillary option. This will be identical to the `productCode`.
{% endtab %}

{% tab title="Samples" %}
```json
 "ancillaryProductElements": [
        {
          "segmentIndex": 1,
          "endSegmentIndex": null,
          "productCode": "SCI_BAG_1PC_15KG",
          "productName": "StandardCheckInBaggage",
          "productType": 1,
          "canPurchaseWithTicket": 1,
          "canPurchasePostTicket": 1,
          "price": 37.94,
          "currency": "USD",
          "vendorPrice": 34.49,
          "vendorCurrency": "GBP",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 15,
            "isAllWeight": true
          },
          "offerId": null,
          "ancillaryCode": "SCI_BAG_1PC_15KG"
        },
        {
          "segmentIndex": 1,
          "endSegmentIndex": null,
          "productCode": "SCI_BAG_1PC_23KG",
          "productName": "StandardCheckInBaggage",
          "productType": 1,
          "canPurchaseWithTicket": 1,
          "canPurchasePostTicket": 1,
          "price": 40.69,
          "currency": "USD",
          "vendorPrice": 36.99,
          "vendorCurrency": "GBP",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 23,
            "isAllWeight": true
          },
          "offerId": null,
          "ancillaryCode": "SCI_BAG_1PC_23KG"
        },
        {
          "segmentIndex": 2,
          "endSegmentIndex": null,
          "productCode": "SCI_BAG_1PC_23KG",
          "productName": "StandardCheckInBaggage",
          "productType": 1,
          "canPurchaseWithTicket": 1,
          "canPurchasePostTicket": 1,
          "price": 52.76,
          "currency": "USD",
          "vendorPrice": 48.49,
          "vendorCurrency": "EUR",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 23,
            "isAllWeight": true
          },
          "offerId": null,
          "ancillaryCode": "SCI_BAG_1PC_23KG"
        }
      ]
```
{% endtab %}
{% endtabs %}
