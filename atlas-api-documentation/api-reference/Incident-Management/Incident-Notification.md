# Incident Notification

### Incident Notification Webhook

In case of any incident, you will receive the incident notification on your server. You can process and notify your affected customers about this incident.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
*   **`cid` **<mark style="color:blue;">**string**</mark>

    Identifier of client and user.
*   **`type` **<mark style="color:blue;">**string**</mark>

    Incident type
    
    email.schedulechange: Schedule Change-Email Notification
    
    abnormal.cancelled: Unacounted Cancellation
    
    order.schedulechange: Schedule Change-API Notification. The Notification is **<mark style="color:blue;">**Schedule Change Notification**</mark>
      
*   **`notificationId` **<mark style="color:blue;">**string**</mark>

      Incident ID
      
*   **`status` **<mark style="color:blue;">**string**</mark>

      Incident staus
      
      0: Unconfirmed
      1: Confirmed
    
* **data**
  *   **`orderNo` **<mark style="color:blue;">**string**</mark>

      Order number
      
  *   **`scheduleChangeType` **<mark style="color:blue;">**int**</mark>
      Schedule change type. This is only for Schedule Change-API Notification.

      1: Schedule change

      2: Flight cancel
      
  *   **`previousSegs` Array<**<mark style="color:blue;">**scSegment**</mark>**>**

      The original segments. This is only for Schedule Change - API Notification. 
  *   **scSegment **<mark style="color:blue;">**\*\*\*\***</mark>** Array<**<mark style="color:blue;">**scSegment**</mark>**>**

          segment information for schedule change notification

         *   **carrier **<mark style="color:blue;">**string**</mark>

              carrier
         *   **flightNumber **<mark style="color:blue;">**string**</mark>

              flight number
         *   **depAirport **<mark style="color:blue;">**string**</mark>

              departure airport
         *   **arrAirport **<mark style="color:blue;">**string**</mark>

              arrival ariport
         *   **depTime **<mark style="color:blue;">**string**</mark>

              departure time
         *   **arrTime **<mark style="color:blue;">**string**</mark>

              arrival time
         *   **depTerminal **<mark style="color:blue;">**string**</mark>

              departure time
         *   **arrTerminal **<mark style="color:blue;">**string**</mark>\
              arrival time
          
  *   **`revisedSegs` Array<**<mark style="color:blue;">**scSegment**</mark>**>**

      The revised segments. This is only for Schedule Change-API Notification.
      
  *   **`emailReceivingDate` **<mark style="color:blue;">**string**</mark>

      Email receiving Date
      
      Format: (UTC+08:00) yyyymmdd hh:mm:ss. This is only for Schedule Change-Email Notification.
      
  *   **`emailSubject` **<mark style="color:blue;">**string**</mark>
  
      Email Subject. Only for Schedule Change-Email Notification.
      
  *   **`emailLink` **<mark style="color:blue;">**string**</mark>

      Email Link is only valid for 10 mins. After the link expires, it can be retrieved from Incident List API. This is only for Schedule Change-Email Notification.
{% endtab %}
      
{% tab title="Samples" %}
**Schedule Change-Email Notification**

```
{
    "cid":"rggat40831",
    "type":"email.schedulechange",
    "notificationId":"20230323113246035DNIDD",
    "status":0,
    "data":{
        "orderNo":"TESTS20230323103458265",
        "emailSubject":"IMPORTANT: Flight delay notice. Confirmation Code KDK7QG",
        "emailLink":"https://theatlas/#/email-detail/4378270"
    }
}
```
{% endtab %}
{% endtabs %}
