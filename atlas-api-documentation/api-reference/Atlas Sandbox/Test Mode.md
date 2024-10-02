# Test mode

Like any other integration project, you should build your integration with Atlas API in the TEST mode. We want you to experience the Atlas API risk-free and explore all the different features. In Sandbox or the TEST mode you can test run the booking process without the risk of losing any money or booking actual flight tickets.

All you need is a testing access token as well as the sandbox URL to use the test mode. You can get this information through email after you have signed an NDA with Atlas. With a testing access token, you'll only be able to access resources created in test mode. With a live access token, you'll only be able to access resources created in live mode.

### Atlas Sandbox

When you search for flights in the test mode, you'll see offers from Atlas Sandbox. The airlines' fares in Sandbox are not as comprehensive and up to date as in the production environment. Atlas will not create real bookings or issue real tickets with the airline in the test mode.

### Testing VCC Errors

If required, our customers can test the VCC card failures by sending the "pay.do" request using the below information.

Cardholder First Name: "Reject"
Error Displayed: 604 - Payment declined by airline

Cardholder First Name: "Three DS"
Error Displayed: 616 - 3DS Authetication

Any card number and last name can be added. The test for VCC errors can be done for any airline.
