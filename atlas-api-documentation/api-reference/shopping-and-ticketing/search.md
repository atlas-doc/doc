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
  "airlines": ["FR", "W6", "F9"],
  "fromFlightNumbers": ["FR123", "FR456"],
  "retFlightNumbers": ["FR123", "FR456"],
  "includeMultipleFareFamily": true
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
      "fid": "_CRghXPitTBZS-NfM-Ku_5Yttfzh9Cgb4yyIxDTAs_fFcjVKg92FlTFwA_GEaChOQxTZJ7brCduAEac4Cv-UGG8WfOBAHVGM",
      "routingIdentifier": "UFJHX1ZOT18xXzIwMjQxMjI2X18xXzBfMHxocGJybTU1OTM1fDF8MTY2LjY3XzE2Ni42N18xNTkuOTZfMS4wMF80OTQuMzBfVVNEfFBSR19WTk9fMV8yMDI0MTIyNl9fMV8wXzBeUFJHLUJUMDQ4Mi0tUklYLTIwMjQxMjI2MTk0MC0yMDI0MTIyNjIyMjUtRWNvbm9teSBCQVNJQy0xLSNSSVgtQlQwMzQ5LS1WTk8tMjAyNDEyMjYyMzE1LTIwMjQxMjI2MjM1OS1FY29ub215IEJBU0lDLTEtXjE2Ni42N18xNjYuNjdfMTU5Ljk2XzEuMDBfNDk0LjMwXkFCVF9BQlReXkFCVDFQUkdWTk80MDAyMDI0MTIyNl5FVVJ8MHwyMDI0MTIxMzE1MjgzNnwwfDE3MzQwNzQ5MTY1MDd5UlJzZnx8fHx8MS4wMHwzfDB8.kpIBDjjhcL+znY8vH8KDqLB0q+lC9s9Tmt9OBxqhyS4=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 125.57,
      "adultTax": 41.1,
      "childPrice": 125.57,
      "childTax": 41.1,
      "infantPrice": 159.96,
      "infantTax": 0,
      "infantAllowed": true,
      "transactionFeePerPax": 1,
      "transactionFee": 1,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "segmentIndex": 1,
          "carrier": "BT",
          "flightNumber": "BT0482",
          "depAirport": "PRG",
          "depTime": "202412261940",
          "arrAirport": "RIX",
          "arrTime": "202412262225",
          "stopCities": "",
          "duration": 105,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy BASIC"
        },
        {
          "segmentIndex": 2,
          "carrier": "BT",
          "flightNumber": "BT0349",
          "depAirport": "RIX",
          "depTime": "202412262315",
          "arrAirport": "VNO",
          "arrTime": "202412262359",
          "stopCities": "",
          "duration": 44,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy BASIC"
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
            "segmentNo": 2,
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
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          },
          {
            "segmentNo": 2,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
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
                "ruleId": 40283,
                "status": "T",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40288,
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
            "changesStatus": "H",
            "changesFee": 50,
            "currency": "EUR",
            "revNoshow": "T",
            "revNoShowCondition": 0,
            "revNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40293,
                "status": "H",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 50,
                "currency": "EUR"
              },
              {
                "ruleId": 40298,
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
          }
        ]
      },
      "ancillaryProductElements": [],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-12-13T05:25:56Z",
      "displayFare": null,
      "ancillarySupported": []
    },
    {
      "fid": "IX-m5EjtM9EnSVgnuTi7hpYttfzh9Cgb4yyIxDTAs_fFcjVKg92FlTFwA_GEaChOQxTZJ7brCduAEac4Cv-UGG8WfOBAHVGM",
      "routingIdentifier": "UFJHX1ZOT18xXzIwMjQxMjI2X18xXzBfMHxocGJybTU1OTM1fDF8MjQwLjQ1XzI0MC40NV8xOTYuMTBfMS4wMF82NzguMDBfVVNEfFBSR19WTk9fMV8yMDI0MTIyNl9fMV8wXzBeUFJHLUJUMDQ4Mi0tUklYLTIwMjQxMjI2MTk0MC0yMDI0MTIyNjIyMjUtRWNvbm9teSBDTEFTU0lDLTEtI1JJWC1CVDAzNDktLVZOTy0yMDI0MTIyNjIzMTUtMjAyNDEyMjYyMzU5LUVjb25vbXkgQ0xBU1NJQy0xLV4yNDAuNDVfMjQwLjQ1XzE5Ni4xMF8xLjAwXzY3OC4wMF5BQlRfQUJUXl5BQlQxUFJHVk5PNDAwMjAyNDEyMjZeRVVSfDB8MjAyNDEyMTMxNTI4MzZ8MHwxNzM0MDc0OTE2NTA3eVJSc2Z8fHx8fDEuMDB8M3wwfA==.IWTgIRBBgQxn9WVNnySSfJTPhq9XdiH3M4m3cy+f678=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 187.13,
      "adultTax": 53.32,
      "childPrice": 187.13,
      "childTax": 53.32,
      "infantPrice": 196.1,
      "infantTax": 0,
      "infantAllowed": true,
      "transactionFeePerPax": 1,
      "transactionFee": 1,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "segmentIndex": 1,
          "carrier": "BT",
          "flightNumber": "BT0482",
          "depAirport": "PRG",
          "depTime": "202412261940",
          "arrAirport": "RIX",
          "arrTime": "202412262225",
          "stopCities": "",
          "duration": 105,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy CLASSIC"
        },
        {
          "segmentIndex": 2,
          "carrier": "BT",
          "flightNumber": "BT0349",
          "depAirport": "RIX",
          "depTime": "202412262315",
          "arrAirport": "VNO",
          "arrTime": "202412262359",
          "stopCities": "",
          "duration": 44,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy CLASSIC"
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
            "baggagePiece": 1,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 2,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 1,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          },
          {
            "segmentNo": 2,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
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
                "ruleId": 40284,
                "status": "T",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40289,
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
            "changesStatus": "H",
            "changesFee": 50,
            "currency": "EUR",
            "revNoshow": "T",
            "revNoShowCondition": 0,
            "revNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40294,
                "status": "H",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 50,
                "currency": "EUR"
              },
              {
                "ruleId": 40299,
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
          }
        ]
      },
      "ancillaryProductElements": [],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-12-13T05:25:56Z",
      "displayFare": null,
      "ancillarySupported": []
    },
    {
      "fid": "ZE8zDIKlUVVov0gQoBk3QpYttfzh9Cgb4yyIxDTAs_fFcjVKg92FlTFwA_GEaChOQxTZJ7brCduAEac4Cv-UGG8WfOBAHVGM",
      "routingIdentifier": "UFJHX1ZOT18xXzIwMjQxMjI2X18xXzBfMHxocGJybTU1OTM1fDF8MjgyLjAzXzI4Mi4wM18yMDUuNDdfMS4wMF83NzAuNTNfVVNEfFBSR19WTk9fMV8yMDI0MTIyNl9fMV8wXzBeUFJHLUJUMDQ4Mi0tUklYLTIwMjQxMjI2MTk0MC0yMDI0MTIyNjIyMjUtRWNvbm9teSBGTEVYLTEtI1JJWC1CVDAzNDktLVZOTy0yMDI0MTIyNjIzMTUtMjAyNDEyMjYyMzU5LUVjb25vbXkgRkxFWC0xLV4yODIuMDNfMjgyLjAzXzIwNS40N18xLjAwXzc3MC41M15BQlRfQUJUXl5BQlQxUFJHVk5PNDAwMjAyNDEyMjZeRVVSfDB8MjAyNDEyMTMxNTI4MzZ8MHwxNzM0MDc0OTE2NTA3eVJSc2Z8fHx8fDEuMDB8M3wwfA==.Gxi0Kcy7ytxhPdvnDW+aoJ2wGuzE1hZ/X1YddW8Tejs=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 216.79,
      "adultTax": 65.24,
      "childPrice": 216.79,
      "childTax": 65.24,
      "infantPrice": 205.47,
      "infantTax": 0,
      "infantAllowed": true,
      "transactionFeePerPax": 1,
      "transactionFee": 1,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "segmentIndex": 1,
          "carrier": "BT",
          "flightNumber": "BT0482",
          "depAirport": "PRG",
          "depTime": "202412261940",
          "arrAirport": "RIX",
          "arrTime": "202412262225",
          "stopCities": "",
          "duration": 105,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy FLEX"
        },
        {
          "segmentIndex": 2,
          "carrier": "BT",
          "flightNumber": "BT0349",
          "depAirport": "RIX",
          "depTime": "202412262315",
          "arrAirport": "VNO",
          "arrTime": "202412262359",
          "stopCities": "",
          "duration": 44,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy FLEX"
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
            "baggagePiece": 2,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 2,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 2,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 1,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          },
          {
            "segmentNo": 2,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          }
        ],
        "refundRules": [
          {
            "refundType": 0,
            "refundStatus": "H",
            "refundFee": 25,
            "currency": "EUR",
            "refNoshow": "T",
            "refNoShowCondition": 0,
            "refNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40285,
                "status": "H",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 25,
                "currency": "EUR"
              },
              {
                "ruleId": 40290,
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
            "changesStatus": "F",
            "changesFee": 0,
            "currency": "EUR",
            "revNoshow": "T",
            "revNoShowCondition": 0,
            "revNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40295,
                "status": "F",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40300,
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
            "hasFreeSeat": 2,
            "hasFreeMeal": 0
          }
        ]
      },
      "ancillaryProductElements": [],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-12-13T05:25:56Z",
      "displayFare": null,
      "ancillarySupported": []
    },
    {
      "fid": "dKLKop9ZAjxNZfbXFnEjV5Yttfzh9Cgb4yyIxDTAs_fFcjVKg92FlTFwA_GEaChOQxTZJ7brCduAEac4Cv-UGG8WfOBAHVGM",
      "routingIdentifier": "UFJHX1ZOT18xXzIwMjQxMjI2X18xXzBfMHxocGJybTU1OTM1fDF8NDAyLjE4XzQwMi4xOF8zMDYuNDNfMS4wMF8xMTExLjc5X1VTRHxQUkdfVk5PXzFfMjAyNDEyMjZfXzFfMF8wXlBSRy1CVDA0ODItLVJJWC0yMDI0MTIyNjE5NDAtMjAyNDEyMjYyMjI1LUJVU0lORVNTLTEtI1JJWC1CVDAzNDktLVZOTy0yMDI0MTIyNjIzMTUtMjAyNDEyMjYyMzU5LUJVU0lORVNTLTEtXjQwMi4xOF80MDIuMThfMzA2LjQzXzEuMDBfMTExMS43OV5BQlRfQUJUXl5BQlQxUFJHVk5PNDAwMjAyNDEyMjZeRVVSfDB8MjAyNDEyMTMxNTI4MzZ8MHwxNzM0MDc0OTE2NTA3eVJSc2Z8fHx8fDEuMDB8M3wwfA==.wbZD+u0BtWPDehg9GcZ+pnAoY/qWk1MF7+9oeKE/GjA=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 335.87,
      "adultTax": 66.31,
      "childPrice": 335.87,
      "childTax": 66.31,
      "infantPrice": 306.43,
      "infantTax": 0,
      "infantAllowed": true,
      "transactionFeePerPax": 1,
      "transactionFee": 1,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "segmentIndex": 1,
          "carrier": "BT",
          "flightNumber": "BT0482",
          "depAirport": "PRG",
          "depTime": "202412261940",
          "arrAirport": "RIX",
          "arrTime": "202412262225",
          "stopCities": "",
          "duration": 105,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 2,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "BUSINESS"
        },
        {
          "segmentIndex": 2,
          "carrier": "BT",
          "flightNumber": "BT0349",
          "depAirport": "RIX",
          "depTime": "202412262315",
          "arrAirport": "VNO",
          "arrTime": "202412262359",
          "stopCities": "",
          "duration": 44,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 2,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "BUSINESS"
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
            "baggagePiece": 2,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 2,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 2,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 1,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 2,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          },
          {
            "segmentNo": 2,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 2,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          }
        ],
        "refundRules": [
          {
            "refundType": 0,
            "refundStatus": "F",
            "refundFee": 0,
            "currency": "EUR",
            "refNoshow": "T",
            "refNoShowCondition": 0,
            "refNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40287,
                "status": "F",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40292,
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
            "changesStatus": "F",
            "changesFee": 0,
            "currency": "EUR",
            "revNoshow": "T",
            "revNoShowCondition": 0,
            "revNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40297,
                "status": "F",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40302,
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
            "hasFreeSeat": 1,
            "hasFreeMeal": 1
          }
        ]
      },
      "ancillaryProductElements": [],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-12-13T05:25:56Z",
      "displayFare": null,
      "ancillarySupported": []
    },
    {
      "fid": "Mwu-N61Mm8veA8_gD1qC0pYttfzh9Cgb4yyIxDTAs_fFcjVKg92FlTFwA_GEaChO-NS6-xXUaUfxYfNPi67bxeiCLttfaj7a",
      "routingIdentifier": "UFJHX1ZOT18xXzIwMjQxMjI2X18xXzBfMHxocGJybTU1OTM1fDF8MjQwLjIyXzI0MC4yMl8yMDAuMDlfMS4wMF82ODEuNTNfVVNEfFBSR19WTk9fMV8yMDI0MTIyNl9fMV8wXzBeUFJHLUJUMDQ4Mi0tUklYLTIwMjQxMjI2MTk0MC0yMDI0MTIyNjIyMjUtRWNvbm9teSBCQVNJQy0xLSNSSVgtQlQwMzQxLS1WTk8tMjAyNDEyMjcwNzI1LTIwMjQxMjI3MDgxNS1FY29ub215IEJBU0lDLTEtXjI0MC4yMl8yNDAuMjJfMjAwLjA5XzEuMDBfNjgxLjUzXkFCVF9BQlReXkFCVDFQUkdWTk80MDAyMDI0MTIyNl5FVVJ8MHwyMDI0MTIxMzE1MjgzNnwwfDE3MzQwNzQ5MTY1MDd5UlJzZnx8fHx8MS4wMHwzfDB8.IBq11hDBLWLxKTDOid1snAJXBlPb2IxybZYI8A/+FGk=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 200.42,
      "adultTax": 39.8,
      "childPrice": 200.42,
      "childTax": 39.8,
      "infantPrice": 200.09,
      "infantTax": 0,
      "infantAllowed": true,
      "transactionFeePerPax": 1,
      "transactionFee": 1,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "segmentIndex": 1,
          "carrier": "BT",
          "flightNumber": "BT0482",
          "depAirport": "PRG",
          "depTime": "202412261940",
          "arrAirport": "RIX",
          "arrTime": "202412262225",
          "stopCities": "",
          "duration": 105,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy BASIC"
        },
        {
          "segmentIndex": 2,
          "carrier": "BT",
          "flightNumber": "BT0341",
          "depAirport": "RIX",
          "depTime": "202412270725",
          "arrAirport": "VNO",
          "arrTime": "202412270815",
          "stopCities": "",
          "duration": 50,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy BASIC"
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
            "segmentNo": 2,
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
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          },
          {
            "segmentNo": 2,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
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
                "ruleId": 40283,
                "status": "T",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40288,
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
            "changesStatus": "H",
            "changesFee": 50,
            "currency": "EUR",
            "revNoshow": "T",
            "revNoShowCondition": 0,
            "revNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40293,
                "status": "H",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 50,
                "currency": "EUR"
              },
              {
                "ruleId": 40298,
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
          }
        ]
      },
      "ancillaryProductElements": [],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-12-13T05:25:56Z",
      "displayFare": null,
      "ancillarySupported": []
    },
    {
      "fid": "QFDyo3S-Pu4CizegTgK8l5Yttfzh9Cgb4yyIxDTAs_fFcjVKg92FlTFwA_GEaChO-NS6-xXUaUfxYfNPi67bxeiCLttfaj7a",
      "routingIdentifier": "UFJHX1ZOT18xXzIwMjQxMjI2X18xXzBfMHxocGJybTU1OTM1fDF8MjUyLjkyXzI1Mi45Ml8yMzAuNzBfMS4wMF83MzcuNTRfVVNEfFBSR19WTk9fMV8yMDI0MTIyNl9fMV8wXzBeUFJHLUJUMDQ4Mi0tUklYLTIwMjQxMjI2MTk0MC0yMDI0MTIyNjIyMjUtRWNvbm9teSBDTEFTU0lDLTEtI1JJWC1CVDAzNDEtLVZOTy0yMDI0MTIyNzA3MjUtMjAyNDEyMjcwODE1LUVjb25vbXkgQ0xBU1NJQy0xLV4yNTIuOTJfMjUyLjkyXzIzMC43MF8xLjAwXzczNy41NF5BQlRfQUJUXl5BQlQxUFJHVk5PNDAwMjAyNDEyMjZeRVVSfDB8MjAyNDEyMTMxNTI4MzZ8MHwxNzM0MDc0OTE2NTA3eVJSc2Z8fHx8fDEuMDB8M3wwfA==.FQZ40tg29YMe6egtoA7Uw83hdIXSYk0RUbGwoxfL6EI=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 201.16,
      "adultTax": 51.76,
      "childPrice": 201.16,
      "childTax": 51.76,
      "infantPrice": 230.7,
      "infantTax": 0,
      "infantAllowed": true,
      "transactionFeePerPax": 1,
      "transactionFee": 1,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "segmentIndex": 1,
          "carrier": "BT",
          "flightNumber": "BT0482",
          "depAirport": "PRG",
          "depTime": "202412261940",
          "arrAirport": "RIX",
          "arrTime": "202412262225",
          "stopCities": "",
          "duration": 105,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy CLASSIC"
        },
        {
          "segmentIndex": 2,
          "carrier": "BT",
          "flightNumber": "BT0341",
          "depAirport": "RIX",
          "depTime": "202412270725",
          "arrAirport": "VNO",
          "arrTime": "202412270815",
          "stopCities": "",
          "duration": 50,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy CLASSIC"
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
            "baggagePiece": 1,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 2,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 1,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          },
          {
            "segmentNo": 2,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
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
                "ruleId": 40284,
                "status": "T",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40289,
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
            "changesStatus": "H",
            "changesFee": 50,
            "currency": "EUR",
            "revNoshow": "T",
            "revNoShowCondition": 0,
            "revNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40294,
                "status": "H",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 50,
                "currency": "EUR"
              },
              {
                "ruleId": 40299,
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
          }
        ]
      },
      "ancillaryProductElements": [],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-12-13T05:25:56Z",
      "displayFare": null,
      "ancillarySupported": []
    },
    {
      "fid": "wbElRxulKjH_3YOTIw7gDpYttfzh9Cgb4yyIxDTAs_fFcjVKg92FlTFwA_GEaChO-NS6-xXUaUfxYfNPi67bxeiCLttfaj7a",
      "routingIdentifier": "UFJHX1ZOT18xXzIwMjQxMjI2X18xXzBfMHxocGJybTU1OTM1fDF8MTgzLjUzXzE4My41M18xODkuMjBfMS4wMF81NTcuMjZfVVNEfFBSR19WTk9fMV8yMDI0MTIyNl9fMV8wXzBeUFJHLUJUMDQ4Mi0tUklYLTIwMjQxMjI2MTk0MC0yMDI0MTIyNjIyMjUtRWNvbm9teSBGTEVYLTEtI1JJWC1CVDAzNDEtLVZOTy0yMDI0MTIyNzA3MjUtMjAyNDEyMjcwODE1LUVjb25vbXkgRkxFWC0xLV4xODMuNTNfMTgzLjUzXzE4OS4yMF8xLjAwXzU1Ny4yNl5BQlRfQUJUXl5BQlQxUFJHVk5PNDAwMjAyNDEyMjZeRVVSfDB8MjAyNDEyMTMxNTI4MzZ8MHwxNzM0MDc0OTE2NTA3eVJSc2Z8fHx8fDEuMDB8M3wwfA==.kbv9khpQ1b93/yqCsv6vN3h3iDvROVbLzlY/5Nqb+xI=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 137.69,
      "adultTax": 45.84,
      "childPrice": 137.69,
      "childTax": 45.84,
      "infantPrice": 189.2,
      "infantTax": 0,
      "infantAllowed": true,
      "transactionFeePerPax": 1,
      "transactionFee": 1,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "segmentIndex": 1,
          "carrier": "BT",
          "flightNumber": "BT0482",
          "depAirport": "PRG",
          "depTime": "202412261940",
          "arrAirport": "RIX",
          "arrTime": "202412262225",
          "stopCities": "",
          "duration": 105,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy FLEX"
        },
        {
          "segmentIndex": 2,
          "carrier": "BT",
          "flightNumber": "BT0341",
          "depAirport": "RIX",
          "depTime": "202412270725",
          "arrAirport": "VNO",
          "arrTime": "202412270815",
          "stopCities": "",
          "duration": 50,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "Economy FLEX"
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
            "baggagePiece": 2,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 2,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 2,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 1,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          },
          {
            "segmentNo": 2,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 1,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          }
        ],
        "refundRules": [
          {
            "refundType": 0,
            "refundStatus": "H",
            "refundFee": 25,
            "currency": "EUR",
            "refNoshow": "T",
            "refNoShowCondition": 0,
            "refNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40285,
                "status": "H",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 25,
                "currency": "EUR"
              },
              {
                "ruleId": 40290,
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
            "changesStatus": "F",
            "changesFee": 0,
            "currency": "EUR",
            "revNoshow": "T",
            "revNoShowCondition": 0,
            "revNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40295,
                "status": "F",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40300,
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
            "hasFreeSeat": 2,
            "hasFreeMeal": 0
          }
        ]
      },
      "ancillaryProductElements": [],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-12-13T05:25:56Z",
      "displayFare": null,
      "ancillarySupported": []
    },
    {
      "fid": "hGdhBjki7YfWzhfcplunmJYttfzh9Cgb4yyIxDTAs_fFcjVKg92FlTFwA_GEaChO-NS6-xXUaUfxYfNPi67bxeiCLttfaj7a",
      "routingIdentifier": "UFJHX1ZOT18xXzIwMjQxMjI2X18xXzBfMHxocGJybTU1OTM1fDF8NDA2LjAzXzQwNi4wM18zMjEuMDJfMS4wMF8xMTM0LjA4X1VTRHxQUkdfVk5PXzFfMjAyNDEyMjZfXzFfMF8wXlBSRy1CVDA0ODItLVJJWC0yMDI0MTIyNjE5NDAtMjAyNDEyMjYyMjI1LUJVU0lORVNTLTEtI1JJWC1CVDAzNDEtLVZOTy0yMDI0MTIyNzA3MjUtMjAyNDEyMjcwODE1LUJVU0lORVNTLTEtXjQwNi4wM180MDYuMDNfMzIxLjAyXzEuMDBfMTEzNC4wOF5BQlRfQUJUXl5BQlQxUFJHVk5PNDAwMjAyNDEyMjZeRVVSfDB8MjAyNDEyMTMxNTI4MzZ8MHwxNzM0MDc0OTE2NTA3eVJSc2Z8fHx8fDEuMDB8M3wwfA==.YW9MS01re+FqhCcXom7YWC+oz1NPYDlzdA76qNJGzBo=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 342.57,
      "adultTax": 63.46,
      "childPrice": 342.57,
      "childTax": 63.46,
      "infantPrice": 321.02,
      "infantTax": 0,
      "infantAllowed": true,
      "transactionFeePerPax": 1,
      "transactionFee": 1,
      "transactionFeeMode": "PER_PAX",
      "nationalityType": 0,
      "nationality": "",
      "suitAge": "",
      "PaxType": "ADT",
      "fromSegments": [
        {
          "segmentIndex": 1,
          "carrier": "BT",
          "flightNumber": "BT0482",
          "depAirport": "PRG",
          "depTime": "202412261940",
          "arrAirport": "RIX",
          "arrTime": "202412262225",
          "stopCities": "",
          "duration": 105,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 2,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "BUSINESS"
        },
        {
          "segmentIndex": 2,
          "carrier": "BT",
          "flightNumber": "BT0341",
          "depAirport": "RIX",
          "depTime": "202412270725",
          "arrAirport": "VNO",
          "arrTime": "202412270815",
          "stopCities": "",
          "duration": 50,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 2,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "BT",
          "operatingFlightnumber": "",
          "fareFamily": "BUSINESS"
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
            "baggagePiece": 2,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 2,
            "baggageType": "StandardCheckInBaggage",
            "passengerType": 0,
            "baggagePiece": 2,
            "baggageWeight": 23,
            "baggageSize": ""
          },
          {
            "segmentNo": 1,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 2,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          },
          {
            "segmentNo": 2,
            "baggageType": "CabinBaggageOverheadLocker",
            "passengerType": 0,
            "baggagePiece": 2,
            "baggageWeight": 8,
            "baggageSize": "55*40*23cm"
          }
        ],
        "refundRules": [
          {
            "refundType": 0,
            "refundStatus": "F",
            "refundFee": 0,
            "currency": "EUR",
            "refNoshow": "T",
            "refNoShowCondition": 0,
            "refNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40287,
                "status": "F",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40292,
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
            "changesStatus": "F",
            "changesFee": 0,
            "currency": "EUR",
            "revNoshow": "T",
            "revNoShowCondition": 0,
            "revNoshowFee": 0,
            "ruleDetailList": [
              {
                "ruleId": 40297,
                "status": "F",
                "startMinute": 525600,
                "endMinute": 0,
                "amount": 0,
                "currency": "EUR"
              },
              {
                "ruleId": 40302,
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
            "hasFreeSeat": 1,
            "hasFreeMeal": 1
          }
        ]
      },
      "ancillaryProductElements": [],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false,
      "refreshTime": "2024-12-13T05:25:56Z",
      "displayFare": null,
      "ancillarySupported": []
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
