# Real-time Search

### Dependency

No preceding function needs to be called before `Search`.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/realTimeSearch.do](https://sandbox.atriptech.com/realTimeSearch.do)




### Request

{% tabs %}
{% tab title="Schema" %}

**`cid`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Identifier of client and user.

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

Arrival date, the format is YYYYMMDD

Must not be earlier than fromDate. And it can be blank if tripType=1.

**`airlines`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

An array of IATA Codes of airlines. The result will only contain the airlines specified in the search request.

**`requestSource`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Identify the source of the search traffic, E.g. Google Flights, Oganic Search, SkyScanner.

**`acceptCacheIfTimeout`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Required**</mark>

Boolean. Defines if the cache search should be done if the real-time search is timed-out.

If "false", then the request will time-out if it exceeds 120s and no results will be displayed.

If "true", then after 120s we will look for results from cache and display the cache results.

{% endtab %}

{% tab title="Samples" %}
```
{
  "cid": "xxxxxxxxxx",
  "tripType": "1",
  "adultNum": 1,
  "childNum": 0,
  "infantNum": 0,
  "fromCity": "CEB",
  "toCity": "DXB",
  "fromDate": "20230721",
  "retDate": "",
  "airlines": ["5J"],
  "acceptCacheIfTimeout": true,
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

The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.

**`refreshTime`  **<mark style="color:blue;">**string**</mark>

The time when the cache was populated with the results from the airline. When "acceptCacheIfTimeout" is "false" then the `refreshTime` will be "null".

**`routings` Array <**[**Routing Element**](search.md#route-element-schema)**>**

The array of the routings include suitable flights and fares. Click [<mark style="color:red;">here</mark> ](search.md#route-element-schema)to check the schema

{% hint style="info" %}
**Points to note for real-time search:**

* This function will only be opened by Atlas after understanding the requirements. 
* The content of the RQ and RS remains the same. Once the search response is received, the exact same flow needs to be followed for verify, book and pay process. The end-points for these services also remain the same.
* The timeout duration is 120s
* As this is a LIVE search, we would recommend that the airline filter is used during the search process to speed-up the response.
* Please contact your Business Development Director or Account Manager if you require access to this functionality.
{% endhint %}

{% endtab %}

{% tab title="Samples" %}
```
{
  "status": 0,
  "msg": "success",
  "routings": [
    {
      "fid": "xVn1sJWZv5OfC2_Kvxx5MinqMiK42MgDFfexy9CcyKUAN8I_PrmuWg..",
      "routingIdentifier": "rSFlKG9ikyzhEpCawoQj6+n4pzMNWvmmc316YexRjyNCLGIVqbywjjLRoBcZvJtFaE+2F9ek2xlAqYz6utyVKa9/eJTFZ1aEtIRTxsHkpR57bXH1nPQ22YBH7oNsJeA+YFhna0K19xFYYefTBZCp10crf98Kj+XmKt5xqnewVFrNy8azpf5S8lA3MBp9nv+mm8FvgOm5+gd+jjt5u1bcg/l20jt4Do/WhG8WjMqAhR4PLsy61iMgeGS0XgIY64vujMGhJrt+1RzDpPLusqt7aFZvQz3Z0NHknPksr4knuraxiKtIueR5wpsN0rdQga2o98by0ZZEaCq3Ws2ckChtohVCH+Eda6Sv",
      "supportCreditTransPayment": "1",
      "supportB2bPayment": null,
      "supportPaymentMethods": null,
      "currency": "EUR",
      "adultPrice": 26.25,
      "adultTax": 17.5,
      "childPrice": 26.25,
      "childTax": 17.5,
      "infantPrice": 0,
      "infantTax": 0,
      "infantAllowed": false,
      "transactionFeePerPax": 0.92,
      "transactionFee": 0.92,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "carrier": "5J",
          "flightNumber": "5J580",
          "depAirport": "CEB",
          "depTime": "202307210000",
          "arrAirport": "MNL",
          "arrTime": "202307210130",
          "stopCities": "",
          "duration": 90,
          "codeShare": false,
          "cabin": "E",
          "cabinClass": 1,
          "seatCount": 1,
          "aircraftCode": "321",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "",
          "operatingFlightnumber": "",
          "fareFamily": "GO Basic"
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
            "baggageWeight": 0,
            "baggageSize": ""
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
            "ruleList": null
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
            "ruleList": null
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
          "price": 11.97,
          "currency": "EUR",
          "vendorPrice": 677.6,
          "vendorCurrency": "PHP",
          "clientTechnicalServiceFee": 0,
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
          "price": 23.93,
          "currency": "EUR",
          "vendorPrice": 1355.2,
          "vendorCurrency": "PHP",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 32,
            "isAllWeight": true,
            "size": ""
          },
          "offerId": null,
          "maxQty": 1,
          "minQty": 1,
          "categoryCode": "StandardCheckInBaggage",
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
          "price": 30.46,
          "currency": "EUR",
          "vendorPrice": 1724.8,
          "vendorCurrency": "PHP",
          "clientTechnicalServiceFee": 0,
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
          "ancillaryCode": "SCI_BAG_2PC_40KG"
        }
      ],
      "vendorFare": {
        "vendorAdultPrice": 1486.49,
        "vendorAdultTax": 990.99,
        "vendorChildPrice": 1486.49,
        "vendorChildTax": 990.99,
        "vendorInfantPrice": 0,
        "vendorInfantTax": 0,
        "vendorCurrency": "PHP"
      },
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2023-05-18T07:12:32Z"
    }
  ],
  "vendorFare": {
    "vendorAdultPrice": 4045.47,
    "vendorAdultTax": 2696.97,
    "vendorChildPrice": 4045.47,
    "vendorChildTax": 2696.97,
    "vendorInfantPrice": 0,
    "vendorInfantTax": 0,
    "vendorCurrency": "PHP"
  },
  "bundleOptions": [],
  "links": null,
  "separateBookings": false,
  "refreshTime": "2023-05-18T07:12:32Z"
}
```
{% endtab %}
{% endtabs %}
