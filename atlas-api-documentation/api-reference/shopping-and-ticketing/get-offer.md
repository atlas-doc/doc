# Get Offer

### Dependency

No preceding function needs to be called before Get Offer.  

### Endpoint {% debug uid="getoffers_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/getOffers.do](https://sandbox.atriptech.com/getOffers.do)

{% hint style="info" %}

* Compared to the Verify API, the Getoffer API does not rely on Search results and improves the success rate of price verify. Since using our GetOffer real-time search increases the L2B Ratio of our requesting carrier API, not all carriers support price verification via the Getoffer.
* Please contact your Key Account Manager if you want to use the getOffer API. Atlas will review your workflow and if deemed aplicable, Atlas will provide further information and support you with the implementation of this API.

{% endhint %}

### Request

{% tabs %}
{% tab title="Schema" %}

## adults
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of adult passengers.  
- **Constraints:** Must be 1 or more.  
- **Default:** None  
- **Example:** `1`  

## children
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of child passengers.  
- **Constraints:** Must be 0 or more.  
- **Default:** `0`  
- **Example:** `0`  

## infants
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of infant passengers.  
- **Constraints:** Must be 0 or more.  
- **Default:** `0`  
- **Example:** `0`  

## outboundSegments
- **Description:** The segments will be arranged in the order of the flights.  

### outboundSegments[].departureAirport
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code of the departure airport.  
- **Constraints:** 3-letter airport code.  
- **Default:** None  
- **Example:** `"LON"`  

### outboundSegments[].arrivalAirport
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code of the arrival airport.  
- **Constraints:** 3-letter airport code.  
- **Default:** None  
- **Example:** `"PAR"`  

### outboundSegments[].carrier
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA two letter code of marketing carrier.
- **Constraints:** 2-letter airline code.  
- **Default:** None  
- **Example:** `"U2"`  

### outboundSegments[].flightNumber
- **Type:** String  
- **Required:** Yes  
- **Description:** Marketing flight number without airline code prefix. 
- **Constraints:** Numeric flight number.  
- **Default:** None  
- **Example:** `"673"`  

### outboundSegments[].departureDate
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure date of the flight. We do not require users to specify departure times. We do not support return segments based on specific departure time as well. Considering that the externally transmitted time may not match the actual flight segment time on the supplier's (airline's) side, this can lead to search results being lost. Therefore, we will return flights with the specified flight number departing on the specified date. 
- **Constraints:** Format `YYYYMMDD`.  
- **Default:** None  
- **Example:** `"20250301"`  

## inboundSegments
### inboundSegments[].departureAirport
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code of the departure airport.  
- **Constraints:** 3-letter airport code.  
- **Default:** None  
- **Example:** `"PAR"`  

### inboundSegments[].arrivalAirport
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code of the arrival airport.  
- **Constraints:** 3-letter airport code.  
- **Default:** None  
- **Example:** `"LON"`  

### inboundSegments[].carrier
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA two letter code of marketing carrier.
- **Constraints:** 2-letter airline code.  
- **Default:** None  
- **Example:** `"U2"`  

### inboundSegments[].flightNumber
- **Type:** String  
- **Required:** Yes  
- **Description:** Marketing flight number without airline code prefix. 
- **Constraints:** Numeric flight number.  
- **Default:** None  
- **Example:** `"674"`  

### inboundSegments[].departureDate
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure date of the flight. We do not require users to specify departure times. We do not support return segments based on specific departure time as well. Considering that the externally transmitted time may not match the actual flight segment time on the supplier's (airline's) side, this can lead to search results being lost. Therefore, we will return flights with the specified flight number departing on the specified date. 
- **Constraints:** Format `YYYYMMDD`.  
- **Default:** None  
- **Example:** `"20250303"`  

## currency
- **Type:** String or Null  
- **Required:** No  
- **Description:** Preferred currency for pricing.  
- **Constraints:** 3-letter currency code or null.  
- **Default:** `null`  
- **Example:** `USD`  

{% endtab %}

