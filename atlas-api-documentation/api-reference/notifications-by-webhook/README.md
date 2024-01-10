# Notifications by Webhook

We will quickly walk you through the process to set up and handle webhooks for your Atlas API integration. Webhooks will automatically notify you on airline changes that affect your customers’ bookings. For example, when an airline has changed the flight schedule affecting one of your orders, the Atlas API will send a notification about this event to your server, and you can process it. For example, you may take actions by updating your database or emailing the customer. Currently, we send out webhook notifications in four scenarios: 

1. Ticket booked: <mark style="color:green;">`order.ticketed`</mark>
2. Change in flight schedule: <mark style="color:green;">`order.scheduleChange`</mark>
3. Purchase of ancillary services post-booking: <mark style="color:green;">`order.addonComplete`</mark>
4. Ticket and ancillary service cancellation: <mark style="color:green;">`order.refundComplete`</mark>
5. Airline status update: <mark style="color:green;">`airline.status`</mark>
6. Email noticification: <mark style="color:green;">`email.all`</mark>
