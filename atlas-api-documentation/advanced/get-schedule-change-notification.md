# Get Schedule Change Notification

### Schedule Change Notification Webhook

With Atlas, you can configure webhooks to automatically receive notifications about change in flight schedule made by airlines on your orders. Once you receive an `order.schedulechange` notification on your server, you can process it and take necessary action. To configure webhooks, you need to build a webhook receiver, create a webhook and you are all set to receive automatic notification.

EndPoint ：The URL you configured to receive notifications&#x20;

Method : Post

{% tabs %}
{% tab title="Samples" %}
```json
{
    "cid":"XXXXXXXX",
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
{% endtab %}
{% endtabs %}
