# Search API Integration for Fare Comparison

## Overview

Atlas understands that the customer wants to check the flights and fares which Atlas provides before a business decision is made to use the content.

We also understand that it is difficult to compare the routes, flights and fares one by one manually even if a web portal is provided.

The effort to integrate the search API is equivalent to 0.5 man-days of a developer’s time. Once integrated, a comprehensive fare comparison can be finished within 30 minutes in an automated manner.

The workflow to achieve this is as below:

![](<../.gitbook/assets/Search Only API workflow (5).jpg>)

{% hint style="info" %}
Atlas quotation consists of four parts as mentioned below :

* <mark style="color:blue;">Currency</mark>   &#x20;

&#x20;      Configured according to your demand during your application for fare comparison integration.

* <mark style="color:blue;">FarePrice</mark> &#x20;

&#x20;     The same as airline official price converted to your selected currency using the market FX rate.

* <mark style="color:blue;">Tax</mark>           &#x20;

&#x20;      The same as airline official tax converted to your selected currency using the market FX rate.

* <mark style="color:blue;">Technical Service fee (Booking Fee)</mark>     &#x20;

&#x20;      $0 in comparison results. For real transaction, the value will be set according to the contractual agreement between the Atlas and your company.
{% endhint %}

## 1. Get Atlas Sandbox Credential

The Search API application should be submitted to the Atlas account manager with 3 sets of information as mentioned below. The sandbox API credentials will be created and shared by your account manager.&#x20;

1\) <mark style="color:blue;">Company name</mark>&#x20;

2\) <mark style="color:blue;">Email Address</mark>&#x20;

3\) <mark style="color:blue;">Fare Quote Currency</mark>

The API credentials contain two items : <mark style="color:green;">x-atlas-client-id</mark> and <mark style="color:green;">x-atlas-client-secret.</mark>

The API requests are authenticated using the API credentials. Any request that doesn't include an API credential will return an error.

Please add the API credentials in the header of each <mark style="color:blue;">**post**</mark> request.

## 2. Finish the search API integration

### 1) Endpoint

