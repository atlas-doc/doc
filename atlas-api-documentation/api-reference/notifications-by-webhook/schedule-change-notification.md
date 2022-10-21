# Schedule Change Notification

### Schedule Change Notification Webhook

In case of flight schedule changes, you will receive the `order.schedulechange` notification on the server, you can process and notify your affected customers about this change.

EndPoint ： The URL you configured to receive notifications&#x20;

Method : Post

{% tabs %}
{% tab title="Schema" %}
*   #### cid                                  <mark style="color:blue;">string</mark>                                                                                                &#x20;

    Identifier of client and user.
*   #### type                              <mark style="color:blue;">string</mark>                                                                                                 &#x20;

    Notification type.
* #### data                                                                                                                                           &#x20;
  *   #### scheduleChangeType               <mark style="color:blue;">int</mark> &#x20;

      Schedule change type.&#x20;

      1: Schedule change

      2: Flight cancel&#x20;
  *   #### previousSegs                                 **Array**<<mark style="color:blue;">scSegment</mark>>      <mark style="color:blue;"></mark>     &#x20;

      The original segments
  *   #### revisedSegs                             <mark style="color:blue;"></mark>       Array<<mark style="color:blue;">scSegment</mark>>      <mark style="color:blue;"></mark>     &#x20;

      The revised segments

      *   **scSegment                               **<mark style="color:blue;">****</mark>**  Array<**<mark style="color:blue;">**scSegment**</mark>**>**      <mark style="color:blue;"></mark>     &#x20;

          segment information for schedule change notification              <mark style="color:blue;"></mark>             &#x20;

          *   #### carrier                                  <mark style="color:blue;">string</mark>                                                                      &#x20;

              carrier
          *   #### flightNumber                     <mark style="color:blue;">string</mark>                                                                            &#x20;

              flight number
          *   #### depAirport                          <mark style="color:blue;">string</mark>                                                                            &#x20;

              departure airport
          *   **arrAirport                             **<mark style="color:blue;">**string**</mark>        <mark style="color:blue;"></mark>                                                                     <mark style="color:blue;"></mark><mark style="color:blue;"></mark>                                                                    &#x20;

              arrival ariport
          *   **depTime                                **<mark style="color:blue;">**string**</mark>    <mark style="color:blue;"></mark>                                                                         <mark style="color:blue;"></mark><mark style="color:blue;"></mark>                                                                        &#x20;

              departure time
          *   **arrTime                                  **<mark style="color:blue;">**string**</mark>       <mark style="color:blue;"></mark>                                                                      <mark style="color:blue;"></mark><mark style="color:blue;"></mark>                                                                     &#x20;

              arrival time                <mark style="color:blue;"></mark>               &#x20;
          *   **depTerminal                         **<mark style="color:blue;">**string**</mark>    <mark style="color:blue;"></mark>                                                                         <mark style="color:blue;"></mark><mark style="color:blue;"></mark>                                                                        &#x20;

              departure time
          *   **arrTerminal                           **<mark style="color:blue;">**string**</mark>       <mark style="color:blue;"></mark>                                                                      <mark style="color:blue;"></mark><mark style="color:blue;"></mark>                                                                     &#x20;

              arrival time      <mark style="color:blue;"></mark>     &#x20;
{% endtab %}

{% tab title="Samples" %}
#### Schedule change with alternative flights

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

#### Flight cancellation without alternative flight

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