{% tab title="Samples" %}
```
{
  "adults": 1,
  "children": 0,
  "infants": 0,
  "outboundSegments": [
    {
      "departureAirport": "LON",
      "arrivalAirport": "PAR",
      "carrier": "U2",
      "flightNumber": "673",
      "departureDate": "20250301"
    }
  ],
  "inboundSegments": [
    {
      "departureAirport": "PAR",
      "arrivalAirport": "LON",
      "carrier": "U2",
      "flightNumber": "674",
      "departureDate": "20250303"
    }
  ],
  "currency": null
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}


### `status`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status code of the response. The identifier that determines whether the interface has successfully responded, and only when it is 0, it indicates success. Other situations represent different error scenarios, please refer to the error codes listed in ATRIP for details. 
- **Constraints:** Numeric status code (e.g., 0 for success).  
- **Default:** `0`  
- **Example:** `0`

---

### `msg`
- **Type:** String  
- **Required:** Yes  
- **Description:** Message associated with the status. As an additional description of the response results. Especially when the interface reports an error (status !=0), it is usually a human readable error message.  
DO NOT use this field in any programming scenario, such as determining whether the interface responds successfully based on this field. You should always only determine the success of the response based on whether the status is 0.  
- **Constraints:** None  
- **Default:** `"string"`  
- **Example:** `"string"`

---

### `data`
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of offer details.  
- **Constraints:** Array containing objects of offer details.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {
      "offer": { ... },
      "serviceFee": { ... },
      "bookingRequirement": { ... },
      "paymentOptions": [ ... ]
    }
  ]
  ```

---

### `data.offer`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Offer details including ID, fares, penalties, and services.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "offerID": "o_b07c7d690aea44889eca1f22ad90841c_1",
    "paxFares": [ ... ],
    "penalties": [ ... ],
    "services": [ ... ],
    "outboundJourney": { ... },
    "inboundJourney": { ... },
    "terms": [ ... ]
  }
  ```

---

### `data.offer.offerID`
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the offer.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"o_b07c7d690aea44889eca1f22ad90841c_1"`

---

### `data.offer.paxFares`
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of passenger fares associated with the offer. Contains ticket prices and taxes corresponding to each passenger type. If there are no elements for certain passenger types in the list, it means that the ticket is not currently being sold for that passenger type. 
- **Constraints:** Array of passenger fare objects.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {
      "paxType": "ADT",
      "price": { ... }
    }
  ]
  ```

#### `data.offer.paxFares.paxType`
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of passenger (e.g., ADT for adult).  
- **Constraints:** Must be one of the predefined passenger types (ADT,CHD,INF).
- **Default:** None  
- **Example:** `"ADT"`

#### `data.offer.paxFares.price`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Price details for the passenger fare.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "baseAmount": 100,
    "taxes": 0,
    "currency": "USD"
  }
  ```

##### `data.offer.paxFares.price.baseAmount`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Base fare amount. Basic price, excluding taxes. Up to 2 decimal places.  
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `100`

##### `data.offer.paxFares.price.taxes`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Taxes applicable to the fare. Up to 2 decimal places.   
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `0`

##### `data.offer.paxFares.price.currency`
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the fare (e.g., USD) on capitals. 
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** `"USD"`

---

### `data.offer.penalties`
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of penalties associated with the offer, including journey reference IDs and rules.  
- **Constraints:** Array of penalty objects.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {
      "journeyRefIDs": [ ... ],
      "amount": 0,
      "currency": "USD",
      "rule": { ... }
    }
  ]
  ```

#### `data.offer.penalties.journeyRefIDs`
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of journey reference IDs for which the penalty applies. This may include references to multiple journey IDs (such as round trips), indicating that multiple journeys are applicable to the rule.  
- **Constraints:** Array of valid journey reference strings.  
- **Default:** None  
- **Example:** `["string"]`

#### `data.offer.penalties.amount`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Amount of penalty. Up to 2 decimal places.   
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `0`

#### `data.offer.penalties.currency`
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the penalty amount (e.g., USD). This currency may be different from the fare currency, depending on the airline. 
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** `"USD"`

#### `data.offer.penalties.rule`
- **Type:** Object  
- **Required:** Yes  
- **Description:** The rule governing the penalty (e.g., refund type, percentage, etc.).  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "type": "Refund",
    "paxTypes": [ ... ],
    "levelType": "Full",
    "effectiveMinutes": 0,
    "expirationMinutes": 0,
    "fixedAmount": 0,
    "airlineFee": 0,
    "currency": "USD",
    "percent": 0.2,
    "percentBase": "fare+tax"
  }
  ```

##### `data.offer.penalties.rule.type`
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of penalty rule (e.g., Refund).  
- **Constraints:** Refund, Change  
- **Default:** None  
- **Example:** `"Refund"`