[https://sandbox.atlaslovestravel.com/search.do](https://sandbox.atlaslovestravel.com/search.do)

### 2) Header

```
x-atlas-client-id ： <Your clientid>
x-atlas-client-secret : <Your client secretid>
Content-Type: application/json
Accept-Encoding: gzip
```

### 3) Request

{% tabs %}
{% tab title="Schema" %}
*   #### cid                 <mark style="color:blue;">string</mark>                                                                                                                  <mark style="color:green;">Required</mark>

    Identifier of client and user, please use x-atlas-client-id to fill in.
*   #### tripType      <mark style="color:blue;">string</mark>                                                                                                                  <mark style="color:green;">Required</mark>

    1: Oneway

    2: Return Trip
*   #### adultNum     <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:green;">Required</mark>

    Adult passenger count, the number can be 1-9
*   #### childNum      <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:green;">Required</mark>

    Adult passenger count, the number can be 0-8
*   #### infantNum    <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:orange;">Optional</mark>

    Reserved, currently not support infant fare quotation.
*   #### fromCity      <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

    IATA Code of departure city
*   #### toCity            <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

    IATA Code of arrival city
*   #### fromDate     <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

    Departure date, the format is YYYYMMDD
*   #### retDate         <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:orange;">Optional</mark>

    Arrival date, the format is YYYYMMDD

    Must not be earlier than fromDate. And it can be blank if tripType=1.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXXX",
    "tripType": "1",
    "adultNum": 1,
    "childNum": 0,
    "infantNum": 0,
    "fromCity": "JKT",
    "toCity": "DPS",
    "fromDate": "20220210",
    "retDate": ""
}
```
{% endtab %}
{% endtabs %}

### 4) Response

{% hint style="info" %}
The search results will include a lot of items. This schema will only pick up the items which are helpful in the fare comparison process : &#x20;

* Please pay more attention on the items in orange which would be important in terms of fare comparison
* The returned currency is by configuration according to your demand during your application for fare comparison integration
* The total cost to purchase this routing for a single passenger is as follows:

&#x20;     adultPrice + adultTax + transactionFeePerPax
{% endhint %}

{% tabs %}
{% tab title="Schema" %}
*   #### status     <mark style="color:blue;">int</mark>                                                                                                                         &#x20;

    0: success

    1: request data format error

    2: route is forbidden

    3: unauthorized access
*   #### msg         <mark style="color:blue;">string</mark>                                                                                                                   &#x20;

    Error message
* #### routings   Array<[Routing Element](search-api-integration-for-fare-comparison.md#route-element-schema)>                                                                                               <mark style="color:blue;"></mark>                                                                                              &#x20;
  * #### [Routing Element](search-api-integration-for-fare-comparison.md#route-element-schema)
    *   #### currency    <mark style="color:blue;">string</mark>

        Currency, it's configured in the back office according to your demand before apply.&#x20;
    *   #### <mark style="color:orange;">adultPrice</mark>   <mark style="color:blue;">decimal</mark>

        Adult fare per passenger.
    *   #### <mark style="color:orange;">adultTax</mark>      <mark style="color:blue;">decimal</mark>

        Adult tax per passenger.
    *   #### <mark style="color:orange;">transactionFeePerPax</mark>    <mark style="color:blue;">decimal</mark>

        Technical service fee per passenger.
    * #### rule               <mark style="color:orange;"></mark> Object<[RuleElement](search-api-integration-for-fare-comparison.md#5.-rule-element-schema)>
      *   #### <mark style="color:blue;">RuleElement</mark>   &#x20;

          This element contains bagggage, refund rules and change rules. For fare comparison purpose, please pay attention to these items below

          *   #### <mark style="color:orange;">hasBaggage</mark>                              <mark style="color:blue;">int</mark>

              A tag to identify if the fare include free checked-in baggage

              0 : Not included

              1 : Included
          *   #### BaggageElements                 Array<[BaggageElement](search-api-integration-for-fare-comparison.md#6.-baggage-element-schema)>

              Free checked-in baggage information included in the fare.

              * #### [BaggageElement](search-api-integration-for-fare-comparison.md#6.-baggage-element-schema)
                *   #### segmentNo                              <mark style="color:blue;">int</mark>

                    Segment sequence. Start from 1.

                    If it is roundtrip, outbound and inbound segments are together in the sequence.
                *   #### passengerType                     <mark style="color:blue;">string</mark>

                    0: ADT

                    1: CHD

                    2: INF

                    If search or verify for ADT only, then only ADT is returned;

                    If search or verify for ADT+CHD, then ADT and CHD are returned.
                *   #### <mark style="color:orange;">baggagePiece</mark>                        <mark style="color:blue;">int</mark>

                    Baggage pieces：

                    0  No limitation

                    \>0 Maximum pieces
                *   #### <mark style="color:orange;">baggageWeight</mark>                   <mark style="color:blue;">int</mark>

                    Baggage Weight, with the unit of KG

                    0  means No Free baggage
    *   #### <mark style="color:orange;">fromSegments</mark>      Array<[Segment Element](search-api-integration-for-fare-comparison.md#3.-segment-element-schema)>

        Outbound segments. Please check the schema below

        * #### [Segment Element](search-api-integration-for-fare-comparison.md#3.-segment-element-schema)
          *   #### carrier                       <mark style="color:blue;">string</mark>                                                                                                    &#x20;

              IATA code of airline.
          *   #### <mark style="color:orange;">flightNumber</mark>         <mark style="color:blue;">string</mark>

              Flight number

              The format is : CA123 or TR021 or FR1290.
          *   #### <mark style="color:orange;">depAirport</mark>             <mark style="color:blue;">string</mark>

              IATA code of departure airport.
          *   #### depTime                  <mark style="color:blue;">string</mark>

              Departure time of the flight.

              The format is yyyyMMddHHmm,&#x20;

              202203100300 means 10MAR2022 03:00.
          *   #### <mark style="color:orange;">arrAirport</mark>                <mark style="color:blue;">string</mark>

              IATA code of arrival airport
          *   #### arrTime                     <mark style="color:blue;">string</mark>

              Arrival time of the flight

              The format is yyyyMMddHHmm,&#x20;

              202203100300 means 10MAR2022 03:00.
          *   #### stopCities               <mark style="color:blue;">string</mark>

              Stop airports of the fight, IATA code, , use "," to separate if transfer airports count is higher than 1. E.g. "CGK,SUB"

              Blank means non-stop flight
          *   #### duration               <mark style="color:blue;">int</mark>

              The flying time of this flight with the unit in minutes.
          *   #### codeShare              <mark style="color:blue;">boolean</mark>

              True : code share

              False : Not code share
          *   #### cabin                         <mark style="color:blue;">string</mark>

              Booking code for the fare

              In terms of the LCCs which do not provide this, the cabin would be blank
          *   #### cabinClass             <mark style="color:blue;">int</mark>

              Service grade of the fare

              1 : Economy

              2 : Business

              3 : First Class
          *   #### seatCount              <mark style="color:blue;">int</mark>

              Remaining seats for the fare.
          *   #### aircraftCode           <mark style="color:blue;">string</mark>

              Aircraft equipment
          *   #### depTerminal            <mark style="color:blue;">string</mark>

              Departure terminal
          *   #### arrTerminal               <mark style="color:blue;">string</mark>

              Arrival terminalal
          *   #### operatingCarrier     <mark style="color:blue;">string</mark>

              Operating carrier

              It is blank when codeShare=false
          *   #### operatingFlightnumber      <mark style="color:blue;">string</mark>

              Operating flight number

              It is blank when codeShare=false
    *   #### <mark style="color:orange;">retSegments</mark>         Array<[Segment Element](search-api-integration-for-fare-comparison.md#3.-segment-element-schema)>

        Inbound segments. The SegmentElement structure is the same as fromSegments
{% endtab %}

{% tab title="Samples" %}
```json
{
    "status":0,
    "msg":"success",
    "routings":[
        {
            "routingIdentifier":"K7jWWc8Rq4ETSMWRHlhxhAMDhwUTz1Ty46VwnmDdMe8ZPZQyz3X0KkJxlQV1LwyENuuoYtO28B5k0QK+Vd8Ib4BmiiHQLzX9R7e0VPq8abH5gxFLgeOVQuerBxMqkOi239OWHU/iXVuggQcrbUJ3uxbMNdvNbRECTVvwV3xXgXl07i/72WQoPpN8EA8lik2pKNEtHMsuVpQDk6Wry7MaHQeNspRYJwDEY7i5tKVoTua5c8VEC8fd0g\u003d\u003d",
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":1,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":1,
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
            "routingIdentifier":"K7jWWc8Rq4ETSMWRHlhxhAMDhwUTz1Ty46VwnmDdMe8+9iUjY985ebmViBmzDc1XBptG/tw8XP3qStiFIM0TkNiO83lw4Go4PlwD34tTdxgo74G3LxIDLb0x2x/GJ+5lqHY8luoccEuvaHoJnXRdq96eRncqBt0fl8vDLAq5k/yfRcs6VgKolBGIC2Ud+VyoPlwD34tTdxhCT5N+M50KbYlJmLtdyVlrkNXMng1ISqaDhGqEzZGB0Xlhz1FL0gDU/9UivpvdJUtdvFy5jyNCOMeylCQHpGoJTbSm1kk+c6Q\u003d",
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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
                    "canPurchaseWithTicket":1,
                    "canPurchasePostTicket":0,
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

## 3. UAT Certification

Please add your observations in the \[Comments] column and then send it to your account manager to request the UAT Certification.

| Search Condition  | Decription                                                                                   | Comments                                                                                                                                       |
| ----------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| DVO-CEB Oneway    | One-way with both direct and connecting flights with departure date of 7 days later          | <p>Departure Date:</p><p>Number of routings returned: (<mark style="color:red;">to be filled-up by the customer</mark>)</p>                    |
| SEL-CJU Roundtrip | Roundtrip of different airlines with departure date of 7 days later and return within 3 days | <p>Departure Date:</p><p>Return Date:</p><p>Number of routings returned: (<mark style="color:red;">to be filled-up by the customer</mark>)</p> |

The Postman collection below can also be downloaded to check the samples:

{% file src="../.gitbook/assets/Atlas Sandbox SearchOnly UAT.postman_collection.json.zip" %}

## 4. Start LIVE Search

The Atlas account manager will check the UAT submission at the earliest and respond back with the live credentials if the UAT tests have been completed successfully.

Please replace the <mark style="color:green;">endpoint</mark>, as well as the <mark style="color:green;">x-atlas-client-id</mark> and <mark style="color:green;">x-atlas-client-secret</mark> in your program, and start your LIVE search.

{% hint style="info" %}
The restrictions for fare comparison live search are as below:

* QPS <= 2
* Hits per day < 10000
* Credential available for 7 days
{% endhint %}
