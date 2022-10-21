---
description: Create an order request to search for flights.
---

# Search

### Dependency&#x20;

No preceding function needs to be called before `Search`.&#x20;

### Endpoint&#x20;

[https://sandbox.atlaslovestravel.com/search.do ](https://sandbox.atlaslovestravel.com/search.do)

### Request&#x20;

{% tabs %}
{% tab title="Schema" %}
#### `cid`                 <mark style="color:blue;">string</mark>                                                                                                                  <mark style="color:green;">Required</mark>

Identifier of client and user.

#### `tripType`      <mark style="color:blue;">string</mark>                                                                                                                  <mark style="color:green;">Required</mark>

1: Oneway

2: Return Trip

#### `adultNum`     <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:green;">Required</mark>

Adult passenger count, the number can be 1-9

#### `childNum`      <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:green;">Required</mark>

Adult passenger count, the number can be 0-8

#### `infantNum`    <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:orange;">Optional</mark>

Reserved, currently not support infant purchase

#### `fromCity`      <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

IATA Code of departure city

#### `toCity`            <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

IATA Code of arrival city

#### `fromDate`     <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

Departure date, the format is YYYYMMDD

#### `retDate`         <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:orange;">Optional</mark>

Arrival date, the format is YYYYMMDD

Must not be earlier than fromDate. And it can be blank if tripType=1.

#### `requestSource`         <mark style="color:blue;">string</mark>                                                                                                  <mark style="color:orange;">Optional</mark>

Identify the source of the search traffic, E.g. Google Flights, Oganic Search, SkyScanner.
{% endtab %}

{% tab title="Samples" %}
```
{
    "cid": "XXXXXXXX",
    "tripType": "1",
    "adultNum": 1,
    "childNum": 0,
    "infantNum": 0,
    "fromCity": "JKT",
    "toCity": "DPS",
    "fromDate": "20220210",
    "retDate": "",
    "requestSource": "Organic"
}
```
{% endtab %}
{% endtabs %}

## Response&#x20;

{% tabs %}
{% tab title="Schema" %}
#### `status`     <mark style="color:blue;">int</mark>                                                                                                                         &#x20;

0: success

1: request data format error

2: route is forbidden

3: unauthorized access

#### `msg`        <mark style="color:blue;">string</mark>                                                                                                                   &#x20;

Error message

#### `routings`   Array<[Routing Element](search.md#route-element-schema)>                                                                                               <mark style="color:blue;"></mark>                                                                                              &#x20;

The array of the routings which include suitable flights and fares. Click [<mark style="color:red;">here</mark> ](search.md#route-element-schema)to check the schema
{% endtab %}

{% tab title="Samples" %}
```
{
    "status":0,
    "msg":"success",
    "routings":[
        {
            "routingIdentifier":"",
            "supportCreditTransPayment":"0",
            "currency":"USD",
            "adultPrice":16.46,
            "adultTax":10.98,
            "childPrice":16.46,
            "childTax":10.98,
            "InfantPrice":0,
            "InfantTax":0,
            "transactionFeePerPax":2,
            "nationalityType":0,
            "nationality":"",
            "suitAge":"",
            "PaxType":"ADT",
            "fromSegments":[
                {
                    "carrier":"IW",
                    "flightNumber":"IW1848",
                    "depAirport":"DPS",
                    "depTime":"202202041210",
                    "arrAirport":"LOP",
                    "arrTime":"202202041250",
                    "stopCities":"",
                    "duration":40,
                    "codeShare":false,
                    "cabin":"",
                    "cabinClass":1,
                    "seatCount":4,
                    "aircraftCode":"",
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
                        "refNoshowFee":0
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
                    "productCode":"BAG_IW_1_1P_10KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":18.61,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":10,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":1,
                    "productCode":"BAG_IW_1P_15KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":26.8,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":15,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":1,
                    "productCode":"BAG_IW_1_1P_20KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":37.22,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":20,
                        "isAllWeight":true
                    }
                }
            ],
            "vendorFare":null
        },
       {
            "routingIdentifier":"",
            "supportCreditTransPayment":"0",
            "currency":"USD",
            "adultPrice":31.56,
            "adultTax":21.04,
            "childPrice":31.56,
            "childTax":21.04,
            "InfantPrice":0,
            "InfantTax":0,
            "transactionFeePerPax":2,
            "nationalityType":0,
            "nationality":"",
            "suitAge":"",
            "PaxType":"ADT",
            "fromSegments":[
                {
                    "carrier":"JT",
                    "flightNumber":"JT919",
                    "depAirport":"DPS",
                    "depTime":"202202040835",
                    "arrAirport":"SUB",
                    "arrTime":"202202040830",
                    "stopCities":"",
                    "duration":55,
                    "codeShare":false,
                    "cabin":"",
                    "cabinClass":1,
                    "seatCount":4,
                    "aircraftCode":"",
                    "depTerminal":"",
                    "arrTerminal":"",
                    "operatingCarrier":"",
                    "operatingFlightnumber":""
                },
                {
                    "carrier":"JT",
                    "flightNumber":"JT822",
                    "depAirport":"SUB",
                    "depTime":"202202040930",
                    "arrAirport":"LOP",
                    "arrTime":"202202041135",
                    "stopCities":"",
                    "duration":65,
                    "codeShare":false,
                    "cabin":"",
                    "cabinClass":1,
                    "seatCount":4,
                    "aircraftCode":"",
                    "depTerminal":"",
                    "arrTerminal":"",
                    "operatingCarrier":"",
                    "operatingFlightnumber":""
                }
            ],
            "retSegments":[

            ],
            "rule":{
                "hasBaggage":1,
                "baggageElements":[
                    {
                        "segmentNo":1,
                        "passengerType":0,
                        "baggagePiece":0,
                        "baggageWeight":20
                    },
                    {
                        "segmentNo":2,
                        "passengerType":0,
                        "baggagePiece":0,
                        "baggageWeight":20
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
                        "refNoshowFee":0
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
                    "productCode":"BAG_JT_DPS-SUB_1,2,3_1P_10KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":12.27,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":10,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":1,
                    "productCode":"BAG_JT_DPS-SUB_1,2,3_1P_15KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":17.91,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":15,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":1,
                    "productCode":"BAG_JT_DPS-SUB_1,2,3_1P_20KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":23.55,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":20,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":1,
                    "productCode":"BAG_JT_DPS-SUB_1,2,3_1P_30KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":34.83,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":30,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":2,
                    "productCode":"BAG_JT_SUB-LOP_1,2,3_1P_10KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":14.39,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":10,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":2,
                    "productCode":"BAG_JT_SUB-LOP_1,2,3_1P_15KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":21.09,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":15,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":2,
                    "productCode":"BAG_JT_SUB-LOP_1,2,3_1P_20KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":27.78,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":20,
                        "isAllWeight":true
                    }
                },
                {
                    "segmentIndex":2,
                    "productCode":"BAG_JT_SUB-LOP_1,2,3_1P_30KG",
                    "productName":"Baggage",
                    "productType":1,
                    "price":41.17,
                    "currency":"USD",
                    "auxBaggageElement":{
                        "piece":1,
                        "weight":30,
                        "isAllWeight":true
                    }
                }
            ],
            "vendorFare":null
        }
   ]
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}


#### The search results will include a lot of items. Some highlights are: &#x20;

* The returned currency is by configuration according to the business agreement between you and Atlas.&#x20;
* The total cost to purchase for a single adult passenger is: `adultPrice` + `adultTax` + `transactionFeePerPax`&#x20;
* For the airlines which support pass through payment method, we would set `supportCreditTransPayment` to `1` and present the vendor's fare in the `vendorFare` element. Alternatively, if the airline doesn't support pass through payment method, we would set `supportCreditTransPayment` to `0` and the `vendorFare` element will be `null`.&#x20;
* You can choose to show or hide `ancillaryProductElements` in search response, according to the configuration of each client in the backend system.&#x20;
{% endhint %}

### Route Element Schema

{% tabs %}
{% tab title="Schema" %}


#### `routingIdentifier`     <mark style="color:blue;">string</mark>                                                                                                    &#x20;

This unique string identifier is used to verify requests for a particular route.



#### `supportCreditTransPayment`   <mark style="color:blue;">string</mark>

This tag is used to identify if the fare needs to be paid using the client's credit card. If it is set to 1, then the API will allow you to pass through client’s credit card details for payment. If it is set to 0, the credit card details will not be passed through.



#### `currency`    <mark style="color:blue;">string</mark>

The currency in which Atlas settles transactions with you.



#### `adultPrice`   <mark style="color:blue;">decimal</mark>

Adult fare per passenger.



#### `adultTax`      <mark style="color:blue;">decimal</mark>

Adult tax per passenger.



#### `childPrice`   <mark style="color:blue;">decimal</mark>

Child fare per passenger.



#### `childTax`     <mark style="color:blue;">decimal</mark>

Child tax per passenger.



#### `InfantPrice`    <mark style="color:blue;">decimal</mark>

Reserved, currently does not support infant purchase.



#### `InfantTax`     <mark style="color:blue;">decimal</mark>

Reserved, currently does not support infant purchase.



#### `transactionFeePerPax`    <mark style="color:blue;">decimal</mark>

Technical service fee per passenger.



#### `nationalityType`     <mark style="color:blue;">int</mark>

Nationality limitation type

0 No Limitation

1 Allowed

2 Forbidden



#### `nationality`     <mark style="color:blue;">string</mark>

This is nationality limitation value, pass the IATA country code, use a comma if more than one country. Blank means there is no limitation.



#### `suitAge`       <mark style="color:blue;">string</mark>

Passenger age limitation format is 12-24. Blank means no limitation.



#### `paxType`      <mark style="color:blue;">string</mark>

Currently, only ADT fare is available.



#### `fromSegments`      Array<[Segment Element](search.md#3.-segment-element-schema)>

For outbound segments, click [<mark style="color:red;">**here**</mark> ](search.md#segment-element-schema)to check the schema



#### `retSegments`         Array<[Segment Element](search.md#3.-segment-element-schema)>

For inbound segments, click [<mark style="color:red;">**here**</mark> ](search.md#segment-element-schema)to check the schema



#### `rule`               Object<[RuleElement](search.md#5.-rule-element-schema)>

Pass `RuleElement` info for every booking to include the standard details such as baggage allowance, refund rules, change rules for the selected airline. Click [here](file://api-reference/shopping-and-ticketing/search#rule-element-schema) to check the schema.&#x20;



#### `ancillaryProductElements`    Array<[AncillaryProductElement](search.md#9.-ancillaryproduct-element-schema)>

Currently only baggage is available in ancillaries.



#### `AncillaryProductElement` includes the following parameters:&#x20;

*   #### `segmentIndex`                              <mark style="color:blue;">int</mark>

    Segment sequence, start from 1. If it is return trip, sequence outbound and inbound together.
*   #### `productCode`                                <mark style="color:blue;">string</mark>

    Unique identifier for the ancillary product. It would be used in the order request.
*   #### `productName`                                <mark style="color:blue;">string</mark>

    Ancillary product name.
*   #### `productType`                                 <mark style="color:blue;">int</mark>

    Ancillary product type

    1: baggage

    Currently, only baggage is available.
*   #### `price`                                                <mark style="color:blue;">decimal</mark>

    Price for this ancillary.
*   #### `currency`                                          <mark style="color:blue;">string</mark>

    The currency in which Atlas settles transactions with you.
* #### `auxBaggageElement`                 Object<[AuxBaggageElement](search.md#10.-auxbaggage-element-schema)>
  * #### `AuxBaggageElement` includes the following parameters
    *   #### `piece`                                                 <mark style="color:blue;">int</mark>

        0：No Limitation about piece;

        \>0：Maximum pieces
    *   #### `weight`                                            <mark style="color:blue;">int</mark>

        Value mentions maximum weight for ancillary baggage; this should be greater than 0.
    *   #### `isAllWeight`                                   <mark style="color:blue;">boolean</mark>

        True：The weight is for all the pieces

        False：The weight is for each piece





#### `vendorFare`     Object<[VendorFare Element](search.md#4.-vendorfare-element-schema)>

To identify the vendor’s fare with vendor’s currency. It is only available when `supportCreditTransPayment` = 1.



#### &#x20;[VendorFare Element](file://api-reference/shopping-and-ticketing/search#4.-vendorfare-element-schema)&#x20;

*   #### `vendorAdultPrice`         <mark style="color:blue;">decimal</mark>

    Adult fare per passenger in vendor’s currency.
*   #### `vendorAdultTax`             <mark style="color:blue;">decimal</mark>

    Adult tax per passenger in vendor’s currency.
*   #### `vendorChildPrice`          <mark style="color:blue;">decimal</mark>

    Child fare per passenger in vendor’s currency.
*   #### `vendorChildTax`              <mark style="color:blue;">decimal</mark>

    Child tax per passenger in vendor’s currency.
*   #### `vendorCurrency`             <mark style="color:blue;">string</mark>

    This is the currency in which your customers will do transaction with you.

&#x20;
{% endtab %}
{% endtabs %}

### Segment Element Schema

{% tabs %}
{% tab title="Schema" %}
#### `carrier`                       <mark style="color:blue;">string</mark>                                                                                                    &#x20;

IATA code of airline.



#### `flightNumber`         <mark style="color:blue;">string</mark>

Value denotes flight number. The format is: CA123 or TR021 or FR1290, the letters denote the carrier and the three/four-digit number that follows is the flight number.



#### `depAirport`              <mark style="color:blue;">string</mark>

IATA code of departure airport.



#### `depTime`                  <mark style="color:blue;">string</mark>

Departure time of the flight. The format is ：yyyyMMddHHmm, 202203100300 means 10MAR2022 03:00



#### `arrAirport`                <mark style="color:blue;">string</mark>

IATA code of arrival airport.



#### `arrTime`                    <mark style="color:blue;">string</mark>

Arrival time of the flight. The format is ：yyyyMMddHHmm, 202203100300 means 10MAR2022 03:00



#### `stopCities`              <mark style="color:blue;">string</mark>

Name of cities from where the passengers will take connecting flights. Include IATA code of cities and use a comma in case of multiple cities to separate transfer airports count is higher than 1. For example: CGK, SUB. Blank means non-stop flight.



#### `duration`               <mark style="color:blue;">int</mark>

The flying duration in minutes.



#### `codeShare`              <mark style="color:blue;">boolean</mark>

True : code share

False : Not code share



#### `cabin`                         <mark style="color:blue;">string</mark>

Booking code for the fare. For the LCCs which do not provide cabin options, the cabin string will be blank.



#### `cabinClass`             <mark style="color:blue;">int</mark>

Service grade of the fare

1 : Economy

2 : Business

3 : First Class



#### `seatCount`              <mark style="color:blue;">int</mark>

Remaining seats for the fare.



#### `aircraftCode`          <mark style="color:blue;">string</mark>

This value identifies the aircraft model, which is the IATA aircraft code. For example, Airbus A380 = 388, Airbus A350 = 351.



#### `depTerminal`            <mark style="color:blue;">string</mark>

Departure terminal.



#### `arrTerminal`               <mark style="color:blue;">string</mark>

Arrival terminal.



#### `operatingCarrier`     <mark style="color:blue;">string</mark>

Operating carrier. It is blank when `codeshare=false`

``

#### `operatingFlightnumber`      <mark style="color:blue;">string</mark>

Operating flight number. It is blank when `codeshare=false`

``
{% endtab %}
{% endtabs %}

### Rule Element Schema

{% tabs %}
{% tab title="Schema" %}
#### `hasBaggage`                                                         <mark style="color:blue;">int</mark>&#x20;

This tag is used to identify if the fare includes free checked-in baggage.&#x20;

0: Not included&#x20;

1: Included&#x20;





#### `BaggageElements`                                                 Array<<mark style="color:blue;">BaggageElement</mark>>&#x20;

Free checked-in baggage information included in the fare.&#x20;

[BaggageElement](file://api-reference/shopping-and-ticketing/search#6.-baggage-element-schema)&#x20;



#### `segmentNo`                                            <mark style="color:blue;">int</mark>&#x20;

Segment sequence, start from 1.&#x20;

If it is roundtrip, sequence outbound and inbound together.&#x20;



#### `passengerType`                                    string&#x20;

0: ADT&#x20;

1: CHD&#x20;

2: INF&#x20;

If search or verify requested for ADT only, then only ADT is returned.&#x20;

If search or verify requested for ADT+CHD, then ADT and CHD are returned.&#x20;



#### `baggagePiece`                                        int&#x20;

Baggage pieces:&#x20;

0: No limitation on the number of pieces&#x20;

\>0: Maximum pieces&#x20;



#### `baggageWeight`                                     int&#x20;

Baggage Weight, in KGs is mentioned if the airline offers free check-in baggage.&#x20;

&#x20;    0: No free baggage&#x20;





#### &#x20;`refundRules`                                                           Array\<RefundElement> &#x20;

Refer to refund rules as mentioned in Refund Element. &#x20;

[RefundElement](file://api-reference/shopping-and-ticketing/search#7.-refund-element-schema)&#x20;



#### `refundType`                                           int&#x20;

0: Wholly unused ticket&#x20;

1: Partially used ticket (For example, when the passenger has used an outbound flight and wants to refund an inbound flight.)&#x20;



#### `refundStatus`            string&#x20;

Refund rule types:&#x20;

T: Non refundable&#x20;

H: Refundable with restrictions&#x20;

F: Free for refund&#x20;



#### `refundFee`                                                 decimal&#x20;

Refund fee&#x20;

If refundStatus = H, it should not be null&#x20;

If refundStatus = T/F, it can be null.&#x20;



#### `currency`                                                    string&#x20;

The currency in which Atlas settles transactions with you, if refundStatus = H&#x20;



#### `refNoshow`                                                 string&#x20;

Refund status in case of no show&#x20;

T: Non refundable&#x20;

H: Refundable with restrictions&#x20;

F: Free for refund&#x20;



#### `refNoShowCondition`                                 string&#x20;

Time before scheduled flight departure, by which passenger(s) need to check in.&#x20;



#### `refNoshowFee`                                             string&#x20;

Total refund fee in case of no show&#x20;

If refNoshow = H, it should not be null&#x20;

&#x20;                       This value includes the refund fee and no-show penalty&#x20;





#### `changesRules`                                                              Array\<ChangesElement>&#x20;

This function is used to fetch the change rules of the selected airline.&#x20;

[ChangesElement](file://api-reference/shopping-and-ticketing/search#8.-change-element-schema)&#x20;



#### `changesType`    int&#x20;

Change flight type&#x20;

0: Wholly unused ticket&#x20;

1: Partially used ticket (For example, when the passenger has used an outbound flight and wants to refund an inbound flight)&#x20;



#### `changesStatus`   string&#x20;

Change flight rule type&#x20;

T: Non changeable&#x20;

H: Changeable with restrictions&#x20;

F: Free for change flight&#x20;



#### `changesFee`    decimal&#x20;

Change flight fee&#x20;

If changesStatus = H, it should not be null&#x20;

If changesStatus = T/F, it can be null&#x20;



#### `currency`    string&#x20;

The currency in which Atlas settles transactions with you.&#x20;

If changesStatus = H, it should not be null&#x20;



#### `refNoshow`                                                 string &#x20;

Change flight rule in case of no show.&#x20;

T: Non changeable&#x20;

H: Changeable with restrictions&#x20;

F: Free for change flight&#x20;



#### `refNoShowCondition`      int&#x20;

Time before scheduled flight departure, by which passenger(s) need to check in.&#x20;



#### `refNoshowFee`      string&#x20;

The total fee charged to change flight in case of no show.&#x20;

If refNoshow = H, it should not be null.&#x20;

This value includes the change flight fee and no-show penalty.&#x20;
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

#### 3.1. Free checked-in baggage

The free checked-in baggage allowance for each fare is available within both `search` and the `verify` response.

{% tabs %}
{% tab title="Schema" %}
#### Baggage Element

*   #### segmentNo                              <mark style="color:blue;">int</mark>

    Segment sequence, start from 1.

    If it is roundtrip, sequence outbond and inbound together.
*   #### passengerType                     <mark style="color:blue;">string</mark>

    0: ADT

    1: CHD

    2: INF

    If search or verify for ADT only, then only ADT is returned;

    If search or verify for ADT+CHD, then ADT and CHD are returned.
*   #### baggagePiece                        <mark style="color:blue;">int</mark>

    Baggage pieces：

    0  No limitation

    \>0 Maximum pieces
*   #### baggageWeight                    <mark style="color:blue;">int</mark>

    Baggage Weight, with the unit of KG

    0  means No Free baggage
{% endtab %}

{% tab title="Samples" %}
```json
{
...,
"rule": {
                "hasBaggage": 1,
                "baggageElements": [
                    {
                        "segmentNo": 1,
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 20
                    },
                    {
                        "segmentNo": 1,
                        "passengerType": 1,
                        "baggagePiece": 0,
                        "baggageWeight": 20
                    },
                    {
                        "segmentNo": 2,
                        "passengerType": 0,
                        "baggagePiece": 0,
                        "baggageWeight": 20
                    },
                    {
                        "segmentNo": 2,
                        "passengerType": 1,
                        "baggagePiece": 0,
                        "baggageWeight": 20
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
#### ancillaryProductElement

*   #### segmentIndex                              <mark style="color:blue;">int</mark>

    Segment sequence, start from 1

    If it is return trip, sequence outbond and inbound together
*   #### productCode                                <mark style="color:blue;">string</mark>

    Unique identifier for the ancillary product

    It would be used in the order request
*   #### productName                                <mark style="color:blue;">string</mark>

    Ancillary product name
*   #### productType                                 <mark style="color:blue;">int</mark>

    Ancillary product type

    1: baggage

    Currently only baggage is available
*   #### price                                                 <mark style="color:blue;">decimal</mark>

    Price for this ancillary
*   #### currency                                          <mark style="color:blue;">string</mark>

    Currency for this price
* #### auxBaggageElement                 Object<<mark style="color:blue;">AuxBaggageElement</mark>>
  * #### AuxBaggageElement
    *   #### piece                                                 <mark style="color:blue;">int</mark>

        0：No Limitation about pieces

        \>0：Maximum pieces
    *   #### weight                                             <mark style="color:blue;">int</mark>

        Maximum weight for ancillary baggage;

        Should be greater than 0
    *   #### isAllWeight                                   <mark style="color:blue;">boolean</mark>

        True：The weight is for all the pieces;

        False：The weight is for each piece
{% endtab %}

{% tab title="Samples" %}
```json
 "ancillaryProductElements": [
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
                },
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
                    "segmentIndex": 2,
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
                }
            ]
```
{% endtab %}
{% endtabs %}

