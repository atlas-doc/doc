# Key Requirements and Order and Fulfillment Flow

{% hint style="info" %}
## Points to note:
### Seats
- When travelling with a child passenger, paid seats will be auto-allocated for 1 ADT and 1 CHD passenger by RyanAir (FR). Seat allocation is not mandatory for any other ADT passenger type.

### Multiple Email Ids
- The order.do request has to contain 2 email ids as mentioned below:
    - Passenger email id
    - Subscriber email id

### Priority Boarding
- When 2 cabin bags are booked (40 x 20 x 25 cm and 55 x 40 x 20 cm), priority boarding is included in the price.

### RyanAir's Terms and Conditions
The subscriber needs to procure the passenger’s acceptance to the following terms, by way of tick box or other means:
- “I confirm that by booking a Ryanair flight as part of my [name of Subscriber] package I have read and accepted Ryanair’s General Terms and Conditions of Carriage, Website Terms, Cookie Policy, Privacy Policy. I also acknowledge that I will need to log into or create a myRyanair account in order to manage my booking.”

{% endhint %}

## 1. Client allowed to obtain data through Ryanair's official API​
- The distribution of any prohibited or scraped content is strictly prohibited​
- Breach of this condition will lead to termination of Subscriber’s FR content agreement within one day

## 2. Order and fulfillment flow
### a. Price Transparency​
- Display airline fares separately from other surcharges (including airline payment fees, Atlas service fees, and Subscriber's markup)​
- Price transparency must cover both flight fares and ancillary charges (bags, seats, etc.)​
- Ensure end users can clearly see Ryanair's actual price

### b. Explicit Passenger Notifications​
- Customers must check boxes to accept Ryanair's terms of service, privacy policy, and cookie policy, and acknowledge they need to create or log in to a myRyanair account to manage bookings​
- Passengers must confirm their order on Ryanair's official website via a pop-up page before ticketing

### c. Passenger Information Transmission​
- Must collect and transmit passengers' genuine contact information to Ryanair, including email & phone number​
- When creating orders, include the subscriber's email address so Ryanair can copy them on ticket confirmations and flight change notifications

### d. Pre-ticketing Pop-up Confirmation
- Before ticketing, the system must display Ryanair's official website order confirmation page for passenger verification.

## 3. Pricing Transparency​
- FR's actual fares must be displayed separately from any payment fees/service charges/markups. Must be shown at verification stage at the latest. Mixed display is also prohibited to avoid misleading customers​

## 4. Customer Information Pass through​
- Ensure that passengers provide their accurate passenger contact information including email address, phone number, and postal address to Ryanair at the time of booking

## 5. Explicit Notice​
- Make the passengers aware that they will be redirected to the Ryanair Website to confirm their purchase of the Ryanair Flight Services before issuing tickets
