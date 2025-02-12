# Cache Data Feed

## Product Description

- Our cache file contains data on routes that have changed or been added during the 
generation cycle.  
- The sources of this data include our regular data collection and passive collection triggered by various tasks in our business.

 
## Implementation Steps  

- **Data Package:** Incremental data is provided in the form of multiple data packages (each package is one file).   
- **Data Unit:** Each data unit is defined by the airline, departure-arrival city pair, and departure date. Multiple data units constitute a data package.
  
  An example of a data unit: VJ, 2024-04-23, Shanghai-Singapore  

  Any changes within a data unit, such as flight additions, reductions, or price changes, this data unit will be in the incremental data package.  

- **Contents of Data Unit:** All flights and prices for a certain airline, departure-arrival city pair, and departure date.
  
  An example of the contents under a data unit: 

  Full data for VJ, 2024-04-23, Shanghai-Singapore  

  VJ1902, USD 145  

  VJ1901, USD 145, USD 156  

  VJ1900, USD 145, USD 156, USD 167  

- **Data Time Window:** 1 hour, meaning we currently only provide incremental data from the past hour.
  
- **Each Download:** Contains multiple data packages, all incremental

## Instructions for Use

- Download and store the initial file. 
- Then, download the latest file as per the business needs.  
- The new file will only contain the updated/added routes. 
- Add/update new routes to the existing routes

## New User Preparation

Since we do not provide full data, new users need to continuously acquire our data packages for 12 hours before official use to accumulate their own full data.  

## Daily Use

