# Search API Integration for Fare Search

## Overview

Atlas understands that the customer wants to check the flights and fares which Atlas provides before a business decision is made to use the content.

We also understand that it is difficult to compare the routes, flights and fares one by one manually even if a web portal is provided.

The effort to integrate the search API is equivalent to 0.5 man-days of a developer’s time. Once integrated, a comprehensive fare comparison can be completed within 30 minutes in an automated manner.

The workflow to achieve this is as below:

![](../.gitbook/assets/Search_Only_API_workflow2.png)

{% hint style="info" %}
Atlas quotation consists of four parts as mentioned below :

* <mark style="color:blue;">Currency</mark>   &#x20;

&#x20;      Configured according to your demand during your application for fare comparison integration.

* <mark style="color:blue;">FarePrice</mark> &#x20;

&#x20;     The same as airline official price converted to your selected currency using the market FX rate.

* <mark style="color:blue;">Tax</mark>           &#x20;

&#x20;      The same as airline official tax converted to your selected currency using the market FX rate.

* <mark style="color:blue;">Technical Service fee (Booking Fee)</mark>     &#x20;

&#x20;      $0 in comparison results. For real transaction, the value will be set according to the contractual agreement between Atlas and your company.
{% endhint %}

## 1. Get Atlas Sandbox Credential

The Sandbox API credentials or the API key can be created by yourself via ATRIP. Access the "Profile" section and then in "My Profile" sub-section, click on the "Customer Information" tab. The "Generate" button should be clicked and the sandbox credentials will be automatically created. 

The API credentials contain two items : <mark style="color:green;">x-atlas-client-id</mark> and <mark style="color:green;">x-atlas-client-secret.</mark>

The API requests are authenticated using the API credentials. Any request that doesn't include an API credential will return an error.

Please add the API credentials in the header of each <mark style="color:blue;">**post**</mark> request.

## 2. Finish the search API integration

### 1) Endpoint

