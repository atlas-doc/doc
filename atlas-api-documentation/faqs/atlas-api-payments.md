# Atlas API Payments

**What Payment methods (Credit card, agency credit, etc.) does Atlas accept?**

We have flexible payment options for our partner agencies. However, the most popular methods are through a Virtual Credit Card (VCC) or advance payment (deposit) to maintain a positive cash balance with Atlas.



**How can we use a credit card to make payments?**

There are two ways to go about this.

The first option is to pay the total ticket amount plus the technical service fee to Atlas, and Atlas will settle the payment with the airlines on your behalf.

The other option is to send your credit card information along with the `IssueTicket` request. Atlas will pass-through the credit card details to the airlines, and the airlines will settle with you directly. In this case, we will deduct the technical service fee from your account with Atlas.

Several airlines support the pass-through option, for which we have added the `supportCreditTransPayment` function in the `routing` element.