1. Download the data packages and overwrite the local data—continuously repeat this operation. Each cycle should ideally not exceed 1 hour (since our incremental data time window is 1 hour, if the user's processing time is too long, it may result in the loss of some data).

2. Match data according to the "data unit" and completely replace all flights and prices within the data unit.  

## Airlines 

The airlines allowed in the feed would be configured at Atlas’ end. 

## Endpoint

This request needs to be sent at regular intervals to keep the cached data fresh. 

Please note that this API is only available in the production environment. Please contact your account manager for further information.

## Points to Note

1. The currency in the cache data feed can be provided either as per the transaction currency of the customer or the airline currency. The airline currency is the currency in which we collect the fare and may not be the currency of the country of journey commencement. The customer can convert it to the currency of their choice using their in-house currency conversion table.  
2. If an airline is under “Maintenance” at our end, then the data feed for that airline will not be returned. 
3. The downloaded link is valid for 1 hour.

## FAQs

1. **Can full data be downloaded during initialization?**
    
No, we do not provide full data for initialization. Customers can accumulate their initial data over several days. As the user's time of use increases, the completeness of the data will continuously improve. For specific operations, please refer to the above [Instructions for Use - New User Preparation].  

2. **How to know which flights are sold out?**
   
We include full flight and price data in each "data unit" (a set of "airline, departure-arrival destination, departure-arrival time" combinations), so you just need to cover with the latest data unit. If a flight is sold out, it will not appear in the latest data and thus will not be searchable by customers.  

Example:

Each data unit consists of airline, departure date and city pair.

The first time we return Full data for: VJ, 2024-04-23, Shanghai-Singapore 

VJ1902, USD 145 

VJ1901, USD 145, USD 156 

VJ1900, USD 145, USD 156, USD 167 

If VJ1902 is sold out, then we will return VJ1902 without price following

VJ, 2024-04-23, Shanghai-Singapore 

VJ1902, 

VJ1901, USD 145, USD 156 

VJ1900, USD 145, USD 156, USD 167 

If VJ1902 is cancelled, then we will not return VJ1902 in this data unit

VJ, 2024-04-23, Shanghai-Singapore 

VJ1901, USD 145, USD 156 

VJ1900, USD 145, USD 156, USD 167 


## Request Header

*   **x-atlas-client-id ** <mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

*   **x-atlas-client-secret ** <mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

### Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The Access key (AK) of the customer.
*   **startTimestamp **<mark style="color:blue;">**string (13 numerals)**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Unix Timestamp. When not filled in, defaults to one hour ago.
*   **endTimestamp **<mark style="color:blue;">**string (13 numerals)**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Unix Timestamp. When not filled in, defaults to one hour ago. The time range cannot exceed one hour. 
    
{% endtab %}

{% tab title="Samples" %}

**Request without Timestamp**
```json
{ 
"cid":"xxxxxxxxxxxx" 
} 
```

**Request with both “startTimestamp” and “endTimestamp”**
```json
{ 
    "cid": " xxxxxxxxxxx ", 
    "startTimestamp": 169663158000, 
    "endTimestamp": 169663158000 
} 
```

**Request with only “startTimestamp”**
```json
{ 
    "cid": " xxxxxxxxxxx", 
    "startTimestamp": 1695804045500 
} 
```

**Request with only “endTimestamp”**
```json
{ 
    "cid": " xxxxxxxxxxx", 
    "endTimestamp": 1695804045500 
} 
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **airline **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    The airline code

*   **createTime **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    The time when the cache was refreshed.

    Format: yyyy-MM-dd HH:mm

*   **itineraries **<mark style="color:blue;">**array**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    List of itinerary details.

### "Itineraries" Array

*   **ancillaryList **<mark style="color:blue;">**array**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    List of ancillary services associated with the itinerary.

*   **prices **<mark style="color:blue;">**array**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Price details for the itinerary.

*   **segments **<mark style="color:blue;">**array**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Flight segments in the itinerary.

### "ancillaryList" Array

*   **outputAncillary **<mark style="color:blue;">**array**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    List of ancillary service options offered for each segment.

*   **segmentIndex **<mark style="color:blue;">**integer**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Index of the flight segment in the itinerary.

### "outputAncillary" Array

*   **categoryEntity **<mark style="color:blue;">**array**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Array defining types of ancillary services, like baggage.

*   **currency **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Currency for ancillary pricing (ISO 4217).

*   **fareFamily **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Class or fare category for ancillary services.

### "categoryEntity" Array

*   **categoryCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Code for ancillary category, e.g., baggage type.

*   **categoryDetail **<mark style="color:blue;">**array**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Details of each category, such as piece count and weight.

### "categoryDetail" Array

*   **auxBaggageElement **<mark style="color:blue;">**object**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Object with specific baggage information.

*   **maxQty **<mark style="color:blue;">**integer**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Maximum quantity allowed for this ancillary.

*   **minQty **<mark style="color:blue;">**integer**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Minimum quantity required for this ancillary.

*   **price **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Price of this ancillary service.

### "auxBaggageElement" Object

*   **isAllWeight **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Indicates if the weight applies universally.

*   **piece **<mark style="color:blue;">**integer**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Number of baggage pieces allowed.

*   **size **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Size of baggage if applicable (empty if not).

*   **weight **<mark style="color:blue;">**integer**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Weight limit in kilograms.

### "prices" Array

*   **bookingCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Reservation or fare class code.

*   **currency **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Currency of the price (ISO 4217).

*   **fareFamily **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Fare category for the passenger (e.g., STANDARD).

*   **paxType **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Passenger type (e.g., ADT for adult).

*   **price **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Base price for the itinerary in the specified currency.

*   **seatCount **<mark style="color:blue;">**integer**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Number of seats available at this fare.

*   **tax **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Total tax applied to the base price.

### "segments" Array

*   **airline **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Airline code for the segment.

*   **arrAirport **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Arrival airport IATA code.

*   **arrCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Arrival city name (if available).

*   **arrTerminal **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Arrival terminal (if available).

*   **arrTime **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Scheduled arrival time. Format: yyyyMMddHHmm

*   **codeShare **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Indicates if the flight is a codeshare flight.

*   **direction **<mark style="color:blue;">**integer**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Flight direction (1 for outbound, 2 for return).

*   **dptAirport **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Departure airport IATA code.

*   **dptCity **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Departure city name (if available).

*   **dptTerminal **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Departure terminal (if available).

*   **dptTime **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Scheduled departure time. Format: yyyyMMddHHmm

*   **duration **<mark style="color:blue;">**integer**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Duration of the segment in minutes.

*   **equipment **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Equipment or aircraft type (if available).

*   **flightNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Mandatory**</mark>

    Flight number for the segment.

*   **operatingAirline **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Operating airline code if different from primary airline.

*   **operatingFlightNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Operating flight number if different from main flight number.

*   **stopCities **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Optional**</mark>

    List of stopover cities, if any.

{% endtab %}

{% tab title="Samples" %}
```json
{ 
    "airline": "W4", 
    "createTime": "2024-10-29 12:54:00", 
    "itineraries": [ 
        { 
            "ancillaryList": [ 
                { 
                    "outputAncillary": [ 
                        { 
                            "categoryEntity": [ 
                                { 
                                    "categoryCode": "StandardCheckInBaggage", 
                                    "categoryDetail": [ 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 5, 
                                                "weight": 160 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 342.30 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 3, 
                                                "weight": 78 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 199.44 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 1, 
                                                "weight": 32 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 64.94 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 4, 
                                                "weight": 80 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 242.11 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 5, 
                                                "weight": 100 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 305.19 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 2, 
                                                "weight": 40 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 118.74 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 3, 
                                                "weight": 96 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 202.23 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 4, 
                                                "weight": 104 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 268.09 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 3, 
                                                "weight": 60 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 179.96 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 6, 
                                                "weight": 120 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 369.20 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 2, 
                                                "weight": 52 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 131.73 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 2, 
                                                "weight": 64 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 133.58 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 6, 
                                                "weight": 192 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 413.73 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 6, 
                                                "weight": 156 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 408.16 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 1, 
                                                "weight": 10 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 44.53 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 5, 
                                                "weight": 130 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 337.66 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 4, 
                                                "weight": 128 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 271.80 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 1, 
                                                "weight": 26 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 64.01 
                                        }, 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 1, 
                                                "weight": 20 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 57.51 
                                        } 
                                    ] 
                                }, 
                                { 
                                    "categoryCode": "CabinBaggageOverheadLocker", 
                                    "categoryDetail": [ 
                                        { 
                                            "auxBaggageElement": { 
                                                "isAllWeight": true, 
                                                "piece": 1, 
                                                "size": "", 
                                                "weight": 10 
                                            }, 
                                            "maxQty": 1, 
                                            "minQty": 1, 
                                            "price": 34.32 
                                        } 
                                    ] 
                                } 
                            ], 
                            "currency": "EUR", 
                            "fareFamily": "Basic" 
                        } 
                    ], 
                    "segmentIndex": 1 
                } 
            ], 
            "prices": [ 
                { 
                    "bookingCode": "", 
                    "currency": "EUR", 
                    "fareFamily": "Basic", 
                    "paxType": "ADT", 
                    "price": 49.90, 
                    "seatCount": 2, 
                    "tax": 9.46 
                }, 
                { 
                    "bookingCode": "", 
                    "currency": "EUR", 
                    "fareFamily": "Plus", 
                    "paxType": "ADT", 
                    "price": 227.91, 
                    "seatCount": 2, 
                    "tax": 9.46 
                } 
            ], 
            "segments": [ 
                { 
                    "airline": "W4", 
                    "arrAirport": "FCO", 
                    "arrCity": "", 
                    "arrTerminal": "", 
                    "arrTime": "202411261345", 
                    "codeShare": false, 
                    "direction": 1, 
                    "dptAirport": "SPX", 
                    "dptCity": "", 
                    "dptTerminal": "", 
                    "dptTime": "202411261100", 
                    "duration": 225, 
                    "equipment": "", 
                    "flightNo": "W46070", 
                    "operatingAirline": "W4", 
                    "operatingFlightNo": "", 
                    "stopCities": "" 
                } 
            ] 
        } 
    ] 
} 
```
{% endtab %}
{% endtabs %}

## Verification

The next step is to go to the verification process. 

To verify the selected fare, the below fields are mandatory for the verification request: 

- cid
- tripType
- adultNumber
- fromCity
- toCity
- fromDate
- fromFlightNumbers

The above fields (plus any other required info) should be transferred from the cache data feed to the verification request. 

### Without Fare Family

If a verification request is sent without populating the “fromFareFamily” and/or “retFareFamily”, then the lowest fare will be returned in the verification response. 

### Request

```json
{
  "cid": "xxxxxxxxxx",
  "tripType": "2",
  "adultNum": 1,
  "childNum": 0,
  "infantNum": 0,
  "fromCity": "DUR",
  "toCity": "HLA",
  "fromDate": "20240116",
  "fromFlightNumbers": [
    "FA321"
  ]
 }
