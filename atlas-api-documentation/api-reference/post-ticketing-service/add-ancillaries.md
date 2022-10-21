# Add Ancillaries

### Dependency

Offer ancillary list function should be called in prior of this call

### Endpoint

[https://sandbox.atlaslovestravel.com/orderAncillary.do](https://sandbox.atlaslovestravel.com/orderAncillary.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Identifier of client and user.
*   #### orderNo                       <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.
*   #### passengers               Array<<mark style="color:blue;">PassengerElement</mark>>                                                     <mark style="color:blue;"></mark>                                                     <mark style="color:green;">Required</mark>

    Order number. It can be an order for ticketing, or an order for add bags. The format of each kind of order is different.

    * #### <mark style="color:blue;">PassengerElement</mark>
      *   #### name                             <mark style="color:blue;">string</mark>                                                                                  <mark style="color:green;">Required</mark>

          LastName/FirstName MiddleName.
      *   #### ancillaries                       Array<[AncillaryElement](add-ancillaries.md#undefined)>                                        <mark style="color:blue;"></mark>                                        <mark style="color:green;">Required</mark>

          Ancillaries selection for the specific passenger
      * #### [AncillaryElement](add-ancillaries.md#undefined)                                                                                 <mark style="color:blue;"></mark>                                                                                &#x20;
        *   #### segmentIndex       <mark style="color:blue;">int</mark>                                                                                       <mark style="color:green;">Required</mark>

            Segment sequence, start from 1. If it is round trip, sequence outbond and inbound together.
        *   #### offerId                       <mark style="color:blue;">string</mark>                                                                                <mark style="color:green;">Required</mark>

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
*   #### status                                     <mark style="color:blue;">int</mark>                                                                                              &#x20;

    0: success

    2: System error

    6: Price change
*   #### msg                                         <mark style="color:blue;">string</mark>                                                                                       &#x20;

    Error message
*   #### orderNo                                  <mark style="color:blue;">string</mark>                                                                                      &#x20;

    Add ancillary order number
* **originalOrderNo                  **<mark style="color:blue;">**string**</mark>   &#x20;

&#x20;       <mark style="color:blue;">****</mark>        The original order number                                                                     <mark style="color:blue;">****</mark>                                                                    &#x20;

*   #### totalPrice                               <mark style="color:blue;">decimal</mark>                                                                                  &#x20;

    Total fare of this order in the currency TheAtlas settled with you.
*   #### totalTransactionFee         <mark style="color:blue;">decimal</mark>                                                                                  &#x20;

    Total technical fees for this order in the currency TheAtlas settled with you.
*   #### currency                                 <mark style="color:blue;">string</mark>                                                                                     &#x20;

    The currency TheAtlas settled with you.
*   #### vendorTotalPrice                <mark style="color:blue;">decimal</mark>                                                                                 &#x20;

    Total fare of this order in the vendor's currency, reference for you to generate the specific credit card.
*   #### vendorCurrency                  <mark style="color:blue;">string</mark>                                                                                     &#x20;

    Vendor's currency.
*   #### tktLimitTime                          <mark style="color:blue;">string</mark>                                                                                     &#x20;

    Payment deadline for this order.
*   #### paxTicketInfos                      Array<<mark style="color:blue;">PAXTicketInfo</mark>>                                                  <mark style="color:blue;"></mark>                                                 &#x20;

    Ticket information for passengers

    * #### <mark style="color:blue;">PAXTicketInfo</mark>
      *   #### name                             <mark style="color:blue;">string</mark>                                                                                 &#x20;

          LastName/FirstName MiddleName.
      *   #### passengerType         <mark style="color:blue;">int</mark>                                                                                        <mark style="color:green;"></mark>        &#x20;

          0   ADT

          1   CHD
      *   #### birthday                       <mark style="color:blue;">string</mark>                                                                                &#x20;

          Birthday, Format: YYYYMMDD
      *   #### gender                          <mark style="color:blue;">string</mark>                                                                                &#x20;

          M : Male

          F  : Female
      *   #### cardNum                      <mark style="color:blue;">string</mark>                                                                                 &#x20;

          Passenger id card number
      *   #### cardType                      <mark style="color:blue;">string</mark>                                                                                 &#x20;

          Passenger id card type：

          PP - Passport

          GA - Hong Kong Macau Pass for China mainland citizens

          TW - Taiwan Pass for China mainland citizens

          TB - China mainland pass for Taiwanese

          HY - International Seaman's Certificate
      *   #### cardIssuePlace           <mark style="color:blue;">string</mark>                                                                                &#x20;

          Card issue country，IATA code of country
      *   #### cardExpired                  <mark style="color:blue;">string</mark>                                                                                &#x20;

          Card expire date，Format：YYYYMMDD
      *   #### nationality                     <mark style="color:blue;">string</mark>                                                                                &#x20;

          Nationality，IATA code of country
      *   #### ticketNos                       Array<<mark style="color:blue;">string</mark>>                                                                <mark style="color:blue;"></mark>                                                               &#x20;

          Ticket numbers
      *   #### airlinePNRs                   Array<<mark style="color:blue;">string</mark>>                                                                <mark style="color:blue;"></mark>                                                               &#x20;

          AirlinePNRs, the array count would be the same as ticketnos count
      *   #### ancillaries                    Array<<mark style="color:blue;">AncillaryElement</mark>>                                                                <mark style="color:blue;"></mark>                                                               &#x20;

          Ancillaries selection for the specific passenger

          * ****[**AncillaryElement**](add-ancillaries.md#undefined)****
            *   #### productCode                             <mark style="color:blue;">string</mark>                                                     &#x20;

                Ancillary product code;

                Got from routing element in the search/revalidation response.
            *   #### segmentIndex                           <mark style="color:blue;">int</mark>                                                            &#x20;

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
If you want to pay for the add-ancillary order, please call the [pay](broken-reference) function as same as the ticketing orders.
{% endhint %}
