# Airline Online Status Update Notification

### Airline Online Status Update Webhook

Once a airline's online status is changed, you will receive the `airline.status` notification on your server. You can process it and take action as required. For example, you could adjust your search caching strategy.

### EndPoint

The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}

*   **type **<mark style="color:blue;">**string**</mark>

    Notification type. Notification type=airline.status

* **data**
  *   **airline Array**<mark style="color:blue;">**string**</mark>

  Airline Code.

  *   **airlineStatus **<mark style="color:blue;">**int**</mark>

  Ailline Online Status. It's the same as Online Status of Airline List on Atrip.

  Active = Online

  Maintenance = Airline is under maintenance.

  Inactive = Offline


**`status` **<mark style="color:blue;">**string**</mark>

  Internal field, no need to handle


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


