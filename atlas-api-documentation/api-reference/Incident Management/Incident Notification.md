# Incident Notification

### Incident Notification Webhook

In case of incident happens, you will receive the incident notification on the server, you can process and notify your affected customers about this incident.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
*   **`cid` **<mark style="color:blue;">**string**</mark>

    Identifier of client and user.
*   **`type` **<mark style="color:blue;">**string**</mark>

    Incident type.
    
    email.schedulechange: Schedule Change-Email Notification
    
    abnormal.cancelled: Unacounted Cancellation
    
    order.schedulechange: Schedule Change-API Notification. The Notification is <**[**Schedule Change Notification**](schedule-change-notification.md)**>
    
*   **`orderNo` **<mark style="color:blue;">**string**</mark>

      Order number.
* **data**
  *   **`scheduleChangeType` **<mark style="color:blue;">**int**</mark>
      Schedule change type. Only for Schedule Change-API Notification.

      1: Schedule change

      2: Flight cancel
      
  *   **`previousSegs` Array<**<mark style="color:blue;">**scSegment**</mark>**>**

      The original segments. Only for Schedule Change-API Notification. <**[**Schedule Change Notification**](schedule-change-notification.md)**>
  *   **`revisedSegs` Array<**<mark style="color:blue;">**scSegment**</mark>**>**

      The revised segments. Only for Schedule Change-API Notification. <**[**Schedule Change Notification**](schedule-change-notification.md)**>
      
  *   **`emailReceivingDate` **<mark style="color:blue;">**string**</mark>

      Email receiving Date(UTC+08:00) yyyymmdd hh:mm:ss. Only for Schedule Change-Email Notification.
      
  *   **`emailSubject` **<mark style="color:blue;">**string**</mark>
  
      Email Subject. Only for Schedule Change-Email Notification.
      
  *   **`emailLink` **<mark style="color:blue;">**string**</mark>

      Email Link, only valid for 10 mins. After the link expires, it can be retrieved from Incident List API. Only for Schedule Change-Email Notification.
      