```

### Response

```json
{ 
    "sessionId": "8e6c45e9-4d1e-4dab-8239-7369496a0a45", 
    "maxSeats": 3, 
    "routing": { 
        "fid": "opnnUevXmtqm0xUi5IZ824BcA1bxPJD65Z5VxQ9HDTfDIz9r9X16NQ..", 
        "routingIdentifier": "ONeXHNEi/HPTSlnSN4jJXUeO9d1gEcWIZ21qjY0rM3DzJTpBwuew/dCX3M+vzHUQe0c7X8Gfe8PpEn1g8TrdFXXefkPy/0jkTPNS6jr3WPEoPlS2SFQmv0eNcFNfnFY2UK68k23tEj0VaSxO8judiM8yjxqAnCGo6Elx+F55E/WQZrllnlD5UErCAlPljHvo0Jfcz6/MdRB7RztfwZ97w+kSfWDxOt0VyMIgXvK+XaXtSsRDkIniywK5XD/RVMe1PS97mp9Zk3KhKrewARjdvk5Mh4//4/H8cUXHz3HFvJoDgjdSbhOZcV/BpdLw/m5Kk8UAuPV6bKI4Gk+j5zSNW9+JHhhjzxyG", 
        "supportCreditTransPayment": "0", 
        "currency": "EUR", 
        "adultPrice": 29.47, 
        "adultTax": 10.78, 
        "childPrice": 29.47, 
        "childTax": 10.78, 
        "infantPrice": 0, 
        "infantTax": 0, 
        "infantAllowed": false, 
        "transactionFeePerPax": 0, 
        "transactionFee": 0, 
        "transactionFeeMode": "PER_PAX", 
        "nationalityType": 0, 
        "nationality": "", 
        "suitAge": "", 
        "PaxType": "ADT", 
        "fromSegments": [ 
            { 
                "segmentIndex": 1, 
                "carrier": "FA", 
                "flightNumber": "FA321", 
                "depAirport": "DUR", 
                "depTime": "202401161440", 
                "arrAirport": "HLA", 
                "arrTime": "202401161555", 
                "stopCities": "", 
                "duration": 75, 
                "codeShare": false, 
                "cabin": "", 
                "cabinClass": 1, 
                "seatCount": 3, 
                "aircraftCode": "738", 
                "depTerminal": "", 
                "arrTerminal": "", 
                "operatingCarrier": "", 
                "operatingFlightnumber": "", 
                "fareFamily": "TA" 
            }
```

### With the Fare Family (in development) – Do not integrate 

### Request

```json
{
  "cid": "xxxxxxxxxx",
  "tripType": "2",
  "adultNum": 1,
  "childNum": 0,
  "infantNum": 0,
  "fromCity": "DUR",
  "toCity": "HLA",
  "fromDate": "20240116",
  "fromFlightNumbers": [
    "FA321"
  ]
"fromFareFamily": ["Corporatefareinclbag"]
 }
```

### Response

```json
{
  "sessionId": "9f0e075e-026e-4d78-aec8-bbb8def18905",
  "maxSeats": 3,
  "routing": {
    "fid": "j7XI48P6jqYMMfe5vgZ64YBcA1bxPJD65Z5VxQ9HDTfDIz9r9X16NQ..",
    "routingIdentifier": "ONeXHNEi/HPTSlnSN4jJXUeO9d1gEcWIZ21qjY0rM3CuPQlhUc1mShGfhUBgGBxBI5sVCjw2YH6HgkyZqgoSQ6WTeNIepR7FONeXHNEi/HPTSlnSN4jJXUeO9d1gEcWI0Lu31Yg1BwYm8UZGHw6S9sWQhNtgvPDXeR/hF0KHBYsJkBxDOd4VbaWaD34xx6v+XViUyaE2M0LVyoqJtBIUv9eYfAVNStifDKKBkbBfMxweUN+9ZToJhR4/KNv7cB1DSvYyEMKssV20P0RMEE+tT/VnTb94Rrm6YAybmSX83Upz7uU9w6P1CX5X2t6uVJP4kkcdkIUqCRrtA8HlpTi2lKNoAKyalUdHkwvLcASDZmMGPe55AFeRnVVUACQGnBqN",
    "supportCreditTransPayment": "0",
    "currency": "EUR",
    "adultPrice": 38.34,
    "adultTax": 12.11,
    "childPrice": 38.34,
    "childTax": 12.11,
    "infantPrice": 0,
    "infantTax": 0,
    "infantAllowed": false,
    "transactionFeePerPax": 0,
    "transactionFee": 0,
    "transactionFeeMode": "PER_PAX",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "segmentIndex": 1,
        "carrier": "FA",
        "flightNumber": "FA321",
        "depAirport": "DUR",
        "depTime": "202401161440",
        "arrAirport": "HLA",
        "arrTime": "202401161555",
        "stopCities": "",
        "duration": 75,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 3,
        "aircraftCode": "738",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "Corporate fare incl bag"
      }
    ]
  }
}
```

The rest of the process is the standard workflow as mentioned below: 

Book -> Pay -> Retrieve PNR 
