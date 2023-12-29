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
    
    order.schedulechange: Schedule Change-API Notification. The Notification is [<mark style="color:blue;">**Schedule Change Notification**</mark>]
      
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
      
  *   **`vendorRefundInformation` **<mark style="color:blue;">**string**</mark>

      Reference information for determining Unacounted Cancellation. This is only for Unacounted Cancellation.
      
      Fully: Atlas received a full refund from the airline without any schedule change or refund application.
      
      Cancelled: Atlas found some abnormal cancellation from airline.
      
  *   **`emailReceivingDate` **<mark style="color:blue;">**string**</mark>

      Email receiving Date
      
      Format: (UTC+08:00) yyyymmdd hh:mm:ss. This is only for Schedule Change-Email Notification.
      
  *   **`emailSubject` **<mark style="color:blue;">**string**</mark>
  
      Email Subject. Only for Schedule Change-Email Notification.
      
  *   **`emailLink` **<mark style="color:blue;">**string**</mark>

      Email Link is only valid for 10 mins. This is only for Schedule Change-Email Notification.
{% endtab %}
      
{% tab title="Samples" %}
**Schedule Change-Email Notification**

```
{
    "cid":"xxxxxxxxxx",
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

> **Tip**: The customer’s server URL needs to be registered with Atlas to receive notifications via webhook.

This can be done via API as shown below:

```
{

    "cid": "XXXXXXXX",
    
    "url": "https://xxx.com/xxxx"
    
}
```
The registration can also be done via ATRIP in the “Customer Information” tab of the “My Profile” menu.

Receiving notifications:

Three types of Incident notifications will be received. They are:

a. [Schedule Change – Email Notification]
Any schedule change email notification received from the airline using Atlas generated email id.

Sample:

```
{

    "cid":"xxxxxxxxxx",

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
Please note that the email link has a validity period of 10 minutes. The data received in the email will need to be stored at the customer’s end.


b. [Schedule Change - API Notification]

Structured Notification of Schedule Change. Information on old and new flights.

Sample:

```
{

  "cid": "xxxxxxxxxx",

  "data": {

    "orderNo": "XCEWF20221203094515954",

    "previousSegs": [

      {

        "arrAirport": "DPS",

        "arrTerminal": "",

        "arrTime": "2023-01-24 10:35:00",

        "carrier": "IU",

        "codeShare": false,

        "depAirport": "CGK",

        "depTerminal": "",

        "depTime": "2023-01-24 07:45:00",

        "flightNumber": "IU740"

      },

      {

        "arrAirport": "CGK",

        "arrTerminal": "",

        "arrTime": "2023-04-24 16:05:00",

        "carrier": "IU",

        "codeShare": false,

        "depAirport": "DPS",

        "depTerminal": "",

        "depTime": "2023-04-24 15:15:00",

        "flightNumber": "IU759"

      }

    ],

    "revisedSegs": [

      {

        "arrAirport": "CGK",

        "arrTerminal": "",

        "arrTime": "2023-04-24 16:05:00",

        "carrier": "IU",

        "codeShare": false,

        "depAirport": "DPS",

        "depTerminal": "",

        "depTime": "2023-04-24 15:15:00",

        "flightNumber": "IU743"

      }

    ],

    "scheduleChangeType": 1

  },

  "notificationId": "20230424050252711WZDMB",

  "status": 0,

  "type": "order.schedulechange"

}
```
c. [Unaccounted Cancellation]

These are cancellations made by our customers, airlines or passengers themselves. This info will be sent to the customers to confirm the same and inform the customer, if necessary.

Sample:

```
{

  "cid": "xxxxxxxxxx",

  "data": {

    "orderNo": "RQWUV20230617185232880",

    "vendorRefundInformation": "FULLY"

  },

  "notificationId": "20230906014000568DRLNX",

  "status": 0,

  "type": "abnormal.cancelled"

}
```
