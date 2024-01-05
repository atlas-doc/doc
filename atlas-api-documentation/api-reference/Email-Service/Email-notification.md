# Email Notification

### Email Notification Webhook

Once Altas's email service receives the airline's email, you will receive the `email.all` notification on the server.

EndPoint ： The URL you configured to receive notifications

Method : Post

{% tabs %}
{% tab title="Schema" %}
*   **cid **<mark style="color:blue;">**string**</mark>

    Identifier of client and user.
    
*   **type **<mark style="color:blue;">**string**</mark>

    Notification type.
    
*   **`notificationId` **<mark style="color:blue;">**string**</mark>

      Notification ID
      
*   **`status` **<mark style="color:blue;">**string**</mark>

      In this type of notification status always = -1, internal field, ignore it.

      
* **data**
  *   **`orderNo` **<mark style="color:blue;">**string**</mark>

  Order number

  *   **`emailReceivingDate` **<mark style="color:blue;">**string**</mark>

  Receiving Time is the time Atlas received the airline's email.

  Format: yyyy-MM-dd HH:mm:ss UTC+08:00

  *   **`uniqueCode` **<mark style="color:blue;">**string**</mark>

  Unique Code of the email

  *   **`emailCategory` **<mark style="color:blue;">**string**</mark>

  Atlas email categories. Atlas categorizes emails but does not guarantee accuracy in classification.
  - Schedule change
  - Receipt
  - Payment Success
  - Verification
  - Trip Reminder
  - Promo code
  - Travel Itinerary
  - Advertisement
  - PNR Cancellation Success
  - Payment Due
  - Unidentified
  - Duplicated Schedule Change
  - Unaccounted Cancellation

  *   **`from` **<mark style="color:blue;">**string**</mark>

  Email “from” address

  *   **`to` **<mark style="color:blue;">**string**</mark>

  Email “to” address

  *   **`emailSubject` **<mark style="color:blue;">**string**</mark>
  
  Email “Subject”

  *   **`emailLink` **<mark style="color:blue;">**string**</mark>
  
  Email Link. Email Link is only valid for 10 mins.

  *   **`createTime` **<mark style="color:blue;">**string**</mark>
  Create Time is the time when Atlas created this email record in the Email list. Generally, it will be later than the receiving time.
  Format: yyyy-MM-dd HH:mm:ss UTC+08:00

{% endtab %}

{% tab title="Samples" %}

```
{
    "cid":"XXXXX",
    "data":{
        "orderNo":"XXXXXX",
        "emailReceivingDate":"2024-01-05 10:54:21",
        "uniqueCode":"e4afbecfd5727817ff73a71a94a2a64d",
        "emailCategory":"Payment Success",
        "from":"donotreply@easyjet.com",
        "to":"NSDLZCQTGJTEYXOMFOD@gorn.top",
        "emailSubject":"easyJet booking reference: XXXXX",
        "emailLink":"http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/2024/01/e4afbecfd5727817ff73a71a94a2a64d.eml?Expires=1704426870&OSSAccessKeyId=LTAI5tDmTE9iwtNdsqxVXuom&Signature=zF8aNNsGgY8n2jhsW7V1gmPLw8c%3D",
        "createTime":"2024-01-05 10:54:26"
    },
    "notificationId":"20240105105430470MJMOR",
    "status":-1,
    "type":"email.all"
}

```
{% endtab %}
{% endtabs %}
