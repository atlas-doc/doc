# Atlas API Payments

**What Payment methods (Credit card, agency credit, etc.) does Atlas accept?**

We have flexible payment options for our partner agencies. However, the most popular methods are through a Virtual Credit Card (VCC) or advance payment (deposit) to maintain a positive cash balance with Atlas.



**How can we use a credit card to make payments?**

The customer can send your credit card information along with the pay.do request. Atlas will pass-through the credit card details to the airlines, and the airlines will settle with you directly. In this case, we will deduct the technical service fee from your account with Atlas.

Several airlines support the pass-through option, for which we have added the supportCreditTransPayment function in the routing element.

**Why am I not allowed to pay with "VCC Passthrough" mode when 2 airlines are combined (outbound and inbound) and when it's the same airline in both directions, "VCC Passthrough" is allowed?**

Today, Atlas does not support the usage of 2 VCCs in a single payment (pay.do) request. Whether the "VCC Passthrough" mode of payment is allowed or not is determined by the ticketing channel at Atlas' end. When the ticketing channels are different, 2 separate payments will need to be made for 2 different airlines and hence 2 different VCCs will be required. As Atlas does not support multiple VCCs in a single request, the payment mode will be changed to "Deposit" by Atlas' AI engine.
