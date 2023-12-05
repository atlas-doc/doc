# Airline Status Update Notification

### Airline Status Update Webhook

Once an airline's status is changed, an `airline.status` notification will be received on your server. You can process it and take action as required. For example; you could adjust your search caching strategy as per the status of the airline.

### EndPoint

The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}

*   **type **<mark style="color:blue;">**string**</mark>

    Notification type.
    Notification type = airline.status

* **data**
  *   **airline Array**<mark style="color:blue;">**string**</mark>

  Airline Code

  *   **airlineStatus **<mark style="color:blue;">**int**</mark>

  Airline Status. It is the same as the information in "Online Status" of Airline List on Atrip.

  Active = Online

  Maintenance = Airline is under maintenance

  Inactive = Offline


**`status` **<mark style="color:blue;">**string**</mark>

  Only for internal use by Atlas.


{% endtab %}
{% tab title="Samples" %}
```
{
  "data":{
     "airline":["TO","HV"],
     "airlineStatus":"Active"},
  "status":-1,
  "type":"airline.status"
}
```
{% endtab %}
{% endtabs %}


