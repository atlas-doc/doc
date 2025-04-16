# Get Luggage

{% hint style="info" %}

In a booking process, please call the 'getLuggage' API to get precise baggage quotes after price verification via 'verify' or 'getOffer'.  

Steps:

1. API sequence
    - Search - Verify- getLuggage - Order - Pay
    - getOffer - getLuggage - Order - Pay
2. For exact baggage prices, request 'getLuggage'.
3. Pass 'offerId' in 'getLuggage' requests:
    - From 'verify': Use sessionId as offerId
    - From 'getOffer': Use its offerId directly.
4. 'getLuggage' returns all flight segments' baggage data, each identified by a unique productCode.
5. In the Order step, use the productCode to add specific baggage products to the ticket order.

{% endhint %}

### Endpoint {% debug uid="getLuggage_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/getLuggage.do](https://sandbox.atriptech.com/getLuggage.do)

## Request

{% tabs %}
{% tab title="Schema" %}

### **offerId**  
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the offer. offerId returned by getOffer and sessionId returned by verify can also be used. Must be a valid UUID.  
- **Default:** None  
- **Example:** `"1499249e-4149-483b-824c-a4ff8e150a40"`

### **maxResponseTime**  
- **Type:** Integer  
- **Required:** No  
- **Description:** Maximum response time for the request in milliseconds. The API will return an accurate quotation within this time. If this time is exceeded, the system will directly return a rule - based quotation. 
- **Default:** 15000  
- **Example:** `6000`

{% endtab %}

