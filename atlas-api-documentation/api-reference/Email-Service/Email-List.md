# Email List

The "Email List" is used to retrieve email in batches.

### Dependency

No preceding function needs to be carried out.

### Endpoint
[https://sandbox.atriptech.com/event/queryMail.do](https://sandbox.atriptech.com/event/queryMail.do)

### Request

{% tabs %}
{% tab title="Schema" %}


**`orderNo`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Order number

At least one of the order number, receiving time and/or creation time must be specified for querying.

**`emailReceivingDateStart`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Start of the receiving time.

The time Atlas received the airline's email.

Format: yyyy-MM-dd hh:mm:ss UTC+08:00


**`emailReceivingDateEnd`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

End of the receiving time.

The time Atlas received the airline's email.

Format: yyyy-mm-dd hh:mm:ss UTC+08:00

You can only query data for up to one month at a time

**`createTimeStart`  **<mark style="color:blue;">**Date**</mark>**  **<mark style="color:green;">**Optional**</mark>

Start of creation time.

Create Time is the time when Atlas created this email record in the Email list. Generally, it will be later than the receiving time.

Format: yyyy-mm-dd hh:mm:ss UTC+08:00

**`createTimeEnd`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

End of creation time.

Create Time is the time when Atlas created this email record in the Email list. Generally, it will be later than the receiving time.

Format: yyyy-MM-dd hh:mm:ss UTC+08:00

You can only query data for up to one month at a time.

**`emailCategory`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

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

**`pageIndex`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Pagination

**`pageSize`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Number of records per page.

Maximum number=1000.

{% endtab %}


{% tab title="Samples" %}
```
{
  "orderNo": "TESTD20230811113115020",
  "emailReceivingDateStart": "2022-12-11 18:33:33",
  "emailReceivingDateEnd": "2022-12-11 18:33:33",
  "createTimeStart": "2022-12-11 18:33:33",
  "createTimeEnd": "2022-12-11 18:33:45",
  "emailCategory": "Unidentified",
  "pageIndex": 1,
  "pageSize": 100
}
```

{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}

**`status`  **<mark style="color:blue;">**int**</mark>

0: success

9999: error 

**`msg`  **<mark style="color:blue;">**string**</mark>

Error message.

**`hasNext`  **<mark style="color:blue;">**boolean**</mark>

True: There is also the next page

False：There is not the next page

* **records**
  *   **`orderNo` **<mark style="color:blue;">**string**</mark>

  Order number

  *   **`emailReceivingDate` **<mark style="color:blue;">**string**</mark>

  The time Atlas received the airline's email.

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
  "records": [
    {
      "orderNo": "TESTD20230811113115020",
      "emailReceivingDate": "2022-12-11 18:33:33",
      "uniqueCode": "2b5435c63102ac28d840b2a54f61e2db",
      "emailCategory": "Unidentified",
      "from": "xiaoyebiao@qq.com",
      "to": "connexpay@mx.theatlas.top",
      "emailSubject": "sda",
      "emailLink": "http://order-oss-sg.oss-ap-southeast-1.aliyuncs.com/2022/12/2b5435c63102ac28d840b2a54f61e2db.eml?Expires=1704364782&OSSAccessKeyId=LTAI5tDmTE9iwtNdsqxVXuom&Signature=Hl6vBTM8lv%2Fan%2FFnCVQmQnwaXnk%3D",
      "createTime": "2022-12-11 18:33:45"
    }
  ],
  "hasNext": false,
  "status": 0,
  "msg": "success"
}
```

{% endtab %}
{% endtabs %}



  








