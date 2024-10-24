---
description: Create an order request to search for flights.
---

# Search

### Dependency

No preceding function needs to be called before `Search`.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/search.do](https://sandbox.atriptech.com/search.do)

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

**`displayCurrency`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

The alternative currency in which the fare and taxes amount needs to be displayed. The 3-letter currency code should be entered. Please refer to the "Highlights" section below for further information.

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
  "airlines": ["W6"],
  "currency": "GBP",
  "displayCurrency": "PHP",
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
      "fid": "NNQPjln9io_VkVCLML-tV4uTWB1-bYVbwEbgbq1gwbbyIGmv3IQjvGArLc-kVkfqqonjuSrhTmd6q9tCSQ5JdEbgsLbAG9YqlESmEgnTm4P1GEmT5TthTQ..",
      "routingIdentifier": "EXsU8XSpfLYTSaQTVCjrJMJvG/ysDtKYfq1WIi9iKV3RuKGQWRYoLHwlk3d3nfx3CfcndJLEJ0OelZh4CJOznF9aTBiw3WJrCv1w5tPrnLqsrzEwGf6LU4JnimIHlZ8g9Mbw9o1UAsRxu28yDTH1sxCUiQXhe9aQqCnWwMFh28gA/nj6IKNh5/yz0GWbBL6s1yDekyABUkLWmuWriKG76AcSFeTleOVJEjXfFd3mUvpZJe1wsRs5TI/Nma2Sz/cOdhAjhrTIFnOMJEKInVplSW3JYquYRVlKPNaFSuoF5K7IHGWlTR0X2vJysOfDQQZWR7Qv1wj0wUrE1kfV4vUrurLMbC/8XlxjYBc7iz9giHkbTb9r/K5/eabN+BX2cuBjtcmNH0T9SwZdxpCXnsjGxdC6wjGifmzacvdkADFsgfWzqaR6+aEfwt4jQKkit64X8IoXcz9XqDadvtpoFyrQz1tXYb6UK8+doiventK1gdc8oJQnVwpWZDKzsW4suk3TsDp0v+v8UKQy69wsHIbB/y+fzp2gv7VR6YPlLhv9P5f1GEmT5TthTQ==",
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
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-03-20T09:31:46Z",
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
* Display Currency is only to be used for display purposes. The amount in the response is not to be used for fare comparison or accounting purposes. The display currency conversion will be available in fares, taxes and ancillary baggage sections of the search and verify response. When the "vendorFare" element is available, the conversion will be from the vendor fare. In the absence of the "vendorFare" element, the conversion would be from the transacted fare.
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


**`currency`  **<mark style="color:blue;">**string**</mark>

The currency in which Atlas settles transactions with you.

**`adultPrice`  **<mark style="color:blue;">**decimal**</mark>

Adult fare per passenger.

**`adultTax`  **<mark style="color:blue;">**decimal**</mark>

Adult tax per passenger.

**`childPrice`  **<mark style="color:blue;">**decimal**</mark>

Child fare per passenger.

**`childTax`  **<mark style="color:blue;">**decimal**</mark>

Child tax per passenger.

**`InfantPrice`  **<mark style="color:blue;">**decimal**</mark>

Infant fare per passenger.

**`InfantTax`  **<mark style="color:blue;">**decimal**</mark>

Infant tax per passenger.

**`infantAllowed`  **<mark style="color:blue;">**boolean**</mark>

Infant passenger allowed for that airline.

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

*   **`displayPrice`  **<mark style="color:blue;">**string**</mark>

The fare converted into the display currency.

*   **`displayCurrency`  **<mark style="color:blue;">**string**</mark>

The currency into which the fare has been converted.

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

**`displayFare`  **<mark style="color:blue;">**string**</mark>

The converted fare as per the display currency.

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
