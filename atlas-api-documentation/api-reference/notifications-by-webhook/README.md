# Notifications by Webhook

We will quickly walk you through the process to set up and handle webhooks for your Atlas API integration. Webhooks will automatically take care of notifying you about changes that happen to the bookings your customers have made. For example, when an airline has changed the flight schedule, affecting one of your orders. The Atlas API will send a notification about this event to your server, and you can process them and take necessary action, for example, updating your database or emailing the customer. Currently, we send out webhook notifications in four scenarios: &#x20;

1. Ticket booked: <mark style="color:green;">`order.ticketed`</mark>&#x20;
2. Change in flight schedule: <mark style="color:green;">`order.scheduleChange`</mark>&#x20;
3. Purchase of ancillary services post booking: <mark style="color:green;">`order.addonComplete`</mark>&#x20;
4. Ticket and ancillary service cancellation: <mark style="color:green;">`order.refundComplete`</mark>