{% tab title="Samples" %}
```json
{ 

    "offerId": "1499249e-4149-483b-824c-a4ff8e150a40",  

    "maxResponseTime": 6000 

} 
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}



### **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status code of the response. **0** = success, other values = error or special condition.   
- **Default:** **0**  
- **Example:** **212**

### **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Message describing the result. Format: Free text or **null**.  
- **Default:** **"Success"**  
- **Example:** **"Success"**

### **data.offerId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the fare offer. Format: UUID  
- **Default:** None  
- **Example:** **"85540632-ef14-4cb2-900e-453ef0a19477"**

### **data.outboundSegments[]**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of outbound flight segments. Must contain at least one segment object.  
- **Default:** **[]**  
- **Example:** **[ { ... } ]**

#### **segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Position of the segment in the itinerary (1-based index).  
- **Default:** **1**  
- **Example:** **1**

#### **carrier**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA airline code. Must be a valid 2-character airline code.    
- **Default:** None  
- **Example:** **"W6"**

#### **flightNumber**
- **Type:** String  
- **Required:** Yes  
- **Description:** Airline's flight number. Alphanumeric, includes airline code prefix.  
- **Default:** None  
- **Example:** **"W65083"**

#### **depAirport** / **arrAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA airport code for departure/arrival. Must be valid 3-letter codes.    
- **Default:** None  
- **Example:** **"TIA"** / **"GOA"**

#### **depTime** / **arrTime**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure/arrival time in **yyyyMMddHHmm** format.  
- **Default:** None  
- **Example:** **"202503051115"** / **"202503051320"**

#### **stopCities**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Stopover cities (comma-separated IATA codes).  
- **Default:** **null**  
- **Example:** **null**

#### **duration**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Flight duration in minutes.  
- **Default:** None  
- **Example:** **125**

#### **codeShare**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Whether the flight is operated under a codeshare agreement. 
  Valid values:
  - true: codeshare flight
  - false: not a codeshare flight
- **Default:** **false**  
- **Example:** **false**

#### **cabin**
- **Type:** String  
- **Required:** No  
- **Description:** Cabin code as per airline’s internal designation.  
- **Default:** **""**  
- **Example:** **"R"**

#### **cabinClass**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Cabin class level. 
  Valid values:
  - **1** = Economy  
  - **2** = Premium Economy 
  - **3** = Business  
  - **4** = First  
- **Default:** **1**  
- **Example:** **1**

#### **seatCount**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of seats available.  
- **Default:** **0**  
- **Example:** **6**

#### **aircraftCode**
- **Type:** String  
- **Required:** No  
- **Description:** Aircraft type code (e.g., "320" for A320).  
- **Default:** **""**  
- **Example:** **"32Q"**

#### **depTerminal** / **arrTerminal**
- **Type:** String  
- **Required:** No  
- **Description:** Departure / arrival terminal code.  
- **Default:** **""**  
- **Example:** **"T1"**

#### **operatingCarrier**
- **Type:** String  
- **Required:** No  
- **Description:** Actual operating airline’s IATA code. Must be a valid 2-letter IATA code.  
- **Default:** **""**  
- **Example:** **"W6"**

#### **operatingFlightnumber**
- **Type:** String  
- **Required:** No  
- **Description:** Operating airline’s flight number.  
- **Default:** **""**  
- **Example:** **""**

#### **fareFamily**
- **Type:** String  
- **Required:** Yes  
- **Description:** Fare family name.  
- **Default:** None  
- **Example:** **"ECOFLEX"**

### **data.inboundSegments**
- **Type:** Array or Null  
- **Required:** No  
- **Description:** List of inbound segments (for round trips).  
- **Default:** **null**  
- **Example:** **null**

### **data.ancillaryProductElements[]**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of baggage and ancillary options.  
- **Constraints:** Must contain at least one object if ancillary products are offered.  
- **Default:** **[]**  
- **Example:** **[ { ... } ]**

#### **segmentIndex**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** The segment index this product applies to. Must match a segment from itinerary.  
- **Default:** **1**  
- **Example:** **1**

#### **productCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique code identifying the ancillary product. It would be used in the order request. 
- **Default:** None  
- **Example:** "SCI_BAG_1PC_18KG"  

#### **price** 
- **Type:** Number  
- **Required:** Yes  
- **Description:** Price of the ancillary product.  
- **Default:** None  
- **Example:** 68.00  

#### **currency** 
- **Type:** String  
- **Required:** Yes  
- **Description:** ISO 4217 currency code. Must be a valid currency code.   
- **Default:** **"USD"**  
- **Example:** **"USD"**

#### **vendorPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Vendor price of the ancillary product.  
- **Default:** None  
- **Example:** 68.00  

#### **vendorCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the vendor prices the ancillary product. Must be a valid ISO 4217 currency code.    
- **Default:** "USD"  
- **Example:** "USD"  

#### **displayPrice**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Price displayed to the user for the ancillary product in display currency.  
- **Default:** None  
- **Example:** 68.00  

#### **displayCurrency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency in which the display price is shown. Must be a valid ISO 4217 currency code.    
- **Default:** "USD"  
- **Example:** "USD"  

#### **maxQty**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Maximum quantity of the ancillary product that can be purchased.  
- **Default:** 1  
- **Example:** 1  

#### **minQty** 
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Minimum quantity of the ancillary product that must be purchased.  
- **Default:** 1  
- **Example:** 1  

#### **categoryCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Category classification of the ancillary product.  
- **Default:** None  
- **Example:** "StandardCheckInBaggage"  

#### **ancillaryCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code uniquely identifying the ancillary product.  
- **Default:** None  
- **Example:** "SCI_BAG_1PC_18KG"  

### **auxBaggageElement**

#### **piece**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of baggage pieces allowed.  
- **Default:** 1  
- **Example:** 1  

#### **weight**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Weight limit in kilograms.  
 Valid values:
  0：No Limitation about piece;
  higher than 0：Maximum pieces
- **Default:** 18  
- **Example:** 18  

#### **isAllWeight**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates whether the total weight is distributed among all pieces.
  Valid values:
  true: Weight is for all the pieces of baggage.
  false: Weight is only for a single piece of baggage.
- **Default:** true  
- **Example:** true  

#### **size**
- **Type:** String  
- **Required:** No  
- **Description:** Dimensions of the baggage, if applicable.  
- **Default:** ""  
- **Example:** ""  

{% endtab %}

{% tab title="Samples" %}
```json
{ 
  "status": 212, 
  "msg": "Success", 
  "data": { 
    "offerId": "85540632-ef14-4cb2-900e-453ef0a19477", 
    "outboundSegments": [ 
      { 
        "segmentIndex": 1, 
        "carrier": "W6", 
        "flightNumber": "W65083", 
        "depAirport": "TIA", 
        "depTime": "202503051115", 
        "arrAirport": "GOA", 
        "arrTime": "202503051320", 
        "stopCities": "IST,ATH", 
        "duration": 125, 
        "cabin": "R", 
        "cabinClass": 1, 
        "seatCount": 6, 
        "aircraftCode": "B737", 
        "depTerminal": "T1", 
        "arrTerminal": "T2", 
        "operatingCarrier": "W6", 
        "operatingFlightnumber": "W6101", 
        "fareFamily": "ECOFLEX" 
      } 
    ], 
    "inboundSegments": null, 
    "ancillaryProductElements": [ 
      { 
        "segmentIndex": 1, 
        "productCode": "SCI_BAG_1PC_10KG", 
        "price": 15.7, 
        "currency": "USD", 
        "vendorPrice": 0, 
        "vendorCurrency": "EUR", 
        "auxBaggageElement": { 
          "piece": 1, 
          "weight": 20, 
          "isAllWeight": true, 
          "size": "23x35x55cm" 
        }, 
        "minQty": 1, 
        "maxQty": 1, 
        "categoryCode": "StandardCheckInBaggage", 
        "ancillaryCode": "SCI_BAG_1PC_10KG", 
        "displayPrice": 15.7, 
        "displayCurrency": "USD" 
      } 
    ] 
  } 
} 
```
{% endtab %}
{% endtabs %}  