##### `data.offer.penalties.rule.paxTypes`
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of passenger types to which the penalty rule applies.  
- **Constraints:** Array of valid passenger types (ADT,CHD,INF).  
- **Default:** None  
- **Example:** `["ADT"]`

##### `data.offer.penalties.rule.levelType`
- **Type:** String  
- **Required:** Yes  
- **Description:** The level of the penalty (e.g., Full).  
Full: If it is a refund, it means a full refund. If it is a rescheduling, it means free rescheduling. 
Partial: If it is a refund, it means a partial refund. If it is a rescheduling, it means that there will be a fee for rescheduling. 
None: If it is a refund, it means it cannot be refunded. If it is a rescheduling, it means that rescheduling is not possible 
- **Constraints:** Full, Partial, None   
- **Default:** None  
- **Example:** `"Full"`

##### `data.offer.penalties.rule.effectiveMinutes`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** The effective minutes after booking when the penalty applies. It forms a time interval together with expiratorMinutes to indicate the time range within which the rule applies. This value serves as the starting point of the interval, measured in minutes. >= 0 represents the number of minutes before takeoff, <0 represents the number of minutes after takeoff. 
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `0`

##### `data.offer.penalties.rule.expirationMinutes`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** The expiration time in minutes after booking when the penalty expires. It forms a time interval together with expirationMinutes to indicate the time range within which the rule applies. This value serves as the end point of the interval, measured in minutes. >=0 represents the number of minutes before takeoff, <0 represents the number of minutes after takeoff.  
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `0`

##### `data.offer.penalties.rule.fixedAmount`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Fixed amount of penalty, if applicable.  up to 2 decimal places.
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `0`

##### `data.offer.penalties.rule.airlineFee`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** The airline fee associated with the penalty. Fixed deduction of airline handling fees, with a maximum of 2 decimal places retained. 
- **Constraints:** Must be a positive integer (>= 0).  
- **Default:** `0`  
- **Example:** `0`

##### `data.offer.penalties.rule.currency`
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the penalty (e.g., USD). This currency may be different from the fare currency, depending on the	airline.  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** `"USD"`

##### `data.offer.penalties.rule.percent`
- **Type:** Number  
- **Required:** Yes  
- **Description:** Percentage of the penalty, if applicable.  
- **Constraints:** Must be a positive float between 0 and 1.  
- **Default:** `0.2`  
- **Example:** `0.2`

##### `data.offer.penalties.rule.percentBase`
- **Type:** String  
- **Required:** Yes  
- **Description:** The base value for the penalty percentage (e.g., "fare+tax"). 
Fare + Tax: The base for expressing percentages is the total price including tax. 
Fare: The base for expressing percentages is the fare. 
- **Constraints:** Must be a valid string (fare + tax, fare).  
- **Default:** None  
- **Example:** `"fare+tax"`

### `data.offer.services`
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** Includes various free and chargeable services, including but not limited to baggage, seat selection, meals, etc.   
- **Constraints:** Array of service objects.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {
      "serviceID": "string",
      "segmentRefIDs": [
        "string"
      ],
      "type": "Baggage",
      "level": "Free",
      "paxTypes": [
        "ADT"
      ],
      "metadata": {
        "type": "StandardCheckInBaggage",
        "maximumWeight": 20,
        "maximumPiece": 1,
        "maximumDimension": "L+W+H<=158cm"
      }
    }
  ]
  ```

#### `data.offer.services.serviceID`
- **Type:** String  
- **Required:** Yes  
- **Description:** The unique ID of this service. This ID is unique within the context of the current offer.   
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

#### `data.offer.services.segmentRefIDs`
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of segment reference IDs the service applies to. This is the flight segment ID reference applicable to this service.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `["string"]`

#### `data.offer.services.type`
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of service (e.g., Baggage, Seat Selection, etc.).  
- **Constraints:** Baggage, Seat, Meal   
- **Default:** None  
- **Example:** `"Baggage"`

#### `data.offer.services.level`
- **Type:** String  
- **Required:** Yes  
- **Description:** Service level (e.g., Free, Paid).  
- **Constraints:** Free，Partial，Chargeable  
- **Default:** None  
- **Example:** `"Free"`

#### `data.offer.services.paxTypes`
- **Type:** Array of Strings  
- **Required:** Yes  
- **Description:** List of passenger types applicable to the service.  
- **Constraints:** ADT, CHD, INF  
- **Default:** None  
- **Example:** `["ADT"]`

#### `data.offer.services.metadata`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Additional metadata for the service. This represents different services, such as package weight, quantity, size, and other restrictions. The content of this node may vary depending on the type of service. Users should read the content of the node according to different service types.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "type": "StandardCheckInBaggage",
    "maximumWeight": 20,
    "maximumPiece": 1,
    "maximumDimension": "L+W+H<=158cm"
  }
  ```