[https://sandbox.atriptech.com/search.do](https://sandbox.atriptech.com/search.do)

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

    Identifier of client and user. Please use x-atlas-client-id to fill in.
*   #### tripType      <mark style="color:blue;">string</mark>                                                                                                                  <mark style="color:green;">Required</mark>

    1: Oneway

    2: Return Trip
*   #### adultNum     <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:green;">Required</mark>

    Adult passenger count. The number can be 1-9
*   #### childNum      <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:green;">Required</mark>

    Child passenger count. The number can be 0-8
*   #### infantNum    <mark style="color:blue;">int</mark>                                                                                                                       <mark style="color:orange;">Optional</mark>

    Infant passenger count. The number can be 0-8
*   #### fromCity      <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

    IATA Code of departure city
*   #### toCity            <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

    IATA Code of arrival city
*   #### fromDate     <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:green;">Required</mark>

    Departure date. The format is YYYYMMDD
*   #### retDate         <mark style="color:blue;">string</mark>                                                                                                                 <mark style="color:orange;">Optional</mark>

    Arrival date. The format is YYYYMMDD

    Must not be earlier than "fromDate". It can be blank if "tripType=1".
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
    "retDate": "",
    "airlines": ["JT", "ID"],
    "requestSource": "Organic"
}
```
{% endtab %}
{% endtabs %}

### 4) Response

{% hint style="info" %}
The search results will include a lot of items. This schema will only pick up the items which are helpful in the fare comparison process : &#x20;

* Please pay more attention on the items in orange which would be important in terms of fare comparison
* The currency in which the results are returned currency is according to your request during your application for fare comparison integration
* The total cost of the fare for a single passenger is as follows:

&#x20;     adultPrice + adultTax + transactionFeePerPax
{% endhint %}

{% tabs %}
{% tab title="Schema" %}
*   #### status     <mark style="color:blue;">int</mark> 

0: success

1: request data format error

2: route is forbidden

3: unauthorized access

*   #### msg         <mark style="color:blue;">string</mark>  

Error message

The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.

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
              4 : Premium Ecocnomy
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
  "routings": [
    {
      "fid": "E96Zg5Lr4XQxVimN0_rhFeZULZ_HVT5DXZo6cPTdQrVod3ISQRlb4thdb239v6gV",
      "routingIdentifier": "IMBJh2LCiGucW/2fPoF4vPMRYyg0zjCX46VwnmDdMe+jn0SjHfR2nG/JWOkMaBeWTD2rDYRcqpu+y/YaX10pmxKn2tUuttY+1HfJLgz0LHI7LnOZ2jrdvSBEvOFFovPyBKlSp2XhW3lhu4n5bTSW67m2QQZVOrWrEsGNhmm8v+j4dHlFLH6/Y7xKzPl7i52mnGIbZR4pWe0/j4n8fX4J5VlodBwhKkOgK3MRf65LxvKKACMZha4JVAxOEnkHDfFZ7KsmGZnBHUyCee/FIdOnQLx74DLLMAEu0pzoU80F/Basafezl/tBV1hB9xDk1Zs39RhJk+U7YU0=",
      "supportCreditTransPayment": "0",
      "currency": "USD",
      "adultPrice": 28.59,
      "adultTax": 16.17,
      "childPrice": 28.59,
      "childTax": 16.17,
      "infantPrice": 32.8,
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
          "carrier": "EC",
          "flightNumber": "EC7846",
          "depAirport": "STN",
          "depTime": "202304151930",
          "arrAirport": "AMS",
          "arrTime": "202304152135",
          "stopCities": "",
          "duration": 65,
          "codeShare": false,
          "cabin": "",
          "cabinClass": 1,
          "seatCount": 4,
          "aircraftCode": "",
          "depTerminal": "",
          "arrTerminal": "",
          "operatingCarrier": "",
          "operatingFlightnumber": "",
          "fareFamily": "Standard"
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
            "baggageSize": "40*25*20cm"
          }
        ],
        "refundRules": [
          {
            "refundType": 0,
            "refundStatus": "H",
            "refundFee": 83.01,
            "currency": "SGD",
            "refNoshow": "H",
            "refNoShowCondition": 0,
            "refNoshowFee": 83.01,
            "ruleList":[],
            "ruleDetailList": [
                            {
                                "ruleId": 1993,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": -4320,
                                "amount": 30.0,
                                "currency": "SGD"
                            },
                            {
                                "ruleId": 1996,
                                "status": "H",
                                "startMinute": -4320,
                                "endMinute": -240,
                                "amount": 46.12,
                                "currency": "SGD"
                            },
                            {
                                "ruleId": 1999,
                                "status": "H",
                                "startMinute": -240,
                                "endMinute": 0,
                                "amount": 83.01,
                                "currency": "SGD"
                            },
                            {
                                "ruleId": 2002,
                                "status": "H",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 83.01,
                                "currency": "SGD"
                            }
        ],
        "changesRules": [
          {
            "changesType": 0,
            "changesStatus": "H",
            "changesFee": 83.01,
            "currency": "SGD",
            "revNoshow": "H",
            "revNoShowCondition": 0,
            "revNoshowFee": 83.01,
            "ruleList":[],
            "ruleDetailList": [
                            {
                                "ruleId": 1993,
                                "status": "H",
                                "startMinute": 525600,
                                "endMinute": -4320,
                                "amount": 30.0,
                                "currency": "SGD"
                            },
                            {
                                "ruleId": 1996,
                                "status": "H",
                                "startMinute": -4320,
                                "endMinute": -240,
                                "amount": 46.12,
                                "currency": "SGD"
                            },
                            {
                                "ruleId": 1999,
                                "status": "H",
                                "startMinute": -240,
                                "endMinute": 0,
                                "amount": 83.01,
                                "currency": "SGD"
                            },
                            {
                                "ruleId": 2002,
                                "status": "H",
                                "startMinute": 0,
                                "endMinute": -525600,
                                "amount": 83.01,
                                "currency": "SGD"
                            }
                        ]
      },
      "ancillaryProductElements": [
        {
          "segmentIndex": 1,
          "endSegmentIndex": null,
          "productCode": "SCI_BAG_1PC_15KG",
          "productName": "StandardCheckInBaggage",
          "productType": 1,
          "canPurchaseWithTicket": 1,
          "canPurchasePostTicket": 1,
          "price": 31.7,
          "currency": "USD",
          "vendorPrice": 25.49,
          "vendorCurrency": "GBP",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 15,
            "isAllWeight": true,
            "size": ""
          },
          "offerId": null,
          "maxQty": 1,
          "minQty": 1,
          "categoryCode": "StandardCheckInBaggage",
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
          "price": 37.16,
          "currency": "USD",
          "vendorPrice": 29.89,
          "vendorCurrency": "GBP",
          "clientTechnicalServiceFee": 0,
          "auxBaggageElement": {
            "piece": 1,
            "weight": 23,
            "isAllWeight": true,
            "size": "56*36*23cm"
          },
          "offerId": null,
          "maxQty": 1,
          "minQty": 1,
          "categoryCode": "StandardCheckInBaggage",
          "ancillaryCode": "SCI_BAG_1PC_23KG"
        }
      ],
      "vendorFare": null,
      "bundleOptions": [],
      "links": null,
      "separateBookings": false
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

Pass `RuleElement` info for every booking to include the standard details such as baggage allowance, refund rules and change rules for the selected airline. Click [here](file://api-reference/shopping-and-ticketing/search#rule-element-schema) to check the schema.

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
        
*   **`offerId`  **<mark style="color:blue;">**string**</mark>

The identifier of the offer of ancillary product. This will be "null" in the booking flow but will have an id in the post-ticketing flow.

*   **`maxQty`  **<mark style="color:blue;">**string**</mark>

Maximum purchase quantity per product

*   **`minQty`  **<mark style="color:blue;">**string**</mark>

Starting purchase quantity per product

*   **`size`  **<mark style="color:blue;">**string**</mark>

Maximum size for ancillary baggage

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

**`operatingFlightnumber`  **<mark style="color:blue;">**string**</mark>

Operating flight number. It is blank when `codeshare=false`

**`fareFamily`  **<mark style="color:blue;">**string**</mark>

Fare Family as per the information received from the airline.

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

```
0 : No free baggage
-1: No limitation on weight. 
```

**`baggageSize` **<mark style="color:blue;">**string**</mark>

Baggage Size: 

length＊width＊height and units. eg. "56＊36＊23cm", "18＊14＊8inch". 

Or Total dimensions (length + width + height) of each piece. eg. "L+W+H<=158cm". 

Empty means no limitation.

**`refundRules` Array<RefundElement>**

Refer to refund rules as mentioned in Refund Element. 

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

```
                   This value includes the refund fee and no-show penalty
