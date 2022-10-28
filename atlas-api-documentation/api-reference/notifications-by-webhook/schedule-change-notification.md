# Schedule Change Notification

### Schedule Change Notification Webhook

In case of flight schedule changes, you will receive the `order.schedulechange` notification on the server, you can process and notify your affected customers about this change.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>

    Identifier of client and user.
*   **type **<mark style="color:blue;">**string**</mark>

    Notification type.
* **data**
  *   **scheduleChangeType **<mark style="color:blue;">**int**</mark>

      Schedule change type.

      1: Schedule change

      2: Flight cancel
  *   **previousSegs Array<**<mark style="color:blue;">**scSegment**</mark>**>**

      The original segments
  *   **revisedSegs Array<**<mark style="color:blue;">**scSegment**</mark>**>**

      The revised segments

      *   **scSegment **<mark style="color:blue;">**\*\*\*\***</mark>** Array<**<mark style="color:blue;">**scSegment**</mark>**>**

          segment information for schedule change notification

          *   **carrier **<mark style="color:blue;">**string**</mark>

              carrier
          *   **flightNumber **<mark style="color:blue;">**string**</mark>

              flight number
          *   **depAirport **<mark style="color:blue;">**string**</mark>

              departure airport
          *   \*\*arrAirport \*\*<mark style="color:blue;">**string**</mark>

              arrival ariport
          *   \*\*depTime \*\*<mark style="color:blue;">**string**</mark>

              departure time
          *   \*\*arrTime \*\*<mark style="color:blue;">**string**</mark>

              arrival time
          *   \*\*depTerminal \*\*<mark style="color:blue;">**string**</mark>

              departure time
          * \*\*arrTerminal \*\*<mark style="color:blue;">**string**</mark>\
            arrival time
{% endtab %}

{% tab title="Samples" %}
**Schedule change with alternative flights**

```
{
    "cid":"rggat40831",
    "type":"order.schedulechange",
    "data":{
        "previousSeg":[
            {
                "carrier":"PC",
                "flightNumber":"PC2673",
                "depAirport":"ESB",
                "depTime":"2020-02-08 20:45:00",
                "arrAirport":"SAW",
                "arrTime":"2020-02-08 22:50:00",
                "departureTerminal":"",
                "arrivingTerminal":""
            },
            {
                "carrier":"PC",
                "flightNumber":"PC2674",
                "depAirport":"SAW",
                "depTime":"2020-02-08 23:55:00",
                "arrAirport":"ASR",
                "arrTime":"2020-02-09 01:20:00",
                "departureTerminal":"",
                "arrivingTerminal":""
            }
        ],
        "revisedSeg":[
            {
                "carrier":"PC",
                "flightNumber":"PC2673",
                "depAirport":"ESB",
                "depTime":"2020-02-08 21:45:00",
                "arrAirport":"SAW",
                "arrTime":"2020-02-08 23:50:00",
                "departureTerminal":"",
                "arrivingTerminal":""
            },
            {
                "carrier":"PC",
                "flightNumber":"PC2800",
                "depAirport":"SAW",
                "depTime":"2020-02-09 01:50:00",
                "arrAirport":"ASR",
                "arrTime":"2020-02-09 03:55:00",
                "departureTerminal":"",
                "arrivingTerminal":""
            }
        ],
        "scheduleChangeType":1
    }
}
```

**Flight cancellation without alternative flight**

```
{
    "cid":"rggat40831",
    "type":"order.schedulechange",
    "data":{
        "previousSeg":[
            {
                "carrier":"PC",
                "flightNumber":"PC2500",
                "depAirport":"ESB",
                "depTime":"2020-02-08 09:45:00",
                "arrAirport":"SAW",
                "arrTime":"2020-02-08 10:50:00",
                "departureTerminal":"",
                "arrivingTerminal":""
            }
        ],
        "revisedSeg":[

        ],
        "scheduleChangeType":2
    }
}
```
{% endtab %}
{% endtabs %}
