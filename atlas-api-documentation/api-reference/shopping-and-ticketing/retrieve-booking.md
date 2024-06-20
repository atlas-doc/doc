# Retrieve Booking

### Dependency

`Order` function should be called in prior to this call.

### Endpoint {% debug uid="queryOrderDetails_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/queryOrderDetails.do](https://sandbox.atriptech.com/queryOrderDetails.do)

{% hint style="info" %}
Please refer to the below information for the usage of the queryOrderDetails.do API.

1. All the parameters can be used together, if required.

2. “OrderNo” is “required” if “airlinePNR” and “carrier” cannot be provided upon calling the API. Inversely, “airlinePNR” and “carrier” are “required” if “OrderNo” cannot be provided.

3. In case parameters in request don’t match (such as “orderNo”, “airlinePNR”, “carrier” and "passengers"), API response will show the error message "Parameters don't match, please check and retry".

4. In case the parameters of “airlinePNR” and “carrier” cannot identify an unique order (e.g BC - PNR is made up with 4 number), customer needs to enter additional parameters such as "firstName" and "lastName" for identification. In such scenarios, API will respond with error msg ”Multi-orderNos are identified, please provide more parameters in the request, such as “firstName” and “lastName” under passengers’ element.”

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
*   **isCompletedOrder **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:green;">**Required**</mark>

    If it's true, it means the user wants to check all the order info (including air ticket and any post-booking ancillary attached). If it's false, it means the user wants to check the given order only. It could be the air ticket order in 1st transaction, or the post-booking ancillary order in 2nd transaction.
*   **passengers Array<**<mark style="color:blue;">**PassengerElement**</mark>**> **<mark style="color:orange;">**Optional**</mark>

    Passengers' information.

* #### <mark style="color:blue;">**PassengerElement**</mark>
*   **firstName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

  First name of the passenger.
*   **lastName **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

  Last name of the passenger.
    
