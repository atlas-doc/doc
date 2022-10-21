# Addon Complete Notification

### Addon Complete Notification Webhook

When your customer books an ancillary service post booking their ticket, you will receive the `order.addonComplete` notification.

EndPoint ： The URL you configured to receive notifications&#x20;

Method : Post

{% tabs %}
{% tab title="Schema" %}
*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                &#x20;

    Identifier of client and user.
*   #### type                              <mark style="color:blue;">string</mark>                                                                                                 &#x20;

    Notification type.
* #### data                                                                                                                                                          <mark style="color:blue;"></mark>                                                                                      &#x20;
  *   #### addonOrderNo                                  <mark style="color:blue;">string</mark>                                                         &#x20;

      Order number.
  *   #### originalOrderNo                               <mark style="color:blue;">string</mark>                                                         &#x20;

      Order number.
  *   #### orderStatus                                        <mark style="color:blue;">int</mark>                                                                            &#x20;

      orderStatus=2 means ticketed
  *   #### paxTicketInfos                                  Array<[PAXTicketInfo](broken-reference)>                                   <mark style="color:blue;"></mark>                                  &#x20;

      Passengers' ticket information, the same format as the PAXTicketInfo in order response or retrive booking response, click [**here**](broken-reference) **** to check the schema
{% endtab %}

{% tab title="Sample" %}
```
{
    "cid": "rggat40831",
    "type": "order.addonComplete",
    "data":
    {
        "addonOrderNo": "BCNQL20201031184148568KLDKS",
        "originalOrderNo": "BCNQL20201031184148568",
        "orderStatus": "2",
        "paxTicketInfos": [
            {
                "name": "MOREL/JEROME",
                "passengerType": 0,
                "birthday": "19661118",
                "gender": "M",
                "cardNum": "G000000000",
                "cardType": "PP",
                "cardIssuePlace": "FR",
                "cardExpired": "20320118",
                "nationality": "FR",
                "ticketNos": [
                    "EDVLRZ"
                ],
                "airlinePNRs": [
                    "EDVLRZ"
                ],
                "ancillaries": [
                    {
                        "productCode": "SCI_BAG_ID_25KG_AABBBB",
                        "segmentIndex": 1
                    }
                ]
            }
        ]
    }  
}
```


{% endtab %}
{% endtabs %}
