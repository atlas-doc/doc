# Atlas API Post-ticketing

## **Do we get notified when there is a change in flight schedule for our customers?**

Sometimes airlines can make changes to their flight schedule. These changes range from minor changes in flight schedules to major ones such as cancellation or rerouting.
In this case, the airline will send the message to the contact email or mobile number of this booking.



## **How is the post-ticketing process being handled?**

Atlas API supports the post-ticketing process. The API allows for post-ticketing functions such as purchasing ancillary services, cancellation requests and processing refunds. Please refer to the API Reference section for further information. You can also reach out to our API support team or the Customer Service Centre to investigate any post-ticketing queries.



## **Is there a refund claim process for Atlas customers?**

The refund claim process differs as per the mode of payment. Please refer to the process as per the payment mode:


Mode of Payment: **Deposit**

1. When the refund has been initiated by customers via Atlas, Atlas will process the refund and keep a track of the refund status. Customers can request Atlas for the refund status.
   
2. When customers or the passenger submits the refund to the airline directly, customers can use the "Agent and Passenger Initiated Refund" feature in ATRIP to send Atlas a notification. Atlas will refund the ticket when Atlas receives the funds from the airline. Customers can also request Atlas for the refund status.

Mode of Payment: **VCC**

When the refund has been initiated by customers via Atlas OR when customers or the passenger submits the refund to the airline directly, the funds will be directly credited into customers VCC account by the airline. The card statement will show the credit into the account.



## **What is the REFUND process to be followed with Atlas?**

A comprehensive process for refund is documented below for our customers.

### Method of Initiating Refund with Atlas

#### 1) Atlas Initiated Refund
   
a) Refund button.

b) Service request (Cancel & Refund)

#### 2) Agency & Passenger Initiated Refund

a) Service request (Agency & Passenger Initiated Refund)
      
b)	Batch update.

#### Atlas Initiated Refund

##### Refund Button

Refund for all airlines can be submitted to Atlas.

In the “Booking Detail” screen:

1)	Click on the “Refund” button. A slide-out window is displayed.
   
2)	Check the refund fee.
   
3)	Accept the calculation and click the “Refund” button.
   
Our operations team will process the refund.

This is the recommended method of initiating refund with Atlas as the refund quotation will be instant.

 ![](../../.gitbook/assets/RefundFlow_1.png)


##### Service Request (Cancel & Refund)

In the “Booking Detail” screen, the customer can click on the “Raise a Request” button. A slide-out window will open. 

The customer can: 

1)	Select the “Post-Ticketing Request  Cancel & Refund” option.
   
2)	Add the information regarding the refund in the “Describe the issue” box.
   
3)	“Submit” the request.
   
Our operations team will process the refund once the quote is accepted by the customer.

![](../../.gitbook/assets/RefundFlow_2.png)

A service request can be submitted in 2 ways: 

1)	By clicking on the “Raise a Request” button on the “Booking Detail” screen.
   
2)	By clicking on the “New Request” button on the “My Requests” screen. Please note that the order number would need to be entered if this option is used.


#### Agent & Passenger Initiated Refund

##### Service Request (Agency & Passenger Initiated Refund)

When the customer or the passenger has already submitted the refund to the airline directly, the “Agency & Passenger Initiated Refund” option should be used.

In the “Booking Detail” screen, the customer can click on the “Raise a Request” button. A slide-out window will open. 

The customer can: 

1)	Select the “Post-Ticketing Request  Agent & Passenger Initiated Refund” option.
   
2)	“Submit” the request.
   
The refund request will be added to the “Refund” queue at Atlas’ end and processed by our operations team.

![](../../.gitbook/assets/RefundFlow_3.png)

The order number will be added to the refund queue at Atlas’ end.

A service request can be submitted in 2 ways:

1)	By clicking on the “Raise a Request” button on the “Booking Detail” screen.
   
2)	By clicking on the “New Request” button on the “My Requests” screen. Please note that the order number would need to be entered if this option is used.

##### Batch Update 

After initiating the refund on the airline website, the customer will access the “Financial” module and the “Refund” menu. The customer will then click on the “Agent & Passenger Initiated” tab.

![](../../.gitbook/assets/RefundFlow_4.png)

The refund template needs to be downloaded via the “Download File Template” button. 

The order numbers need to be added in the template and the same template must be uploaded by clicking on the “Initiate a Refund” button.

![](../../.gitbook/assets/RefundFlow_5.png)

Once uploaded, the order number will be displayed in the “Refunds” list.

![](../../.gitbook/assets/RefundFlow_6.png)

#### Checking the Refund Status

The refund status can be checked in ATRIP from “Finance  Refunds” section.

![](../../.gitbook/assets/RefundFlow_7.png)

#### Checking the Service Requests Created

The service request details will be also displayed in the “Request History” tab in the booking details.

![](../../.gitbook/assets/RefundFlow_8.png)

### Follow-up Process for Refunds

The customer should follow-up for refunds after a minimum of 21 days from the refund submission date.

The customers should use the already created service request (if refund initiated via a service request) or create a new service request via the "Post-ticketing Request --> Cancel & Refund" category to inquire for the submitted refunds.
