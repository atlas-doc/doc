# Get Offer

### Dependency

No preceding function needs to be called before Get Offer.  

### Endpoint {% debug uid="verify_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/getOffers.do](https://sandbox.atriptech.com/getOffers.do)

{% hint style="info" %}

* Compared to the Verify API, the Getoffer API does not rely on Search results and improves the success rate of price verify. Since using our GetOffer real-time search increases the L2B Ratio of our requesting carrier API, not all carriers support price verification via the Getoffer.
* Please contact your Key Account Manager if you want to use the getOffer API. Atlas will review your workflow and if deemed aplicable, Atlas will provide further information and support you with the implementation of this API.

{% endhint %}

### Request

{% tabs %}
{% tab title="Schema" %}
| **Parameter**                          | **Type**   | **Required/Optional** | **Description**                        | **Constraints**      | **Default** | **Example** |
|----------------------------------------|------------|-----------------------|----------------------------------------|----------------------|-------------|-------------|
| **adults**                             | Integer    | Required              | Number of adults                       | N/A                  | 1           | 1           |
| **children**                           | Integer    | Required              | Number of children                     | N/A                  | 0           | 0           |
| **infants**                            | Integer    | Required              | Number of infants                      | N/A                  | 0           | 0           |
| **<span style="color:blue">Outbound Segments</span>** |            |                       |                                        |                      |             |             |
| **outboundSegments**                   | Array      | Required              | List of outbound flight segments       | N/A                  | []          | [{"departureAirport": "LON", "arrivalAirport": "PAR", "carrier": "U2", "flightNumber": "673", "departureDate": "20250301"}] |
| **outboundSegments.departureAirport**  | String     | Required              | IATA three letter code of departure airport which is case sensitive. If the value is illegal, the system will prompt that the airport does not exist.                | 3 Characters              | N/A         | "LON"       |
| **outboundSegments.arrivalAirport**    | String     | Required              | IATA three letter code of departure airport which is case sensitive. If the value is illegal, the system will prompt that the airport does not exist.                   | 3 Characters                  | N/A         | "PAR"       |
| **outboundSegments.carrier**           | String     | Required              | Carrier code                           | N/A                  | N/A         | "U2"        |
| **outboundSegments.flightNumber**      | String     | Required              | Marketing flight number without airline code prefix.                           | N/A                  | N/A         | "673"       |
| **outboundSegments.departureDate**     | String     | Required              | Departure date in YYYYMMDD format. We do not require users to specify departure times, we do not support return segments based on specific departure time as well. Considering that the externally transmitted time may not match the actual flight segment time on the supplier's (airline's) side, this can lead to search results being lost. Therefore, we will return flights with the specified flight number departing on the specified date. | 8 numerics                  | N/A         | "20250301"  |
| **<span style="color:blue">Inbound Segments</span>** |            |                       |                                        |                      |             |             |
| **inboundSegments**                    | Array      | Required              | List of inbound flight segments        | N/A                  | []          | [{"departureAirport": "PAR", "arrivalAirport": "LON", "carrier": "U2", "flightNumber": "674", "departureDate": "20250303"}] |
| **inboundSegments.departureAirport**   | String     | Required              | IATA three letter code of departure airport which is case sensitive. If the value is illegal, the system will prompt that the airport does not exist.                 | 3 Characters        | N/A         | "PAR"       |
| **inboundSegments.arrivalAirport**     | String     | Required              | IATA three letter code of departure airport which is case sensitive. If the value is illegal, the system will prompt that the airport does not exist.                 | 3 Characters                 | N/A         | "LON"       |
| **inboundSegments.carrier**            | String     | Required              | Carrier code                           | N/A                  | N/A         | "U2"        |
| **inboundSegments.flightNumber**       | String     | Required              | Marketing flight number without airline code prefix.          | N/A                  | N/A         | "674"       |
| **inboundSegments.departureDate**      | String     | Required              | Departure date in YYYYMMDD format      | N/A                  | N/A         | "20250303"  |
| **<span style="color:blue">currency</span>** |            |                       |                                        |                      |             |             |
| **currency**                           | String     | Optional              | Currency code (if available)           | N/A                  | null        | null        | 

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

