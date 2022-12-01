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
*   **orderNo **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
*   **passengers Array<**<mark style="color:blue;">**PassengerElement**</mark>**> **<mark style="color:green;">**Required**</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.

    * <mark style="color:blue;">**PassengerElement**</mark>
      *   **name **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

          LastName/FirstName MiddleName.
      *   **ancillaries Array<**[**AncillaryElement**](add-ancillaries.md#undefined)**> **<mark style="color:green;">**Required**</mark>

          Ancillaries selection for the specific passenger
      * [**AncillaryElement**](add-ancillaries.md#undefined)
        *   **segmentIndex **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

            Segment sequence, start from 1. If it is round trip, sequence outbond and inbound together.
        *   **offerId **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

            Unique identifier for this ancillary's offer, used for the following order ancillary function.
{% endtab %}

{% tab title="Samples" %}
```json
{
    "cid": "XXXXXXXX",
    "orderNo": "XPFIW20220209163159425",
    "passengers": [
        {
            "name": "TEST/ONE",
            "ancillaries":[ 
                {
                    "segmentIndex": 1,
                    "offerId":"53c50926b04441ae863ababe3eda2a71"
                }
            ]
        },
        {
            "name": "TEST/THREE",
            "ancillaries":[ 
                {
                    "segmentIndex": 1,
                    "offerId":"c5eb4f500394432ea88bf1b142cf33e5"
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
*   **orderNo **<mark style="color:blue;">**string**</mark>

    Add ancillary order number
*   \*\*originalOrderNo \*\*<mark style="color:blue;">**string**</mark>

    ```
     <mark style="color:blue;">****</mark>        The original order number                                                                     <mark style="color:blue;">****</mark>                                                                    
    ```
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
{% endtab %}

{% tab title="Samples" %}
```json
{
    "status": 0,
    "msg": null,
    "sessionId": null,
    "orderNo": "GXFDU20220117075403790AU05",
    "originalOrderNo": "GXFDU20220117075403790",
    "totalPrice": 233.17,
    "totalTransactionFee": 4.00,
    "currency": "USD",
    "vendorTotalPrice": 302.01,
    "vendorCurrency": "SGD",
    "tktLimitTime": "2022-01-24 14:32:14",
    "pnrCode": "GRJE8R",
    "includeExtraBaggage": 0,
    "paxTicketInfos": [
        {
            "name": "LI/SI",
            "passengerType": 0,
            "birthday": "19920513",
            "gender": "F",
            "cardNum": "E12345678",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20201206",
            "nationality": "CN",
            "ticketNos": [],
            "airlinePNRs": [],
            "ancillaries": []
        },
        {
            "name": "WANG/WU",
            "passengerType": 1,
            "birthday": "20120511",
            "gender": "F",
            "cardNum": "E12345678",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20201206",
            "nationality": "CN",
            "ticketNos": [],
            "airlinePNRs": [],
            "ancillaries": [
                {
                    "productCode": "SCI_BAG_ID_20KG_AABBBB",
                    "segmentIndex": 1,
                    "buyMethod": null,
                    "offerId": null
                }
            ]
        },
        {
            "name": "ZHAO/LIU",
            "passengerType": 0,
            "birthday": "20130111",
            "gender": "M",
            "cardNum": "E12345678",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20201206",
            "nationality": "CN",
            "ticketNos": [],
            "airlinePNRs": [],
            "ancillaries": []
        }
    ]
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
If you want to pay for the add-ancillary order, please call the [pay](broken-reference/) function as same as the ticketing orders.
{% endhint %}