{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo": "TESTA20240620095525476",
    "airlinePNR": "S92309",
    "carrier": "G9",
    "isCompletedOrder": "true",
    "passengers": [
        {
            "firstName": "ADAM",
            "lastName": "SMITH"
        }
    ]
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
*   **tktLimitTime **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Payment deadline for this order. This time will be displayed in SGT (GMT +8)
*   **paxTicketInfos Array<**[**PAXTicketInfo**](order.md#paxticketinfo-schema/)**> **<mark style="color:green;">**Required**</mark>

    Ticket information for passengers, the same format as the PAXTicketInfo in order response.
*   **routing Object<**[**RouteElement**](search.md#route-element-schema/)**> **<mark style="color:green;">**Required**</mark>

    Route and fare details. The structure is the same format as "Routing Element" in search response.
*   **airlineBookings Array<**[**ManageBookingElement**]**> **<mark style="color:green;">**Required**</mark>

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
    "orderNo": "TESTA20240620095525476",
    "orderList": [
        {
            "orderNo": "TESTA20240620095525476",
            "orderStatus": "2",
            "ticketStatus": "1",
            "totalPrice": 133.40,
            "currency": "USD",
            "tktLimitTime": "2024-06-20 11:15:30",
            "vendorTotalPrice": 489.91,
            "vendorTotalAncillaryPrice": 0.00,
            "vendorCurrency": "AED",
            "adultTotalFare": 133.40,
            "childTotalFare": 133.40,
            "infantTotalFare": 218.07,
            "totalAncillaryPrice": 0.00,
            "totalTransactionFee": 1.00,
            "paymentFee": null,
            "supportPaymentMethod": 3
        },
        {
            "orderNo": "TESTB20240620100624142",
            "orderStatus": "2",
            "ticketStatus": "1",
            "totalPrice": 81.42,
            "currency": "USD",
            "tktLimitTime": "2024-06-20 10:22:24",
            "vendorTotalPrice": 299.00,
            "vendorTotalAncillaryPrice": 299.00,
            "vendorCurrency": "AED",
            "adultTotalFare": 0.00,
            "childTotalFare": null,
            "infantTotalFare": null,
            "totalAncillaryPrice": 81.42,
            "totalTransactionFee": 0.00,
            "paymentFee": null,
            "supportPaymentMethod": 1
        }
    ],
    "pnrCode": "S5GROX",
    "orderStatus": null,
    "ticketStatus": null,
    "paxTicketInfos": [
        {
            "name": "Patil/Jitendra",
            "passengerType": 0,
            "birthday": "19591231",
            "gender": "M",
            "cardNum": "Z4885595",
            "cardType": "PP",
            "cardIssuePlace": "IN",
            "cardExpired": "20280611",
            "nationality": "IN",
            "ticketNos": [
                "S92309"
            ],
            "airlinePNRs": [
                "S92309"
            ],
            "contactEmails": [
                "jitendra_patil@persistent.com"
            ],
            "contactPhones": [
                "0091-987654321234"
            ],
            "ancillaries": [
                {
                    "productCode": "SCI_1PC_20KG",
                    "segmentIndex": 1,
                    "offerId": null,
                    "buyMethod": "0",
                    "ancillaryPrice": 81.42,
                    "currency": "USD",
                    "vendorPrice": 299.00,
                    "vendorCurrency": "AED"
                }
            ]
        }
    ],
    "totalPrice": 214.82,
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
        "fid": "LSliV-lBOchjlN3KJUqQL_mPBN0nvNrpVjkHVeWN5WdoGwdIOLav3fUYSZPlO2FN",
        "routingIdentifier": "aLLgQXmljm5IEm4F2B7GwEKQluoX4TVnd1SPa2qQU/Fv7YdQeP59K6Z7a19huCi/lx/9JT0nSkgkQQpugkuv0Mq0jSnTNCA4QFPYM6iGcHollB3xJSIuvYe9trgmfZ5UQs+EDbUemepQ+WprXAZ9CYGLBHekKRJMdAD+im9W2wY44inbr0j9pyQS4mYw/G1xm4SeFfcc97ETSL8R26VTfwa7fl3PT7lkHuq13N/34ZrlSRqSXcGePFziMZsYHmDK7S6re5/Hb3y13QAK7VcSLbntLalj5dk53kFJ3hu4dJlDX9AhoGS+EKXA6EH5RhaPeHwZbKI2jp4E0Wr/ntQb90HN1C6c7bv4NW8Jyn29SkVOlHDVsiAHtA==",
        "supportCreditTransPayment": "1",
        "currency": "USD",
        "adultPrice": 4.96,
        "adultTax": 128.44,
        "childPrice": 4.96,
        "childTax": 128.44,
        "infantPrice": 218.07,
        "infantTax": 0.00,
        "infantAllowed": true,
        "transactionFeePerPax": 1.00,
        "transactionFee": 1.00,
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
                "depTime": "202407201400",
                "arrAirport": "JED",
                "arrTime": "202407201550",
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
                    "refundFee": 0.0,
                    "currency": "AED",
                    "refNoshow": "T",
                    "refNoShowCondition": 0,
                    "refNoshowFee": 0.0,
                    "ruleDetailList": [
                        {
                            "ruleId": 31233,
                            "status": "T",
                            "startMinute": 525600,
                            "endMinute": 4320,
                            "amount": 0.0,
                            "currency": "AED"
                        },
                        {
                            "ruleId": 31235,
                            "status": "T",
                            "startMinute": 4320,
                            "endMinute": 1440,
                            "amount": 0.0,
                            "currency": "AED"
                        },
                        {
                            "ruleId": 31237,
                            "status": "T",
                            "startMinute": 1440,
                            "endMinute": 0,
                            "amount": 0.0,
                            "currency": "AED"
                        },
                        {
                            "ruleId": 31243,
                            "status": "T",
                            "startMinute": 0,
                            "endMinute": -525600,
                            "amount": 0.0,
                            "currency": "AED"
                        }
                    ]
                }
            ],
            "changesRules": [
                {
                    "changesType": 0,
                    "changesStatus": "T",
                    "changesFee": 0.0,
                    "currency": "AED",
                    "revNoshow": "T",
                    "revNoShowCondition": 0,
                    "revNoshowFee": 0.0,
                    "ruleDetailList": [
                        {
                            "ruleId": 20046,
                            "status": "H",
                            "startMinute": 525600,
                            "endMinute": 4320,
                            "amount": 200.0,
                            "currency": "AED"
                        },
                        {
                            "ruleId": 20048,
                            "status": "H",
                            "startMinute": 4320,
                            "endMinute": 1440,
                            "amount": 200.0,
                            "currency": "AED"
                        },
                        {
                            "ruleId": 20050,
                            "status": "T",
                            "startMinute": 1440,
                            "endMinute": 0,
                            "amount": 0.0,
                            "currency": "AED"
                        },
                        {
                            "ruleId": 20056,
                            "status": "T",
                            "startMinute": 0,
                            "endMinute": -525600,
                            "amount": 0.0,
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
                "price": 6.24,
                "currency": "USD",
                "vendorPrice": 22.91,
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
                "price": 11.31,
                "currency": "USD",
                "vendorPrice": 41.52,
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
                "price": 28.02,
                "currency": "USD",
                "vendorPrice": 102.89,
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
            "vendorAdultPrice": 18.20,
            "vendorAdultTax": 471.71,
            "vendorChildPrice": 18.20,
            "vendorChildTax": 471.71,
            "vendorInfantPrice": 800.83,
            "vendorInfantTax": 0.00,
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
            "airlinePnr": "S92309",
            "airlineWebSiteAddress": "https://www.airarabia.com",
            "mmbEmail": "jitendra_patil@persistent.com",
            "tailDigitsOfPaymentCard": null,
            "extras": [
                {
                    "name": "email",
                    "remark": "email",
                    "value": "jitendra_patil@persistent.com"
                }
            ]
        }
    ],
    "itineraryDownload": "http://121.40.236.223:8081/itineraryDownload.do?orderNo=FKEm34znpwxtNjvuGV7D9TuVfxqL3Rbs",
    "contact": {
        "name": "Patil/Jitendra",
        "address": null,
        "postcode": null,
        "email": "jitendra_patil@persistent.com",
        "mobile": "0091-987654321234"
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