##### `data.offer.services.metadata.type`
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of service metadata (e.g., "StandardCheckInBaggage").  
- **Constraints:** StanardCheckInBaggage, CabinBaggageCabinBaggage, OverheadLocker   
- **Default:** None  
- **Example:** `"StandardCheckInBaggage"`

##### `data.offer.services.metadata.maximumWeight`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Maximum weight allowed for the service (e.g., baggage). 0 represents no weight limit.
- **Constraints:** None
- **Default:** `20`  
- **Example:** `20`

##### `data.offer.services.metadata.maximumPiece`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Maximum number of pieces allowed for the service (e.g., baggage). 0 represents no quantity limit  
- **Constraints:** None  
- **Default:** `1`  
- **Example:** `1`

##### `data.offer.services.metadata.maximumDimension`
- **Type:** String  
- **Required:** Yes  
- **Description:** Maximum allowed dimensions (e.g., baggage size). This content is currently not guaranteed to be structured (parsed).
- **Constraints:** None  
- **Default:** `"L+W+H<=158cm"`  
- **Example:** `"L+W+H<=158cm"`

### `data.offer.outboundJourney`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Details of the outbound journey, including journey ID and segments.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "journeyID": "string",
    "segments": [ ... ]
  }
  ```

#### `data.offer.outboundJourney.journeyID`
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the outbound journey.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

#### `data.offer.outboundJourney.segments`
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of flight segments for the outbound journey in the flight order.  
- **Constraints:** Array of segment objects.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {
      "segmentID": "string",
      "carrier": "string",
      "flightNumber": "string",
      "operatingCarrier": "string",
      "operatingFlightNumber": "string",
      "duration": 0,
      "legs": [ ... ],
      "fareFamily": "string",
      "RBD": "string",
      "cabinClass": "Economy",
      "seatsLeft": 0
    }
  ]
  ```

##### `data.offer.outboundJourney.segments.segmentID`
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique identifier for the flight segment.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.carrier`
- **Type:** String  
- **Required:** Yes  
- **Description:** Marketing carrier code for the flight segment (e.g., airline IATA code).  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.flightNumber`
- **Type:** String  
- **Required:** Yes  
- **Description:** Marketing carrier flight number for the outbound journey segment. Do not include airline code prefix.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.operatingCarrier`
- **Type:** String  
- **Required:** Yes  
- **Description:** Operating carrier code for the flight.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.operatingFlightNumber`
- **Type:** String  
- **Required:** Yes  
- **Description:** Operating flight number for the flight. Do not include airline code prefix. 
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.duration`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Duration of the flight segment in minutes.  
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `0`

##### `data.offer.outboundJourney.segments.legs`
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** Details of the flight legs within the segment. The physical flight information that constitutes the flight segment and the stopover information can be obtained from this. The number of elements=1 indicates that there is no stopping point. This will be displayed in flight order.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  [
    {
      "departureAirport": "string",
      "departureTime": "202503011100",
      "departureTerminal": "string",
      "arrivalAirport": "string",
      "arrivalTime": "string",
      "arrivalTerminal": "string",
      "aircraftType": "string"
    }
  ]
  ```

##### `data.offer.outboundJourney.segments.legs.departureAirport`
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code for the departure airport.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.legs.departureTime`
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure time in UTC in the format `YYYYMMDDHHMM`. For flights taking off from transit points, the departure time may not be available. For flights taking off from the starting point, the time will definitely be available.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"202503011100"`

