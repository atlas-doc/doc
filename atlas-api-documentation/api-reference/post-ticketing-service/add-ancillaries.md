# Add Ancillaries

### Dependency

Offer ancillary list function should be called in prior of this call

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

            Segment sequence, start from 1. If it is round trip, sequence outbond and inbound together.
        *   **productCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

            Unique identifier for the ancillary product, used for the following order ancillary function.
            
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "tviin65428",
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

    Add ancillary order number
    
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>

    Order number. It is an order for ticketing.

*   **totalPrice **<mark style="color:blue;">**decimal**</mark>

    Total fare of this order in the currency TheAtlas settled with you.
*   **totalTransactionFee **<mark style="color:blue;">**decimal**</mark>

    Total technical fees for this order in the currency TheAtlas settled with you.
*   **currency **<mark style="color:blue;">**string**</mark>

    The currency TheAtlas settled with you.
*   **vendorTotalPrice **<mark style="color:blue;">**decimal**</mark>

    Total fare of this order in the vendor's currency, reference for you to generate the specific credit card.
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

                Got from routing element in the search/revalidation response.
            *   **segmentIndex **<mark style="color:blue;">**int**</mark>

                Segment sequence

            *   **ancillaryPrice **<mark style="color:blue;">**int**</mark>

                Ancillary's price.

            *   **offerId **<mark style="color:blue;">**int**</mark>

                unique identifier for this ancillary's offer.

            *   **currency **<mark style="color:blue;">**int**</mark>

                The currency of ancillary's price.

            *   **auxSeatElement Array**

                Seat information.

            *   **`rowNo`  **<mark style="color:blue;">**int**</mark>
     
                Which row are the seat in

            *   **`seatNo`  **<mark style="color:blue;">**string**</mark>
     
                Seat Number
          
            *   **`status`  **<mark style="color:blue;">**boolean**</mark>
     
                true: Available seat.
                false: Unavailable seat.

            *   **`seatInfo Array`  **<mark style="color:blue;">**
     
                Seat information description

                position information：window/aisle/middle  Required, used to draw seat maps.

                other information,such as "exit".

            *   **` passengerType`  **<mark style="color:blue;">**

                Passenger types supported by seats.

                
            
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
