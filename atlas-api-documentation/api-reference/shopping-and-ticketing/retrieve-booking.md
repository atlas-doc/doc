# Retrieve Booking

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="queryOrderDetails_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/queryOrderDetails.do](https://sandbox.atriptech.com/queryOrderDetails.do)

{% hint style="info" %}
Please refer to the below information for the usage of the queryOrderDetails.do API.

1. All the parameters can be used together, if required.

2. “OrderNo” is “required” if “airlinePNR” and “carrier” cannot be provided upon calling the API. Inversely, “airlinePNR” and “carrier” are “required” if “OrderNo” cannot be provided. All remaining fields in the request are optional.

3. The PNR (Passenger Name Record) for an airline ticket order or a luggage purchase order must be kept consistent, as per airline regulations.

4. The input parameters orderNo, airlinePNR, carrier, and other optional fields will be validated together to ensure they belong to the same order data source. If any of these input parameters do not match with others, the API will return an error.

5. Airline ticket orders and associated post-booking ancillary orders can be retrieved using the following methods: (airline ticket orders + post-booking ancillary orders):
    - orderNo
    - airlinePNR + carrier
    - orderNo + airlinePNR + carrier
    - orderNo + airlinePNR + carrier + other optional parameters

6. In case the parameters of “airlinePNR” and “carrier” cannot identify an unique order (e.g BC - PNR is made up with 4 number), customer needs to enter additional parameters such as "name" for identification. In such scenarios, API will respond with error msg ”Multi-orderNos are identified, please request again with extra parameters added.”

{% endhint %}


## Request

{% tabs %}
{% tab title="Schema" %}
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
*   **airlinePNR **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    The record locator of the airline.
*   **carrier **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    2 character IATA airline code.
*   **isCompletedOrder **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    If not entered with value, API would take it as “false” by default. 

    **true**: Show the full details of main order and post-booking order

    **false**: Only show the details of given order
*   **passengers Array<**<mark style="color:blue;">**PassengerElement**</mark>**> **<mark style="color:orange;">**Optional**</mark>

    Passengers' information.

* #### <mark style="color:blue;">**PassengerElement**</mark>
*   **name **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Name of the passenger. Format: LastName/FirstName MiddleName
*   **routing Array<**<mark style="color:blue;">**routing**</mark>**> **<mark style="color:orange;">**Optional**</mark>

    Routing information.
*   **segmentIndex **<mark style="color:blue;">**int**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Segment sequence. This will always be 1 as this would be the details of the 1st sector in the booking.
*   **carrier **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    2-character IATA code of the booked airline.
*   **flightNumber **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    The flight number of the 1st sector as received in the order.
*   **depAirport **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    IATA Code of departure city or airport.
*   **arrAirport **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    IATA Code of arrival city or airport.
*   **fromDate **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    Departure date, the format is YYYYMMDD.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo": "TESTA20240627114717735",
    "pnrCode": "XYZ87T",
    "airlinePNR": "S75666",
    "carrier": "G9",
    "passengers": [
        {
            "name": "Kotwal/Behram"
        }
    ],
    "routing": {
        "fromSegments": [
            {
                "segmentIndex": 1,
                "carrier": "G9",
                "flightNumber": "G9147",
                "depAirport": "SHJ",
                "arrAirport": "JED",
                "fromDate": "20240716"
            }
        ]
    },
    "isCompletedOrder": "true"
}       
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **status **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: success

    2: System error
*   **msg **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Error message
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number
*   **orderStatus **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: Unpaid

    1: Ticketing-in-Process

    2: Ticketed
    
    \-3: Cancelled(When the booking is failed due to the request information)
    Order number
*   **orderList **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    List all the ancillary orders in the given orderNo, including in-booking and post-booking transactions.

*   **ticketStatus **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    0: Ticket not issued

    1: Ticket issued
