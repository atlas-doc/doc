# Atlas API Payments

**What Payment methods (Credit card, agency credit, etc.) does Atlas accept?**&#x20;

We have flexible payment options for our partner agencies. However, the most popular methods are through a Virtual Credit Card (VCC) or advance payment to maintain a positive cash balance with Atlas.&#x20;

&#x20;

**How can we use a credit card to make payments?**&#x20;

There are two ways to go about this.&#x20;

The first option is to pay the total ticket amount plus the technical service fee to Atlas, and Atlas will settle the payment with the airlines on your behalf.&#x20;

The other option is to send your credit card information along with the `IssueTicket` request. Atlas will pass through the credit card details to the airlines, and the airlines will settle with you directly. In this case, we will deduct the technical service fee from your account with Atlas.&#x20;

Several airlines support the pass-through option, for which we have added the `supportCreditTransPayment` function in the routing element.&#x20;
