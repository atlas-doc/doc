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
    
*   **`notificationId` **<mark style="color:blue;">**string**</mark>

      Incident ID
      
*   **`status` **<mark style="color:blue;">**string**</mark>

      Incident staus
      
      0: Unconfirmed
      1: Confirmed
* **data**
  *   **orderNo **<mark style="color:blue;">**string**</mark>

      Order number.
      
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
    "cid":"XXXXXXX",
    "data":{
        "orderNo":"ATXFQ20230720193244809",
        "previousSegs":[
            {
                "arrAirport":"SGN",
                "arrTerminal":"",
                "arrTime":"2023-07-24 21:30:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"HKG",
                "depTerminal":"",
                "depTime":"2023-07-24 19:50:00",
                "flightNumber":"VJ877"
            },
            {
                "arrAirport":"HKG",
                "arrTerminal":"",
                "arrTime":"2023-10-18 18:50:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"SGN",
                "depTerminal":"",
                "depTime":"2023-10-18 14:55:00",
                "flightNumber":"VJ876"
            }
        ],
        "revisedSegs":[
            {
                "arrAirport":"SGN",
                "arrTerminal":"",
                "arrTime":"2023-07-24 21:30:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"HKG",
                "depTerminal":"",
                "depTime":"2023-07-24 19:50:00",
                "flightNumber":"VJ877"
            },
            {
                "arrAirport":"HKG",
                "arrTerminal":"",
                "arrTime":"2023-10-19 18:50:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"SGN",
                "depTerminal":"",
                "depTime":"2023-10-19 15:10:00",
                "flightNumber":"VJ876"
            }
        ],
        "scheduleChangeType":1
    },
    "notificationId":"20230917143240511TATVO",
    "status":0,
    "type":"order.schedulechange"
}

```

**Flight cancellation without alternative flight**

```
{
    "cid":"XXXXXXX",
    "data":{
        "orderNo":"ATXFQ20230720193244809",
        "previousSegs":[
            {
                "arrAirport":"SGN",
                "arrTerminal":"",
                "arrTime":"2023-07-24 21:30:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"HKG",
                "depTerminal":"",
                "depTime":"2023-07-24 19:50:00",
                "flightNumber":"VJ877"
            },
            {
                "arrAirport":"HKG",
                "arrTerminal":"",
                "arrTime":"2023-10-18 18:50:00",
                "carrier":"VJ",
                "codeShare":false,
                "depAirport":"SGN",
                "depTerminal":"",
                "depTime":"2023-10-18 14:55:00",
                "flightNumber":"VJ876"
            }
        ],
        "revisedSegs":[
        ],
        "scheduleChangeType":2
    },
    "notificationId":"20230917143240511TATVO",
    "status":0,
    "type":"order.schedulechange"
}

```
{% endtab %}
{% endtabs %}