##### `data.offer.outboundJourney.segments.legs.departureTerminal`
- **Type:** String  
- **Required:** Yes  
- **Description:** Terminal at the departure airport.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.legs.arrivalAirport`
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code for the arrival airport.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.legs.arrivalTime`
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival time in UTC in the format `YYYYMMDDHHMM`. For flights taking off from transit points, the departure time may not be available. For flights taking off from the starting point, the time will definitely be available.
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.legs.arrivalTerminal`
- **Type:** String  
- **Required:** Yes  
- **Description:** Terminal at the arrival airport.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.legs.aircraftType`
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of aircraft used for the segment.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.fareFamily`
- **Type:** String  
- **Required:** Yes  
- **Description:** Fare family for the flight segment.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.RBD`
- **Type:** String  
- **Required:** Yes  
- **Description:** Booking code for the flight segment.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.offer.outboundJourney.segments.cabinClass`
- **Type:** String  
- **Required:** Yes  
- **Description:** Class of the cabin for the flight segment (e.g., Economy, Business).  
- **Constraints:** Economy, Business, First   
- **Default:** `"Economy"`  
- **Example:** `"Economy"`

##### `data.offer.outboundJourney.segments.seatsLeft`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Number of seats left in the flight segment.  
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `0`

---

### `data.offer.inboundJourney`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Details of the inbound journey, similar to outbound journey.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "journeyID": "string",
    "segments": [ ... ]
  }
  ```

The structure of `inboundJourney` is similar to `outboundJourney`. The same attributes apply to the segments and legs. For brevity, we will not repeat the exact same fields for inbound journey. 

---

### `data.offer.terms`
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** Terms and conditions of the offer.  
- **Constraints:** Array of term objects.  
- **Default:** None  
- **Example:**  
  ```json
  [
    {
      "carrier": "string",
      "URL": "string"
    }
  ]
  ```

#### `data.offer.terms.carrier`
- **Type:** String  
- **Required:** Yes  
- **Description:** Carrier associated with the terms.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

#### `data.offer.terms.URL`
- **Type:** String  
- **Required:** Yes  
- **Description:** URL link for the terms and conditions.  
- **Constraints:** Must be a valid URL.  
- **Default:** None  
- **Example:** `"string"`

---

### `data.serviceFee`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Service fee for the offer.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "amountPerUnit": 0,
    "unit": "PER_SEGMENT",
    "currency": "USD"
  }
  ```

#### `data.serviceFee.amountPerUnit`
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Amount of service fee per unit (e.g., per segment).  
- **Constraints:** Must be a positive integer.  
- **Default:** `0`  
- **Example:** `0`

#### `data.serviceFee.unit`
- **Type:** String  
- **Required:** Yes  
- **Description:** Unit of the service fee (e.g., "PER_SEGMENT").  
- **Constraints:** PER_SEGMENT, PER_PAX, PER_BOOKING  
- **Default:** `"PER_SEGMENT"`  
- **Example:** `"PER_SEGMENT"`

#### `data.serviceFee.currency`
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency of the service fee (e.g., USD).  
- **Constraints:** Must be a valid ISO 4217 currency code.  
- **Default:** None  
- **Example:** `"USD"`

---

### `data.bookingRequirement`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Booking requirements for the passenger, including details such as name, type, and card information.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "passenger": { ... }
  }
  ```

---

### `data.bookingRequirement.passenger`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Passenger details required for the booking.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "name": { ... },
    "passengerType": { ... },
    "birthday": { ... },
    "gender": { ... },
    "nationality": { ... },
    "cardType": { ... },
    "cardNum": { ... },
    "cardIssuePlace": { ... },
    "cardExpired": { ... }
  }
  ```

#### `data.bookingRequirement.passenger.name`
- **Type:** Object  
- **Required:** Yes  
- **Description:** Passenger name details.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  {
    "type": "string",
    "required": true,
    "description": "string",
    "maxLength": "string"
  }
  ```

