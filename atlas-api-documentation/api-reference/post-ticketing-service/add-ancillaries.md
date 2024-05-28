# Order Ancillary

### Dependency

The "postbookingancillarysearch.do" function should be called prior to this one.

#### Procedure:

1. Copy the Session ID into the request body.

2. Type the passenger information and "product code" selected from the response in "postbookingancillarysearch.do".

### Endpoint {% debug uid="orderAncillary_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/postbookingancillaryorder.do](https://sandbox.atriptech.com/postbookingancillaryorder.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It is the original order number.

*   **ancillaryCategory **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Ancillary Category. Different categories of ancillaries need to be separately requested. Currently we only support "BAGGAGE".

*   **sessionId **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of the searched ancillary, received from the ancillary search response.
    
*   **passengers Array<**<mark style="color:blue;">**PassengerElement**</mark>**> **<mark style="color:green;">**Required**</mark>
     
    * <mark style="color:blue;">**PassengerElement**</mark>
      *   **name **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          LastName/FirstName MiddleName.
      *   **passengerType **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          0 ADT

          1 CHD
*   **ancillaries Array<**[**AncillaryElement**](add-ancillaries.md#undefined)**> **<mark style="color:green;">**Required**</mark>

          Ancillaries selection for the specific passenger
      * <mark style="color:blue;">**AncillaryElement**</mark>
        *   **segmentIndex **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

            Segment sequence. It starts from 1. If it is round trip, the outbound and inbound sequence would be together.
        *   **productCode **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

            Unique identifier for the ancillary product. Used for the order ancillary function.
            
{% endtab %}

{% tab title="Samples" %}
```json
{
"cid": "xxxxxxxxxx",
"ticketOrderNo": "TESTM20240520171341468",
"ancillaryCategory": "BAGGAGE",
"sessionId": "cde38a72-d7fa-4e5b-9ba5-08b6929143c8",
"passengers": [{
    "name": "TEST/ONE",
    "passengerType": 0,
    "ancillaries": [{
        "productCode": "AD_SCI_1PC_19KG",
        "segmentIndex": 1
                   }]
               }]
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
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to check the result.
    
*   **sessionId **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of the revalidation, received from search ancillary response.
*   **orderNo **<mark style="color:blue;">**string**</mark>

    Order number of the added ancillary.
    
*   **ticketOrderNo **<mark style="color:blue;">**string**</mark>

    Order number of the original ticket.

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

    Payment deadline for this order. This time will be displayed in SGT (GMT +8)
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

          AirlinePNRs, the array count would be the same as ticket nos count
      *   **ancillaries Array<**<mark style="color:blue;">**AncillaryElement**</mark>**>**

          Ancillaries selection for the specific passenger

          * [**AncillaryElement**](add-ancillaries.md#undefined)
            *   **productCode **<mark style="color:blue;">**string**</mark>

                Ancillary product code received from ancillary search response.
                
            *   **segmentIndex **<mark style="color:blue;">**int**</mark>

                Segment sequence

            *   **ancillaryPrice **<mark style="color:blue;">**int**</mark>

                Price for this ancillary.

            *   **offerId **<mark style="color:blue;">**int**</mark>

                unique identifier for this ancillary's offer.

            *   **currency **<mark style="color:blue;">**int**</mark>

                Currency for this ancillary price.

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
        
       *   **`size`  **<mark style="color:blue;">**string**</mark>

           Maximum size for ancillary baggage


\`\`
{% endtab %}
{% endtabs %}

{% tabs %}
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