*   **ticketErrorCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    It's only available when orderStatus = -3.&#x20;

    Please check the definition of ticketErrorCode [**here**](../overview/errors.md#ticket-error-codes)****
*   **ticketErrorMessage **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

    It's only available when orderStatus = -3.&#x20;

    Error message
*   **totalPrice **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total fare of this order in the currency TheAtlas settled with you.
*   **totalTransactionFee **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total technical fees for this order in the currency TheAtlas settled with you.
*   **currency **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The currency TheAtlas settled with you.
*   **vendorTotalPrice **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Total fare of this order in the vendor's currency, reference for you to generate the specific credit card.
*   **vendorTotalAncillaryPrice **<mark style="color:blue;">**decimal**</mark>** 

    Total ancillary fare of this order in the vendor's currency.
*   **vendorCurrency **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Vendor's currency.
*   **supportPaymentMethod **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    1: Prepayment Only

    3: Both Credit Card Payment and Prepayment Available
    
    This tag shows which payment method is supported for that particular booking.
*   **supportPaymentMethods **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    1: Prepayment Only

    3: Both Credit Card Payment and Prepayment Available

    This tag lists down all the various payment methods available for payment for the booking.
*   **paymentMethod **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

    1: Prepayment Only

    3: Both Credit Card Payment and Prepayment Available

    This is the mode of payment used to pay for the booking.
*   **tktLimitTime **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Payment deadline for this order. This time will be displayed in SGT (GMT +8)
*   **paxTicketInfos Array<**[**PAXTicketInfo**](order.md#paxticketinfo-schema/)**> **<mark style="color:green;">**Required**</mark>

    Ticket information for passengers, the same format as the PAXTicketInfo in order response.
*   **routing Object<**[**RouteElement**](search.md#route-element-schema/)**> **<mark style="color:green;">**Required**</mark>

    Route and fare details. The structure is the same format as "Routing Element" in search response.
*   **airlineBookings Array<**[**ManageBookingElement**]**> **<mark style="color:green;">**Required**</mark>

*   **ancillaries Array<**<mark style="color:blue;">**AncillaryElement**</mark>**>**

    Ancillaries selection for the specific passenger

  * [**AncillaryElement**](order.md)
    
    *   **productCode **<mark style="color:blue;">**string**</mark>

        Ancillary product code;

        Got from routing element in the search/revalidation response.
     *   **segmentIndex **<mark style="color:blue;">**int**</mark>

         Segment sequence
     *   **offerId **<mark style="color:blue;">**string**</mark>

         unique identifier for this ancillary's offer.
     *   **auxSeatElement **<mark style="color:blue;">**Array**</mark>**  **<mark style="color:green;">**Required**</mark>

         Configuration of ordering when the seat is occupied

         SIMILAR_SEAT: Default, select a similar seat automatically

         STOP_SEAT: Stop seat and continue ticketing

         STOP_TICKET: Stop ticketing and cancel the order
     *   **row **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>
         Seat row

         **Example**: 27
            
     *   **column **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>
         Seat column

         **Example**: A

         Booking information of the airline.

*   **airlineCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    2 character IATA airline code.

*   **airlineName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Name of the airline.

*   **airlinePnr **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The record locator of the airline.

*   **airlineWebSiteAddress **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The URL of the public airline website.

*   **mmbEmail **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The email id to be used in the airline's MMB (Manage my Booking) section.

*   **tailDigitsOfPaymentCard **<mark style="color:blue;">**decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    The last 4 digits of the VCC used for payment.

*   **itineraryDownload **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    The link to download the itinerary of the trip.

       
{% endtab %}

{% tab title="Samples" %}
```
{
  "orderNo": "TESTA20240627114717735",
  "orderList": [
    {
      "orderNo": "TESTA20240627114717735",
      "orderStatus": "2",
      "ticketStatus": "1",
      "totalPrice": 86.31,
      "currency": "USD",
      "tktLimitTime": "2024-06-27 13:07:21",
      "vendorTotalPrice": 316.96,
      "vendorTotalAncillaryPrice": 0,
      "vendorCurrency": "AED",
      "adultTotalFare": 86.31,
      "childTotalFare": 86.31,
      "infantTotalFare": 153.79,
      "totalAncillaryPrice": 0,
      "totalTransactionFee": 1,
      "paymentFee": null,
      "supportPaymentMethod": 3
    },
    {
      "orderNo": "TESTB20240627120309525",
      "orderStatus": "0",
      "ticketStatus": "0",
      "totalPrice": 174.27,
      "currency": "USD",
      "tktLimitTime": "2024-06-27 12:19:10",
      "vendorTotalPrice": 640,
      "vendorTotalAncillaryPrice": 640,
      "vendorCurrency": "AED",
      "adultTotalFare": 0,
      "childTotalFare": null,
      "infantTotalFare": null,
      "totalAncillaryPrice": 174.27,
      "totalTransactionFee": 0,
      "paymentFee": null,
      "supportPaymentMethod": 1
    }
  ],
  "pnrCode": "ODNSPH",
  "orderStatus": null,
  "ticketStatus": null,
  "paxTicketInfos": [
    {
      "name": "Kotwal/Behram",
      "passengerType": 0,
      "birthday": "19890922",
      "gender": "M",
      "cardNum": "00000011",
      "cardType": "PP",
      "cardIssuePlace": "SG",
      "cardExpired": "20301230",
      "nationality": "LK",
      "ticketNos": [
        "S75666"
      ],
      "airlinePNRs": [
        "S75666"
      ],
      "contactEmails": [
        "TEST@GMAIL.COM"
      ],
      "contactPhones": [
        "0086-13928109091"
      ],
      "ancillaries": [
        {
          "productCode": "SCI_SEAT_B2_F9_PHL_LAS",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 63.8,
          "currency": "USD",
          "vendorPrice": 63.8,
          "vendorCurrency": "USD",
          "productType": null,
          "auxBaggageElement": null,
          "auxSeatElement": {
            "row": "2",
            "column": "B"
          }
        },
        {
          "productCode": "SCI_SEAT_A27_F9_LAS_ORD",
          "segmentIndex": 2,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 49.24,
          "currency": "USD",
          "vendorPrice": 49.24,
          "vendorCurrency": "USD",
          "productType": null,
          "auxBaggageElement": null,
          "auxSeatElement": {
            "row": "27",
            "column": "A"
          }
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_2PC_52KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 174.27,
          "currency": "USD",
          "vendorPrice": 640,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_17KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 109.74,
          "currency": "USD",
          "vendorPrice": 403,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        },
        {
          "productCode": "SCI_1PC_22KG",
          "segmentIndex": 1,
          "offerId": null,
          "buyMethod": "0",
          "ancillaryPrice": 50.11,
          "currency": "USD",
          "vendorPrice": 184,
          "vendorCurrency": "AED"
        }
      ]
    }
  ],
  "totalPrice": 2126.72,
  "currency": "USD",
  "tktLimitTime": null,
  "vendorTotalPrice": null,
  "vendorTotalAncillaryPrice": null,
  "vendorCurrency": null,
  "adultTotalFare": null,
  "childTotalFare": null,
  "infantTotalFare": null,
  "totalAncillaryPrice": null,
  "totalTransactionFee": null,
  "paymentFee": null,
  "supportPaymentMethod": 0,
  "supportPaymentMethods": null,
  "paymentMethod": null,
  "routing": {
    "fid": "lyuXAz1MVngismacM3wuiwJtmFMsLpRTfm0K2S99dsxi-G5TKL1BQQ..",
    "routingIdentifier": "aLLgQXmljm5IEm4F2B7GwEeO9d1gEcWId1SPa2qQU/Exzrmp46qTnP1Bf8nnsQGPliUgxaZGnRxPBBjFHiIgMWXmfDNoWMGlSBAzSStrZYrR/1H8sZENAaLkHq7StdgtFnCqK5m26fQhrveoISCbmz7ZAsfQcCDlbofv55bj9l6/mtrrU77wm6+6J5IB8vVHEHelUNgWevC0TCz2rsfF/wT88pb2eHTQlNmhNqBiXAjDiX47D2mSWlhB0LYI3ocs6P0jM9lV4hVrt+xXjNBBMYqAiG3TPWx6QfeTBjgt1+IwfYdzurVeKVFL3OSZMV2ZywXRwCf8qQtJX8OEUh9CzKFYopbYAwkGfOPJc9sd07lubzPS1rZmyg==",
    "supportCreditTransPayment": "1",
    "currency": "USD",
    "adultPrice": 65.93,
    "adultTax": 20.38,
    "childPrice": 65.93,
    "childTax": 20.38,
    "infantPrice": 153.79,
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
        "carrier": "G9",
        "flightNumber": "G9147",
        "depAirport": "SHJ",
        "depTime": "202407161400",
        "arrAirport": "JED",
        "arrTime": "202407161550",
        "stopCities": "",
        "duration": 170,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 2,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "G9",
        "operatingFlightnumber": "",
        "fareFamily": "lowest"
      }
    ],
    "retSegments": [],
    "combineIndexs": [],
    "rule": {
      "hasBaggage": 1,
      "baggageElements": [
        {
          "segmentNo": 1,
          "baggageType": "CabinBaggageOverheadLocker",
          "passengerType": 0,
          "baggagePiece": 1,
          "baggageWeight": 10,
          "baggageSize": null
        }
      ],
      "refundRules": [
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "AED",
          "refNoshow": "T",
          "refNoShowCondition": 0,
          "refNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 31233,
              "status": "T",
              "startMinute": 525600,
              "endMinute": 4320,
              "amount": 0,
              "currency": "AED"
            },
            {
              "ruleId": 31235,
              "status": "T",
              "startMinute": 4320,
              "endMinute": 1440,
              "amount": 0,
              "currency": "AED"
            },
            {
              "ruleId": 31237,
              "status": "T",
              "startMinute": 1440,
              "endMinute": 0,
              "amount": 0,
              "currency": "AED"
            },
            {
              "ruleId": 31243,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "AED"
            }
          ]
        }
      ],
      "changesRules": [
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "AED",
          "revNoshow": "T",
          "revNoShowCondition": 0,
          "revNoshowFee": 0,
          "ruleDetailList": [
            {
              "ruleId": 20046,
              "status": "H",
              "startMinute": 525600,
              "endMinute": 4320,
              "amount": 200,
              "currency": "AED"
            },
            {
              "ruleId": 20048,
              "status": "H",
              "startMinute": 4320,
              "endMinute": 1440,
              "amount": 200,
              "currency": "AED"
            },
            {
              "ruleId": 20050,
              "status": "T",
              "startMinute": 1440,
              "endMinute": 0,
              "amount": 0,
              "currency": "AED"
            },
            {
              "ruleId": 20056,
              "status": "T",
              "startMinute": 0,
              "endMinute": -525600,
              "amount": 0,
              "currency": "AED"
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
    "ancillaryProductElements": [
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_1PC_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 7.33,
        "currency": "USD",
        "vendorPrice": 26.89,
        "vendorCurrency": "AED",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 1,
          "weight": 20,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_1PC_20KG",
        "auxSeatElement": null,
        "displayPrice": null,
        "displayCurrency": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_30KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 27.03,
        "currency": "USD",
        "vendorPrice": 99.24,
        "vendorCurrency": "AED",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 30,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_30KG",
        "auxSeatElement": null,
        "displayPrice": null,
        "displayCurrency": null
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_2PC_40KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 0,
        "price": 36.94,
        "currency": "USD",
        "vendorPrice": 135.63,
        "vendorCurrency": "AED",
        "clientTechnicalServiceFee": 0,
        "clientTechnicalServiceFeeMode": null,
        "auxBaggageElement": {
          "piece": 2,
          "weight": 40,
          "isAllWeight": true,
          "size": null
        },
        "offerId": null,
        "maxQty": 1,
        "minQty": 1,
        "categoryCode": "StandardCheckInBaggage",
        "ancillaryCode": "SCI_2PC_40KG",
        "auxSeatElement": null,
        "displayPrice": null,
        "displayCurrency": null
      }
    ],
    "vendorFare": {
      "vendorAdultPrice": 242.1,
      "vendorAdultTax": 74.86,
      "vendorChildPrice": 242.1,
      "vendorChildTax": 74.86,
      "vendorInfantPrice": 564.78,
      "vendorInfantTax": 0,
      "vendorCurrency": "AED"
    },
    "bundleOptions": [],
    "links": null,
    "separateBookings": false,
    "refreshTime": null,
    "displayFare": null
  },
  "airlineBookings": [
    {
      "airlineCode": "G9",
      "airlineName": "Air Arabia",
      "airlinePnr": "S75666",
      "airlineWebSiteAddress": "https://www.airarabia.com",
      "mmbEmail": "TEST@GMAIL.COM",
      "tailDigitsOfPaymentCard": null,
      "extras": [
        {
          "name": "email",
          "remark": "email",
          "value": "TEST@GMAIL.COM"
        }
      ]
    }
  ],
  "itineraryDownload": "http://121.40.236.223:8081/itineraryDownload.do?orderNo=FKEm34znpwyGDFss5iwdXC7TNqd8iZaO",
  "contact": {
    "name": "TEST",
    "address": "A-3 NOIDA",
    "postcode": "201307",
    "email": "TEST@GMAIL.COM",
    "mobile": "0086-13928109091"
  },
  "ancillaryBuyMethod": null,
  "errorCode": null,
  "errorMessage": null,
  "airlineMessage": null,
  "locale": "",
  "status": 0,
  "msg": "success"
}
```
{% endtab %}
{% endtabs %}