```
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

**`changesRules` Array<ChangesElement>**

This function is used to fetch the change rules of the selected airline.

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

{% endtab %}
{% endtabs %}

## 3. UAT Certification

Download the <mark style="color:blue;">Postman collection</mark> below to check the samples for UAT and add your observations in the **Comments** column. Then upload the information in ATRIP "Requests" section and send the service request number to your account manager to request the UAT Certification.

| Search Condition  | Decription                                                                                   | Comments                                                                                                                                       |
| ----------------- | -------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| DVO-CEB Oneway    | One-way with both direct and connecting flights with departure date of 7 days later          | <p>Departure Date:</p><p>Number of routings returned: (<mark style="color:red;">to be filled-up by the customer</mark>)</p>                    |
| SEL-CJU Roundtrip | Roundtrip of different airlines with departure date of 7 days later and return within 3 days | <p>Departure Date:</p><p>Return Date:</p><p>Number of routings returned: (<mark style="color:red;">to be filled-up by the customer</mark>)</p> |

The Postman collection below can also be downloaded to check the samples:


> [Atlas Sandbox SearchOnly UAT.postman\_collection.json.zip](../.gitbook/assets/Atlas Sandbox SearchOnly UAT.postman_collection.json.zip)
{% hint style="info" %}
Please right click on the above link and click "Open link in new window". The file will start downloading.
{% endhint %}

## 4. Start LIVE Search

The Atlas account manager will check the UAT submission at the earliest and respond back with the live credentials if the UAT tests have been completed successfully.

Please replace the <mark style="color:green;">endpoint</mark>, as well as the <mark style="color:green;">x-atlas-client-id</mark> and <mark style="color:green;">x-atlas-client-secret</mark> in your program, and start your LIVE search.

{% hint style="info" %}
The restrictions for fare comparison live search are as below:

* QPS <= 2
* Hits per day < 10000
* Credential available for 7 days
{% endhint %}