##### `data.bookingRequirement.passenger.name.type`
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of passenger name.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"string"`

##### `data.bookingRequirement.passenger.name.required`
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Whether the name is required.  
- **Constraints:** `true` or `false`.  
- **Default:** `true`  
- **Example:** `true`

##### `data.bookingRequirement.passenger.name.description`
- **Type:** String  
- **Required:** Yes  
- **Description:** Description of the name field.  
- **Constraints:** None  
- **Default:** `"string"`  
- **Example:** `"string"`

##### `data.bookingRequirement.passenger.name.maxLength`
- **Type:** String  
- **Required:** Yes  
- **Description:** Maximum length allowed for the name.  
- **Constraints:** None  
- **Default:** `"string"`  
- **Example:** `"string"`

---

The rest of the `passenger` elements (`passengerType`, `birthday`, `gender`, `nationality`, `cardType`, `cardNum`, `cardIssuePlace`, and `cardExpired`) would follow the same structure as `name`, so we will not repeat their attributes here.

---

### `data.paymentOptions`
- **Type:** Array of Objects  
- **Required:** Yes  
- **Description:** List of available payment methods.  
- **Constraints:** None  
- **Default:** None  
- **Example:**  
  ```json
  [
    {
      "paymentMethod": "Deposit"
    }
  ]
  ```

#### `data.paymentOptions.paymentMethod`
- **Type:** String  
- **Required:** Yes  
- **Description:** The method of payment (e.g., "Deposit").  
- **Constraints:** Deposit, VCC_Passthrough, BYOA, MoR   
- **Default:** None  
- **Example:** `"Deposit"`

---

{% endtab %}

{% tab title="Samples" %}
```
{
  "status": 0,
  "msg": "string",
  "data": [
    {
      "offer": {
        "offerID": "o_b07c7d690aea44889eca1f22ad90841c_1",
        "paxFares": [
          {
            "paxType": "ADT",
            "price": {
              "baseAmount": 100,
              "taxes": 0,
              "currency": "USD"
            }
          }
        ],
        "penalties": [
          {
            "journeyRefIDs": [
              "string"
            ],
            "amount": 0,
            "currency": "USD",
            "rule": {
              "type": "Refund",
              "paxTypes": [
                "ADT"
              ],
              "levelType": "Full",
              "effectiveMinutes": 0,
              "expirationMinutes": 0,
              "fixedAmount": 0,
              "airlineFee": 0,
              "currency": "USD",
              "percent": 0.2,
              "percentBase": "fare+tax"
            }
          }
        ],
        "services": [
          {
            "serviceID": "string",
            "segmentRefIDs": [
              "string"
            ],
            "type": "Baggage",
            "level": "Free",
            "paxTypes": [
              "ADT"
            ],
            "metadata": {
              "type": "StandardCheckInBaggage",
              "maximumWeight": 20,
              "maximumPiece": 1,
              "maximumDimension": "L+W+H<=158cm"
            }
          }
        ],
        "outboundJourney": {
          "journeyID": "string",
          "segments": [
            {
              "segmentID": "string",
              "carrier": "string",
              "flightNumber": "string",
              "operatingCarrier": "string",
              "operatingFlightNumber": "string",
              "duration": 0,
              "legs": [
                {
                  "departureAirport": "string",
                  "departureTime": "202503011100",
                  "departureTerminal": "string",
                  "arrivalAirport": "string",
                  "arrivalTime": "string",
                  "arrivalTerminal": "string",
                  "aircraftType": "string"
                }
              ],
              "fareFamily": "string",
              "RBD": "string",
              "cabinClass": "Economy",
              "seatsLeft": 0
            }
          ]
        },
        "inboundJourney": {
          "journeyID": "string",
          "segments": [
            {
              "segmentID": "string",
              "carrier": "string",
              "flightNumber": "string",
              "operatingCarrier": "string",
              "operatingFlightNumber": "string",
              "duration": 0,
              "legs": [
                {
                  "departureAirport": "string",
                  "departureTime": "202503011100",
                  "departureTerminal": "string",
                  "arrivalAirport": "string",
                  "arrivalTime": "string",
                  "arrivalTerminal": "string",
                  "aircraftType": "string"
                }
              ],
              "fareFamily": "string",
              "RBD": "string",
              "cabinClass": "Economy",
              "seatsLeft": 0
            }
          ]
        },
        "terms": [
          {
            "carrier": "string",
            "URL": "string"
          }
        ]
      },
      "serviceFee": {
        "amountPerUnit": 0,
        "unit": "PER_SEGMENT",
        "currency": "USD"
      },
      "bookingRequirement": {
        "passenger": {
          "name": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          },
          "passengerType": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          },
          "birthday": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          },
          "gender": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          },
          "nationality": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          },
          "cardType": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          },
          "cardNum": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          },
          "cardIssuePlace": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          },
          "cardExpired": {
            "type": "string",
            "required": true,
            "description": "string",
            "maxLength": "string"
          }
        }
      },
      "paymentOptions": [
        {
          "paymentMethod": "Deposit"
        }
      ]
    }
  ]
}
```
{% endtab %}
{% endtabs %}
