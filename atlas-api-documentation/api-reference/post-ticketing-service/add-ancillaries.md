# Add Ancillaries

### Dependency

"Offer Ancillary List" function should be called in prior of this call.

### Endpoint {% debug uid="orderAncillary_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/orderAncillary.do](https://sandbox.atriptech.com/orderAncillary.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of client and user.
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It is an order for ticketing.
    
*   **passengers Array<**<mark style="color:blue;">**PassengerElement**</mark>**> **<mark style="color:green;">**Required**</mark>
     
    * <mark style="color:blue;">**PassengerElement**</mark>
      *   **name **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          LastName/FirstName MiddleName.
      *   **ancillaries Array<**[**AncillaryElement**](add-ancillaries.md#undefined)**> **<mark style="color:green;">**Required**</mark>

          Ancillaries selection for the specific passenger
      * [**AncillaryElement**](add-ancillaries.md#undefined)
        *   **segmentIndex **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

            Segment sequence. It starts from 1. If it is round trip, the outbound and inbound sequence would be together.
        *   **productCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

            Unique identifier for the ancillary product. Used for the order ancillary function.
            
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXXXXXX",
    "ticketOrderNo": "APXOS20230629164129749",
    "ancillaryCategory": "SEAT",
    "sessionId": "e3593a39-78d4-4e60-a42e-c5c7902455d4",
    "skipSeatVerify": true,
    "passengers": [
        {
            "name": "ZHANG/SAN",
            "passengerType": 0,
            "ancillaries":[ 
                { 
                    "productCode":"AD_SEAT_35F_JT122", 
                    "segmentIndex":1
                },
                { 
                    "productCode":"AD_SEAT_31D_JT123", 
                    "segmentIndex":2
                }
            ]
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>

    0: success

    2: System error

    6: Price change
*   **msg **<mark style="color:blue;">**string**</mark>

    Error message
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
*   **orderNo **<mark style="color:blue;">**string**</mark>

    Order number of the added ancillary.
    
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>

    Order number. It is an order for ticketing.

*   **totalPrice **<mark style="color:blue;">**decimal**</mark>

    Total fare of this order in the currency Atlas settled with the customer.

*   **totalTransactionFee **<mark style="color:blue;">**decimal**</mark>

    Total technical fees for this order in the currency Atlas settled with the customer.
*   **currency **<mark style="color:blue;">**string**</mark>

    The currency Atlas settled with the customer.
*   **vendorTotalPrice **<mark style="color:blue;">**decimal**</mark>

    Total fare of this order in the vendor's currency. This is the reference for the customer to generate the specific credit card.
*   **vendorCurrency **<mark style="color:blue;">**string**</mark>

    Vendor's currency.
*   **tktLimitTime **<mark style="color:blue;">**string**</mark>

    Payment deadline for this order.
*   **paxTicketInfos Array<**<mark style="color:blue;">**PAXTicketInfo**</mark>**>**

    Ticket information for passengers

    * <mark style="color:blue;">**PAXTicketInfo**</mark>
      *   **name **<mark style="color:blue;">**string**</mark>

          LastName/FirstName MiddleName.
      *   **passengerType **<mark style="color:blue;">**int**</mark>

          0 ADT

          1 CHD
      *   **birthday **<mark style="color:blue;">**string**</mark>

          Birthday, Format: YYYYMMDD
      *   **gender **<mark style="color:blue;">**string**</mark>

          M : Male

          F : Female
      *   **cardNum **<mark style="color:blue;">**string**</mark>

          Passenger id card number
      *   **cardType **<mark style="color:blue;">**string**</mark>

          Passenger id card type：

          PP - Passport

          GA - Hong Kong Macau Pass for China mainland citizens

          TW - Taiwan Pass for China mainland citizens

          TB - China mainland pass for Taiwanese

          HY - International Seaman's Certificate
      *   **cardIssuePlace **<mark style="color:blue;">**string**</mark>

          Card issue country，IATA code of country
      *   **cardExpired **<mark style="color:blue;">**string**</mark>

          Card expire date，Format：YYYYMMDD
      *   **nationality **<mark style="color:blue;">**string**</mark>

          Nationality，IATA code of country
      *   **ticketNos Array<**<mark style="color:blue;">**string**</mark>**>**

          Ticket numbers
      *   **airlinePNRs Array<**<mark style="color:blue;">**string**</mark>**>**

          AirlinePNRs, the array count would be the same as ticketnos count
      *   **ancillaries Array<**<mark style="color:blue;">**AncillaryElement**</mark>**>**

          Ancillaries selection for the specific passenger

          * [**AncillaryElement**](add-ancillaries.md#undefined)
            *   **productCode **<mark style="color:blue;">**string**</mark>

                Ancillary product code;

                Received from routing element in the search/revalidation response.
            *   **segmentIndex **<mark style="color:blue;">**int**</mark>

                Segment sequence

            *   **ancillaryPrice **<mark style="color:blue;">**int**</mark>

                Price for this ancillary.

            *   **offerId **<mark style="color:blue;">**int**</mark>

                unique identifier for this ancillary's offer.

            *   **currency **<mark style="color:blue;">**int**</mark>

                Currency for this ancillary price.

            *   **auxSeatElement Array**

                Seat information.

            *   **`rowNo`  **<mark style="color:blue;">**int**</mark>
     
                The row number of the seat.

            *   **`seatNo`  **<mark style="color:blue;">**string**</mark>
     
                Seat Number
          
            *   **`status`  **<mark style="color:blue;">**boolean**</mark>
     
                true: Available seat.
                
                false: Unavailable seat.

            *   **`seatInfo Array`  **<mark style="color:blue;">**
     
                Seat information description

                Seat position information：

                window

                aisle

                middle

                Required. This can be used to draw seat maps.

                Other information. For example; "exit".

            *   **` passengerType`  **<mark style="color:blue;">**

                Passenger types supported by seats.

# Segment Element Schema

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

\`\`

**`operatingFlightnumber`  **<mark style="color:blue;">**string**</mark>

Operating flight number. It is blank when `codeshare=false`

**`fareFamily`  **<mark style="color:blue;">**string**</mark>

Fare Family as per the information received from the airline.

\`\`
{% endtab %}
{% endtabs %}


                
            
{% endtab %}

{% tab title="Samples" %}
```json
{
    "sessionId": "e3593a39-78d4-4e60-a42e-c5c7902455d4",
    "orderNo": "BISKL20230629164129749",
    "originalOrderNo": null,
    "ticketOrderNo": "APXOS20230629164129749",
    "totalPrice": 2.00,
    "totalTransactionFee": 3.00,
    "currency": "USD",
    "vendorTotalPrice": null,
    "vendorCurrency": null,
    "tktLimitTime": "2023-07-19 17:36:35",
    "pnrCode": "YCGY3Y",
    "includeExtraBaggage": null,
    "paxTicketInfos": [
        {
            "name": "ZHANG/SAN",
            "passengerType": 0,
            "birthday": "19960831",
            "gender": "F",
            "cardNum": "1231",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "2023",
            "nationality": "GB",
            "ticketNos": [],
            "airlinePNRs": [],
            "contactEmails": [
                "BISKL20230629164129749_1@ttjipiao.top"
            ],
            "contactPhones": [
                null
            ],
            "ancillaries": [
                {
                    "productCode": "AD_SEAT_35F_JT122",
                    "segmentIndex": 1,
                    "offerId": null,
                    "ancillaryPrice": 1.00,
                    "currency": "USD",
                    "auxSeatElement": 
                },
                {
                    "productCode": "AD_SEAT_31D_JT123",
                    "segmentIndex": 2,
                    "offerId": null,
                    "ancillaryPrice": 1.00,
                    "currency": "USD",
                    "auxSeatElement": null
                }
            ]
        }
    ],
    "routing": null,
    "status": 0,
    "msg": null
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you want to pay for the add-ancillary order, please call the [pay](broken-reference/) function as same as the ticketing orders.
{% endhint %}
