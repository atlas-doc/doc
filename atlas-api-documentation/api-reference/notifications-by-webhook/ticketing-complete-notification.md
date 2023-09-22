# Ticketing Complete Notification

### Ticket Notification Webhook

Once a ticket is booked, you will receive the `order.ticketed` notification on your server. You can process it and take action as required. For example, you could send a booking confirmation email with ticket details to your customer.

### EndPoint

The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>

    Identifier of client and user.
*   **type **<mark style="color:blue;">**string**</mark>

    Notification type.
* **data**
  *   **orderNo **<mark style="color:blue;">**string**</mark>

      Order number.
  *   **orderStatus **<mark style="color:blue;">**int**</mark>

      orderStatus=2 means ticketed
  *   **paxTicketInfos Array<**[**PAXTicketInfo**](broken-reference/)**>**

      Passengers' ticket information, the same format as the PAXTicketInfo in order response or retrive booking response, click [**here**](broken-reference/) \*\*\*\* to check the schema
{% endtab %}

{% tab title="Samples" %}
```
{
  "cid": "tviin65428",
  "data": {
    "orderNo": "TESTL20230922153224323",
    "orderStatus": 2,
    "paxTicketInfos": [
      {
        "airlinePNRs": [
          "S30814"
        ],
        "ancillaries": [],
        "birthday": "20160202",
        "cardExpired": "20400101",
        "cardIssuePlace": "CN",
        "cardNum": "123458",
        "cardType": "PP",
        "gender": "F",
        "name": "zhang/lisi",
        "nationality": "CN",
        "passengerType": 1,
        "ticketNos": [
          "S30814"
        ]
      },
      {
        "airlinePNRs": [
          "S30814"
        ],
        "ancillaries": [],
        "birthday": "19920202",
        "cardExpired": "20400101",
        "cardIssuePlace": "CN",
        "cardNum": "123457",
        "cardType": "PP",
        "gender": "F",
        "name": "li/si",
        "nationality": "CN",
        "passengerType": 0,
        "ticketNos": [
          "S30814"
        ]
      },
      {
        "airlinePNRs": [
          "S30814"
        ],
        "ancillaries": [],
        "birthday": "19910101",
        "cardExpired": "20400101",
        "cardIssuePlace": "CN",
        "cardNum": "123456",
        "cardType": "PP",
        "gender": "M",
        "name": "zhang/san",
        "nationality": "CN",
        "passengerType": 0,
        "ticketNos": [
          "S30814"
        ]
      }
    ]
  },
  "status": -1,
  "type": "order.ticketed"
}

```
{% endtab %}
{% endtabs %}