| **Parameter**                              | **Type**        | **Required/Optional** | **Description**                                                | **Constraints**   | **Default** | **Example**                        |
|--------------------------------------------|-----------------|-----------------------|----------------------------------------------------------------|-------------------|-------------|------------------------------------|
| **<span style="color:blue">status</span>**   | Integer         | Required              | Status of the response                                          | N/A               | 0           | 0                                  |
| **<span style="color:blue">msg</span>**      | String          | Required              | Message related to the status                                    | N/A               | "string"    | "string"                           |
| **<span style="color:blue">data</span>**     | Array of objects| Required              | List of offers and related data                                  | N/A               | []          | [ ... ]                            |
| **<span style="color:blue">offer</span>**    | Object          | Required              | Offer details                                                     | N/A               | {}          | { ... }                            |
| **offer.offerID**                           | String          | Required              | Unique identifier for the offer                                  | N/A               | N/A         | "o_b07c7d690aea44889eca1f22ad90841c_1" |
| **<span style="color:blue">Fares</span>**    |           |               |                                                      |               |           |  
| **offer.paxFares**                          | Array of objects| Required              | Passenger fare details                                           | N/A               | []          | [ { ... } ]                        |
| **offer.paxFares.paxType**                  | String          | Required              | Passenger type (e.g., ADT)                                       | N/A               | N/A         | "ADT"                              |
| **offer.paxFares.price**                    | Object          | Required              | Price information                                                | N/A               | {}          | { ... }                            |
| **offer.paxFares.price.baseAmount**         | Integer         | Required              | Base amount of the fare                                          | N/A               | 0           | 100                                |
| **offer.paxFares.price.taxes**              | Integer         | Required              | Taxes on the fare                                                | N/A               | 0           | 0                                  |
| **offer.paxFares.price.currency**           | String          | Required              | Currency for the fare                                            | N/A               | "USD"       | "USD"                              |
| **<span style="color:blue">Penalties</span>**    |           |               |                                                      |               |           | 
| **offer.penalties**                         | Array of objects| Required              | Penalty details for the offer                                    | N/A               | []          | [ { ... } ]                        |
| **offer.penalties.journeyRefIDs**           | Array of Strings| Required              | Journey reference IDs                                            | N/A               | []          | ["string"]                         |
| **offer.penalties.amount**                  | Integer         | Required              | Penalty amount                                                   | N/A               | 0           | 0                                  |
| **offer.penalties.currency**                | String          | Required              | Currency for the penalty                                         | N/A               | "USD"       | "USD"                              |
| **offer.penalties.rule**                    | Object          | Required              | Rules related to the penalty                                     | N/A               | {}          | { ... }                            |
| **offer.penalties.rule.type**               | String          | Required              | Type of rule (e.g., Refund)                                      | N/A               | "Refund"    | "Refund"                           |
| **offer.penalties.rule.paxTypes**           | Array of Strings| Required              | Passenger types for the rule                                     | N/A               | []          | ["ADT"]                            |
| **offer.penalties.rule.levelType**          | String          | Required              | Level type for the penalty                                       | N/A               | "Full"      | "Full"                             |
| **offer.penalties.rule.effectiveMinutes**   | Integer         | Required              | Effective time for the penalty                                  | N/A               | 0           | 0                                  |
| **offer.penalties.rule.expirationMinutes**  | Integer         | Required              | Expiration time for the penalty                                 | N/A               | 0           | 0                                  |
| **offer.penalties.rule.fixedAmount**       | Integer         | Required              | Fixed amount for the penalty                                     | N/A               | 0           | 0                                  |
| **offer.penalties.rule.airlineFee**         | Integer         | Required              | Airline fee for the penalty                                      | N/A               | 0           | 0                                  |
| **offer.penalties.rule.currency**          | String          | Required              | Currency for the penalty                                         | N/A               | "USD"       | "USD"                              |
| **offer.penalties.rule.percent**           | Float           | Required              | Percentage for the penalty                                       | N/A               | 0.2         | 0.2                                |
| **offer.penalties.rule.percentBase**       | String          | Required              | Base for the percentage (e.g., fare+tax)                         | N/A               | "fare+tax"  | "fare+tax"                         |
| **<span style="color:blue">Services</span>**    |           |               |                                                      |               |           | 
| **offer.services**                          | Array of objects| Required              | Service details for the offer                                    | N/A               | []          | [ { ... } ]                        |
| **offer.services.serviceID**                | String          | Required              | Service identifier                                                | N/A               | N/A         | "string"                           |
| **offer.services.segmentRefIDs**           | Array of Strings| Required              | Segment reference IDs for the service                             | N/A               | []          | ["string"]                         |
| **offer.services.type**                    | String          | Required              | Type of service (e.g., Baggage)                                   | N/A               | "Baggage"   | "Baggage"                          |
| **offer.services.level**                   | String          | Required              | Level of service (e.g., Free)                                    | N/A               | "Free"      | "Free"                              |
| **offer.services.paxTypes**                 | Array of Strings| Required              | Passenger types applicable for the service                        | N/A               | []          | ["ADT"]                            |
| **offer.services.metadata**                | Object          | Required              | Metadata related to the service                                   | N/A               | {}          | { ... }                            |
| **offer.services.metadata.type**           | String          | Required              | Type of metadata (e.g., StandardCheckInBaggage)                   | N/A               | "StandardCheckInBaggage" | "StandardCheckInBaggage" |
| **offer.services.metadata.maximumWeight**  | Integer         | Required              | Maximum weight allowed                                             | N/A               | 20          | 20                                 |
| **offer.services.metadata.maximumPiece**   | Integer         | Required              | Maximum pieces allowed                                            | N/A               | 1           | 1                                  |
| **offer.services.metadata.maximumDimension**| String          | Required              | Maximum dimension allowed (L+W+H<=158cm)                          | N/A               | "L+W+H<=158cm" | "L+W+H<=158cm"                  |
| **<span style="color:blue">Outbound Journey</span>**    |           |               |                                                      |               |           | 
| **offer.outboundJourney**                  | Object          | Required              | Outbound journey details                                           | N/A               | {}          | { ... }                            |
| **offer.outboundJourney.journeyID**        | String          | Required              | Unique identifier for the outbound journey                        | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments**         | Array of objects| Required              | List of segments in the outbound journey                          | N/A               | []          | [ { ... } ]                        |
| **offer.outboundJourney.segments.segmentID**| String          | Required              | Segment identifier for the outbound journey                       | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments.carrier** | String          | Required              | Carrier for the outbound journey                                  | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments.flightNumber** | String      | Required              | Flight number for the outbound journey                            | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments.operatingCarrier** | String   | Required              | Operating carrier for the outbound journey                        | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments.operatingFlightNumber**| String | Required              | Operating flight number for the outbound journey                  | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments.duration**| Integer         | Required              | Duration of the segment                                           | N/A               | 0           | 0                                  |
| **offer.outboundJourney.segments.legs**    | Array of objects| Required              | List of legs in the segment                                        | N/A               | []          | [ { ... } ]                        |
| **offer.outboundJourney.segments.legs.departureAirport**   | String | Required            | Departure airport code for the segment                           | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments.legs.departureTime**      | String | Required            | Departure time for the segment (YYYYMMDDHHMM)                    | N/A               | N/A         | "202503011100"                     |
| **offer.outboundJourney.segments.legs.arrivalAirport**     | String | Required            | Arrival airport code for the segment                             | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments.legs.arrivalTime**        | String | Required            | Arrival time for the segment (YYYYMMDDHHMM)                      | N/A               | N/A         | "string"                           |
| **offer.outboundJourney.segments.legs.aircraftType**       | String | Required            | Aircraft type for the segment                                     | N/A               | N/A         | "string"                           |
| **<span style="color:blue">Inbound Journey</span>**    |           |               |                                                      |               |           | 
| **offer.inboundJourney**                    | Object          | Required              | Inbound journey details                                            | N/A               | {}          | { ... }                            |
| **offer.inboundJourney.journeyID**          | String          | Required              | Unique identifier for the inbound journey                        | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments**           | Array of objects| Required              | List of segments in the inbound journey                          | N/A               | []          | [ { ... } ]                        |
| **offer.inboundJourney.segments.segmentID**| String          | Required              | Segment identifier for the inbound journey                       | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments.carrier**  | String          | Required              | Carrier for the inbound journey                                   | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments.flightNumber**| String       | Required              | Flight number for the inbound journey                             | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments.operatingCarrier**| String  | Required              | Operating carrier for the inbound journey                         | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments.operatingFlightNumber** | String | Required           | Operating flight number for the inbound journey                  | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments.duration** | Integer         | Required              | Duration of the segment                                           | N/A               | 0           | 0                                  |
| **offer.inboundJourney.segments.legs**     | Array of objects| Required              | List of legs in the segment                                        | N/A               | []          | [ { ... } ]                        |
| **offer.inboundJourney.segments.legs.departureAirport**  | String | Required            | Departure airport code for the segment                           | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments.legs.departureTime**     | String | Required            | Departure time for the segment (YYYYMMDDHHMM)                    | N/A               | N/A         | "202503011100"                     |
| **offer.inboundJourney.segments.legs.arrivalAirport**    | String | Required            | Arrival airport code for the segment                             | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments.legs.arrivalTime**       | String | Required            | Arrival time for the segment (YYYYMMDDHHMM)                      | N/A               | N/A         | "string"                           |
| **offer.inboundJourney.segments.legs.aircraftType**      | String | Required            | Aircraft type for the segment                                     | N/A               | N/A         | "string"                           |
| **<span style="color:blue">Airline Terms</span>**    |           |               |                                                      |               |           | 
| **offer.terms**                              | Array of objects| Optional              | Terms related to the offer                                        | N/A               | []          | [ { ... } ]                        |
| **offer.terms.carrier**                       | String          | Required              | Carrier for the terms                                            | N/A               | N/A         | "string"                           |
| **offer.terms.URL**                          | String          | Required              | URL for the terms                                                 | N/A               | N/A         | "string"                           |
| **<span style="color:blue">serviceFee</span>**|           |               |                                              |                |          |                          |
| **serviceFee.amountPerUnit**                 | Integer         | Required              | Amount per unit for the service fee                               | N/A               | 0           | 0                                  |
| **serviceFee.unit**                          | String          | Required              | Unit of service fee (e.g., PER_SEGMENT)                           | N/A               | "PER_SEGMENT" | "PER_SEGMENT"                      |
| **serviceFee.currency**                      | String          | Required              | Currency for the service fee                                      | N/A               | "USD"       | "USD"                              |
| **<span style="color:blue">Booking Requirement</span>**    |           |               |                                                      |               |           | 
| **bookingRequirement** | Object          | Required              | Booking requirement details                                       | N/A               | {}          | { ... }                            |
| **bookingRequirement.passenger.name**       | Object          | Required              | Passenger name details                                            | N/A               | {}          | { ... }                            |
| **bookingRequirement.passenger.name.type**  | String          | Required              | Type of name (e.g., First, Last)                                  | N/A               | "string"    | "string"                           |
| **bookingRequirement.passenger.name.required** | Boolean     | Required              | Whether the name is required                                      | N/A               | true        | true                               |
| **bookingRequirement.passenger.name.maxLength** | Integer    | Required              | Maximum length for the name                                       | N/A               | 50          | 50                                 |
| **bookingRequirement.passenger.passengerType**| Object        | Required              | Passenger type information                                        | N/A               | {}          | { ... }                            |
| **bookingRequirement.passenger.passengerType.type**| String  | Required              | Type of passenger (e.g., Adult, Child)                            | N/A               | "string"    | "string"                           |
| **bookingRequirement.passenger.passengerType.required**| Boolean| Required             | Whether the passenger type is required                            | N/A               | true        | true                               |
| **bookingRequirement.passenger.passengerType.maxLength** | Integer| Required             | Maximum length for the passenger type                             | N/A               | 50          | 50                                 |
| **<span style="color:blue">Payment Options**</span>** |   |           |  |  |  |  |
| **paymentOptions**                          | Array   | Required          | List of available payment methods | N/A | [] | [] |
| **paymentOptions.paymentMethod**            | String  | Required          | Method of payment (e.g., Deposit) | N/A | "Deposit" | "Deposit" |

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
