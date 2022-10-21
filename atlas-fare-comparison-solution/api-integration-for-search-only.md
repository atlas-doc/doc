---
cover: ../.gitbook/assets/ATL_002_Gitbook-headers_Atlas_Search.png
coverY: 0
---

# API Integration For Search Only

Integrate with the Atlas Search API in under 4 hours and start searching for air fares from over 100 low-cost carriers.

### Overview

We want to help you test the Atlas API and arrive at a decision which you feel confident about. Manually comparing air fares for a combination of flight routes across carriers can be overwhelming. We make it easy for you with the Atlas Search API.

Your developer can integrate with the search API in 0.5 man-days and once integrated you can complete a comprehensive, automated fare comparison within 30 mins.

It is a simple four-step process:

![](<../.gitbook/assets/ATL-002\_API integration for search.png>)

{% hint style="info" %}
The Atlas quotation consists of the following four parameters:

**Currency:**&#x20;

* Atlas will configure currency to the one requested in your application.

**FarePrice**:&#x20;

* The fare you see is the same as the airline official price converted to your preferred currency using the market exchange rate.

**Tax:**&#x20;

* The tax is same as the airline official tax converted to your preferred currency using the market exchange rate.

**Booking Fee (Technical Service fee):**

* Please note the technical service fee will show as $0 for you. The transaction fee will be set as per the contractual agreement between Atlas and your company.
{% endhint %}

## 1. Get Atlas Sandbox Credentials

To create your Atlas Sandbox Credentials, submit your Search API application with the following three parameters:

* Company name
* Email Address
* Fare Quote Currency

You will receive the credentials in two parts: `x-atlas-client-id` and `x-atlas-client-secret`.

Any request you initiate needs to be authenticated using your API credentials. The API will return an error for any request without valid API credentials in the header.

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

    Enter return date if tripType = 2, the format is YYYYMMDD. Must not be earlier than fromDate.
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
The search request will return a lot of parameters. For this example schema we will focus only on the following parameters important for fare search: &#x20;

* Pay more attention to the items in orange, as they are important for fare search
* The returned currency is configured, as requested by you
*   The total cost to purchase a ticket on any route for a single passenger is:

    adultPrice + adultTax + transactionFeePerPax
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



* #### routings   Array<[Routing Element](api-integration-for-search-only.md#route-element-schema)>                                                                                               <mark style="color:blue;"></mark>                                                                                              &#x20;
  * #### [Routing Element](api-integration-for-search-only.md#route-element-schema)
    *   #### currency    <mark style="color:blue;">string</mark>

        Currency, it's configured in the back office according to your demand before apply.&#x20;
    *   #### <mark style="color:orange;">adultPrice</mark>   <mark style="color:blue;">decimal</mark>

        Adult fare per passenger.
    *   #### <mark style="color:orange;">adultTax</mark>      <mark style="color:blue;">decimal</mark>

        Adult tax per passenger.
    *   #### <mark style="color:orange;">transactionFeePerPax</mark>    <mark style="color:blue;">decimal</mark>

        Technical service fee per passenger.
    * #### rule               <mark style="color:orange;"></mark> Object<[RuleElement](api-integration-for-search-only.md#5.-rule-element-schema)>
      *   #### <mark style="color:blue;">RuleElement</mark>   &#x20;

          Rule element includes baggage, refund rules and change rules. For fare search purpose, please pay attention to the following elements:

          *   #### <mark style="color:orange;">hasBaggage</mark>                              <mark style="color:blue;">int</mark>

              This tag is used to identify if the fare includes free checked-in baggage

              0 : Not included

              1 : Included
          *   #### BaggageElements                 Array<[BaggageElement](api-integration-for-search-only.md#6.-baggage-element-schema)>

              Free checked-in baggage information included in the fare.

              * #### [BaggageElement](api-integration-for-search-only.md#6.-baggage-element-schema)
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

                    Baggage Weight, mentioned in KG

                    0 means no free checked-in baggage
    *   #### <mark style="color:orange;">fromSegments</mark>      Array<[Segment Element](api-integration-for-search-only.md#3.-segment-element-schema)>

        The following schema is for outbound segments:

        * #### [Segment Element](api-integration-for-search-only.md#3.-segment-element-schema)
          *   #### carrier                       <mark style="color:blue;">string</mark>                                                                                                    &#x20;

              IATA code of airline.
          *   #### <mark style="color:orange;">flightNumber</mark>         <mark style="color:blue;">string</mark>

              Flight number

              The format is : CA123 or TR021 or FR1290.
          *   #### <mark style="color:orange;">depAirport</mark>             <mark style="color:blue;">string</mark>

              IATA code of departure airport.
          *   #### depTime                  <mark style="color:blue;">string</mark>

              Departure time of the flight in yyyyMMddHHmm format. For example: 202203100300 means 10MAR2022 03:00.
          *   #### <mark style="color:orange;">arrAirport</mark>                <mark style="color:blue;">string</mark>

              IATA code of arrival airport
          *   #### arrTime                     <mark style="color:blue;">string</mark>

              Arrival time of the flight in yyyyMMddHHmm format. For example: 202203100300 means 10MAR2022 03:00.
          *   #### stopCities               <mark style="color:blue;">string</mark>

              Returns IATA code of transit airport for the route. Please note "," is used to separate IATA codes if there are more than one transit airports on the route, e.g. "CGK,SUB".

              Blank means it is a non-stop flight.
          *   #### duration               <mark style="color:blue;">int</mark>

              The flight duration in minutes.
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

              Arrival terminal
          *   #### operatingCarrier     <mark style="color:blue;">string</mark>

              Operating carrier

              It is blank when codeShare=false
          *   #### operatingFlightnumber      <mark style="color:blue;">string</mark>

              Operating flight number

              It is blank when codeShare=false
    *   #### <mark style="color:orange;">retSegments</mark>         Array<[Segment Element](api-integration-for-search-only.md#3.-segment-element-schema)>

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

Download the <mark style="color:blue;">Postman collection</mark> bellow to check the samples for UAT and add your observations in the **Comments** column. Then send it to your account manager to request the UAT Certification.

| Search Condition              | Decription                                      | Comments                                                                           |
| ----------------------------- | ----------------------------------------------- | ---------------------------------------------------------------------------------- |
| SEL-CJU 24FEB/28FEB Roundtrip | One-way with both direct and connecting flights | Number of routings returned: (to be filled-up by you)                              |
| SEL-CJU 24FEB/28FEB Roundtrip | Roundtrip with different airlines               | <p>Departure Date:</p><p>Number of routings returned: (to be filled-up by you)</p> |

{% file src="../.gitbook/assets/Atlas Sandbox SearchOnly UAT.postman_collection.json.zip" %}

## Start LIVE Search

Your Atlas account manager will check the UAT submission at the earliest and respond with the live credentials if the UAT is successful. Please replace the endpoint, and the login credentials `x-atlas-client-id` and `x-atlas-client-secret` in your program to start your live search.

{% hint style="info" %}
The following restrictions apply to live search:

* Queries per second QPS <= 2
* Hits per day < 10000
* The live credential will be available for 7 days.
{% endhint %}
