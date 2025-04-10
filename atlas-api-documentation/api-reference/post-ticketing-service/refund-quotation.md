# Refund Quotation

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="RefundQuotation_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/refundQuotation.do](https://sandbox.atriptech.com/refundQuotation.do)

{% hint style="info" %}
### Introduction

The Refund section includes a series of steps required for refunds, including requesting a refund quote, submitting the refund, and returning the refund status and results. This service supports the submission of requests for cancellation that require Atlas to process or for refunds that need to be executed by Atlas. It also allows a variety of cancellation and refund types, including voluntary, involuntary and void, etc.

### Features

-    Refund reason: Voluntary, Involuntary, Void

-    Service Level:

     -    Our refund quotations fall into three scenarios:
             -    We can obtain an accurate quotation from the airline and will quote it directly to you;
             -    We cannot obtain an accurate quotation through the airline. You can still submit the refund request, then we will process the refund, but the refund amount will be based on the actual amount refunded by the airline;
             -    Unrefundable.

     -    Our refund service includes the below steps, 
             -    Atlas submits the refund request to the airline: We provide a service time guarantee;
             -    Airline processes the refund request and responds with the result, and airline executes the refund. The duration for 2 steps depends on the airline's processing speed, and we will provide an estimated reference time based on our experience in handling such cases.

Please note the below while initiating a refund transaction.

1. **Refund of either inbound or outbound sector:** The full ticket needs to be refunded. Only outbound OR inbound sector cannot be refunded. Please contact the airline for the same.

2. **Refund for a partially used itinerary:** Partially used itinerary cannot be refunded. Please contact the airline for the same.

3. **Refund for a specific passenger:** We support the refund of a specific passenger in an itinerary. For example, if there are 3 passengers and only one of them is to be refunded, please send us your refund request.

4. Apart from voluntary, involuntary and void, we currently do not support other types of refunds, such as medical or death refunds. Please contact customer service for manual assistance.

5. The customer is responsible to check whether the traveler has already made ancillary purchase in the transaction. 

6. No email notifications will be sent for refunds rejected by Atlas.

{% endhint %}

## Request

{% tabs %}
{% tab title="Schema" %}
## orderNo
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"TESTA20240725164512131"`  

## airlinePNR
- **Type:** String  
- **Required:** No  
- **Description:** The record locator of the airline. You can choose to requst either orderNo or airlinePNR. 
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"S24933"`  

## carrier
- **Type:** String  
- **Required:** No  
- **Description:** Airline carrier code.  
- **Constraints:** 2-letter airline code.  
- **Default:** None  
- **Example:** `"G9"`  

## displayCurrency
- **Type:** String  
- **Required:** No  
- **Description:** The alternative currency in which the fare and taxes amount needs to be displayed. The 3-letter currency code should be entered.  
- **Constraints:** 3-letter currency code.  
- **Default:** None  
- **Example:** `"EUR"`  

## refundRequestList
Ticket selection of the passengers and flights which is going to refund.

### refundRequestList[].lastName
- **Type:** String  
- **Required:** Yes  
- **Description:** Last name of the passenger requesting a refund.  
- **Constraints:** Alphabetic characters only.  
- **Default:** None  
- **Example:** `"ZHANG"`  

### refundRequestList[].firstName
- **Type:** String  
- **Required:** Yes  
- **Description:** First name of the passenger requesting a refund.  
- **Constraints:** Alphabetic characters only.  
- **Default:** None  
- **Example:** `"SAN"`

### refundRequestList[].refundReason
- **Type:** String  
- **Required:** Yes  
- **Description:** Code representing the reason for the refund request.  
- **Constraints:** 0: Involuntary  1: Voluntary  4: Void  
- **Default:** None  
- **Example:** `"1"`  

### refundRequestList[].segments
#### refundRequestList[].segments[].depDate
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure date of the segment which the passenger wants to refund  (yyyyMMdd).
- **Constraints:** Format `YYYYMMDD`.  
- **Default:** None  
- **Example:** `"20240827"`  

#### refundRequestList[].segments[].flightNo
- **Type:** String  
- **Required:** Yes  
- **Description:** Flight number of the segment which the passenger wants to refund.  
- **Constraints:** Alphanumeric flight number.  
- **Default:** None  
- **Example:** `"LJ820"`  

#### refundRequestList[].segments[].depAirport
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code of the departure airport.  
- **Constraints:** 3-letter airport code.  
- **Default:** None  
- **Example:** `"PVG"`  

#### refundRequestList[].segments[].arrAirport
- **Type:** String  
- **Required:** Yes  
- **Description:** IATA code of the arrival airport.  
- **Constraints:** 3-letter airport code.  
- **Default:** None  
- **Example:** `"CJU"`  

    
{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo": "TESTA20240725164512131",
    "airlinePNR": "S24933",
    "carrier": "G9",
    "displayCurrency": "EUR",
    "refundRequestList": [
        {
            "lastName": "ZHANG",
            "firstName": "SAN",
            "segments": [
                {
                    "depDate": "20240827",
                    "flightNo": "LJ820",
                    "depAirport": "PVG",
                    "arrAirport": "CJU"
                },
                {
                    "depDate": "20240828",
                    "flightNo": "LJ819",
                    "depAirport": "CJU",
                    "arrAirport": "PVG"
                }
            ],
            "refundReason": "1"
        }
    ]
}
```
{% endtab %}
{% endtabs %}

## Response

{% hint style="info" %}

### Deprecated Fields
Please note that the below fields are now deprecated. New fields have been introduced to fulfill their function.
- originalTotalFareAmount
- originalTotalAncillaryAmount
- originalTotalAmount
- airlinePenaltyAmountForFare
- airlinePenaltyAmountForAncillaries
- airlinePenaltyAmount
- estimatedRefundAmount
- transactionFee
- Journey
- status (Refund rules array)

{% endhint %}

{% tabs %}
{% tab title="Schema" %}
## **displayCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** The alternative currency in which the fare and taxes amount needs to be displayed. The 3-letter currency code should be entered. 
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"EUR"`  

## **fastConfirmation**
- **Type:** Integer  
- **Required:** Yes
- **Description:**  Fast confirmation depends on whether the airline supports auto fulfillment.  
- **Constraints:** `0` for False, `1` for True.  
- **Default:** `0`  
- **Example:** `0`  

## **expectedConfirmationDate**
- **Type:** String  
- **Required:** Yes
- **Description:** Expected date of getting airline refund confirmation.  
- **Constraints:** Format `YYYYMMDD`.  
- **Default:** None  
- **Example:** `"20241217"`  

## **expectedRefundDate**
- **Type:** String  
- **Required:** Yes
- **Description:** Expected date of getting refund.  
- **Constraints:** Format `YYYYMMDD`.  
- **Default:** None  
- **Example:** `"20241220"`  

## **refundQuoteType**
- **Type:** String  
- **Required:** Yes   
- **Description:** Type of refund quote：
    -    AccurateQuote：quotation based on the calculated amount.
    -    CannotQuote: quotation is unknown and will be according to the airline's rates
    -    NonRefundable: the ticket is non refundable  
- **Constraints:** Possible values: `AccurateQuote`, `CannotQuote`, `NonRefundable`.  
- **Default:** None  
- **Example:** `"AccurateQuote"`  

## **refundOfferId**
- **Type:** String  
- **Required:** Yes
- **Description:** Refund offer id for this quotation which can be used for the coming refund call.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"q_56dec16d1fe2472095426d0286cc1965"`  

## **isRefundable**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** True : Refundable  False: Non-Refundable  
- **Constraints:** `true` or `false`.  
- **Default:** None  
- **Example:** `true`  

## **refundTickets**
The refund calculation for each of the passengers whose refund quote has been requested

### **refundTickets[].lastName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Last name of the passenger who wants to refund.  
- **Constraints:** Alphabetic characters only.  
- **Default:** None  
- **Example:** `"ZHANG"`  

### **refundTickets[].firstName**
- **Type:** String  
- **Required:** Yes  
- **Description:** First name of the passenger who wants to refund.  
- **Constraints:** Alphabetic characters only.  
- **Default:** None  
- **Example:** `"SAN"`  

### **refundTickets[].ticketNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** The PNR received from the airline in the retrieve PNR response.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"S43484"`  

## **refundFareAmount**
### **refundFareAmount.currency**
- **Type:** String  
- **Required:** Yes 
- **Description:** The refund calculation for flight fare and inflow ancillaries.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"USD"`  

### **refundFareAmount.originalFareAmount**
- **Type:** Number  
- **Required:** Yes 
- **Description:** Original fare of the flight.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `141.19`  

### **refundFareAmount.estimatedRefundAmount**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Estimated amount which can be got back for this refund of flight.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`  

### **refundFareAmount.displayOriginalFareAmount**
- **Type:** Number  
- **Required:** No   
- **Description:** Original Fare Amount in display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `241.19`  

### **refundFareAmount.displayEstimatedRefundAmount**
- **Type:** Number  
- **Required:** No   
- **Description:** EstimatedRefundAmount in display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`  

## **refundPostTicketingServiceAmounts**
The refund calculation for Post-ticketing Servrice, including baggage, seat, etc. Each post-ticketing order will be present as an object.

### **refundPostTicketingServiceAmounts[].postTicketingOrderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number for the post-ticketing service.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"BAFAU20241220110246534"`  

### **refundPostTicketingServiceAmounts[].currency**
- **Type:** String  
- **Required:** Yes   
- **Description:** Currency used for post-ticketing service calculations.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"USD"`  

### **refundPostTicketingServiceAmounts[].originalPostTicketingServiceAmount**
- **Type:** Number  
- **Required:** Yes   
- **Description:** The original amount charged for the post-ticketing service.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `141.19`  

### **refundPostTicketingServiceAmounts[].estimatedRefundAmount**
- **Type:** Number  
- **Required:** Yes   
- **Description:** Estimated amount which can be got back for this refund of Ancillaries.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`  

### **refundPostTicketingServiceAmounts[].displayPostTicketingServiceAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** The original post-ticketing service amount in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `241.19`  

### **refundPostTicketingServiceAmounts[].displayEstimatedRefundAmount**
- **Type:** Number  
- **Required:** No   
- **Description:** The estimated refund amount displayed in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`

## **serviceFee**
Service fee of refund.

### **serviceFee.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency used for the service fee.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"USD"`  

### **serviceFee.transactionFee**
- **Type:** Number  
- **Required:** Yes   
- **Description:** Transaction Fee of refund.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `1.00`  

### **serviceFee.displayTransactionFee**
- **Type:** Number  
- **Required:** No   
- **Description:** TransactionFee in display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `1.50`

## **refundRules**
The refund rules for the fare whose refund quote has been requested.

### **refundRules[].airline**
- **Type:** String  
- **Required:** Yes   
- **Description:** Airline code for which the refund rule applies.  
- **Constraints:** 2-letter IATA airline code.  
- **Default:** None  
- **Example:** `"LJ"`  

### **refundRules[].refundReason**
- **Type:** String  
- **Required:** Yes   
- **Description:** The reason for the refund.  
- **Constraints:** Predefined reason codes such as `0` (Involuntary), `1` (Voluntary), `4` (Void).  
- **Default:** None  
- **Example:** `"1"`  

### **refundRules[].passengerType**
- **Type:** String  
- **Required:** No   
- **Description:** Passenger type for which the refund rule applies.  
- **Constraints:** Can be `ADT` (Adult), `CHD` (Child), `INF` (Infant).  
- **Default:** `""`  
- **Example:** `"ADT"`  

### **refundRules[].penaltyAmount**
- **Type:** String  
- **Required:** No  
- **Description:** The penalty amount charged for the refund.  
- **Constraints:** Monetary value with currency code.  
- **Default:** None  
- **Example:** `"480.00 CNY"`  

### **refundRules[].penaltyPercent**
- **Type:** Number  
- **Required:** No  
- **Description:** The percentage of the fare charged as penalty.
- **Constraints:** Must be a positive number.  
- **Default:** `0`  
- **Example:** `0.0`  

### **refundRules[].penaltyPercentBase**
- **Type:** String or Null  
- **Required:** No   
- **Description:** The calculation on which the penalty percentage is based.  
- **Constraints:** Can be `fare`, `fare+tax`.  
- **Default:** `null`  
- **Example:** `null`  

### **refundRules[].airlineFee**
- **Type:** String  
- **Required:** No   
- **Description:** Additional airline fee for processing the refund.  
- **Constraints:** Monetary value with currency code.  
- **Default:** `"0"`  
- **Example:** `"0"`  

### **refundRules[].taxRefundable**
- **Type:** Boolean  
- **Required:** No   
- **Description:** Indicates whether the tax is refundable is available.  
- **Constraints:** `true` or `false`.  
- **Default:** None  
- **Example:** `true`  

### **refundRules[].fareRefundable**
- **Type:** Boolean  
- **Required:** No   
- **Description:** Indicates whether the ticket is refundable.  
- **Constraints:** `true` or `false`.  
- **Default:** None  
- **Example:** `true`  

### **refundRules[].refundableAncillaries**
- **Type:** Array  
- **Required:** No   
- **Description:** List of refundable ancillary services, if any.  
- **Constraints:** The options are:
    -    StandardCheckInBaggage
    -    CabinBaggage
    -    CabinBaggageUnderSeat
    -    CabinBaggageOverheadLocker  
- **Default:** `[]`  
- **Example:** `[StandardCheckInBaggage]`  

### **refundRules[].startMinute**
- **Type:** Integer  
- **Required:** No   
- **Description:** Starting time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.  
- **Constraints:** Positive or negative integer representing minutes.  
- **Default:** None  
- **Example:** `525600`  

### **refundRules[].endMinute**
- **Type:** Integer  
- **Required:** No   
- **Description:** Ending time of rule application. Positive numbers represent XXX minutes before departure. Negative numbers represent XXX minutes after departure.
- **Constraints:** Positive or negative integer representing minutes.  
- **Default:** None  
- **Example:** `50`

## **referenceInformation**

### **referenceInformation.atlasPolicy**
- **Type:** String or Null  
- **Required:** No   
- **Description:** Atlas policy details related to refunds.  
- **Constraints:** Can be `null` or a policy description.  
- **Default:** `null`  
- **Example:** `null`  

### **referenceInformation.airline**
- **Type:** String  
- **Required:** No  
- **Description:** The airline associated with the refund request.  
- **Constraints:** 2-letter IATA airline code.  
- **Default:** None  
- **Example:** `"LJ"`  

### **referenceInformation.refundReason**
- **Type:** String  
- **Required:** No  
- **Description:** The reason for initiating the refund request.  
- **Constraints:** Predefined reason codes such as `0` (Involuntary), `1` (Voluntary), `4` (Void).  
- **Default:** None  
- **Example:** `"1"`  

### **referenceInformation.airlinePolicy**
- **Type:** String or Null  
- **Required:** No   
- **Description:** Airline-specific refund policy details.  
- **Constraints:** Can be `null` or a policy description.  
- **Default:** `null`  
- **Example:** `null`  

### **orderNo**
- **Type:** String  
- **Required:** Yes
- **Description:** Order number.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"TESTA20240903015953777"`  

## **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status code.  
- **Constraints:** `0` for Success, `2` for System error.  
- **Default:** None  
- **Example:** `0`  

## **msg**
- **Type:** String or Null  
- **Required:** No  
- **Description:** Response message.  
- **Constraints:** None  
- **Default:** `null`  
- **Example:** `null`
        
{% endtab %}

{% tab title="Samples" %}
```
{
    "currency": "USD",
    "originalTotalFareAmount": 141.19,
    "originalTotalAncillaryAmount": 381.00,
    "originalTotalAmount": 522.19,
    "airlinePenaltyAmountForFare": 66.20,
    "airlinePenaltyAmountForAncillaries": 381.00,
    "airlinePenaltyAmount": 447.20,
    "estimatedRefundAmount": 74.99,
    "transactionFee": 2.00,
    "refundOfferId": "q_56dec16d1fe2472095426d0286cc1965",
    "isRefundable": true,
    "refundTickets": [
        {
            "lastName": "ZHANG",
            "firstName": "SAN",
            "ticketNo": "S43484",
            "currency": "USD",
            "originalFareAmount": 141.19,
            "originalAncillaryAmount": 381.00,
            "originalTotalAmount": 522.19,
            "refundableAmountForFare": 74.99,
            "refundableAmountForAncillaries": 0.00,
            "refundReason": "1",
            "airlinePenaltyAmountForFare": 66.20,
            "airlinePenaltyAmountForAncillaries": 381.00,
            "airlinePenaltyAmount": 447.20,
            "estimatedRefundAmount": 74.99
        }
    ],
    "refundRules": [
        {
            "airline": "LJ",
            "refundReason": "1",
            "passengerType": "",
            "penaltyAmount": "480.00 CNY",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 525600,
            "endMinute": 50
        },
        {
            "airline": "LJ",
            "refundReason": "1",
            "passengerType": "",
            "penaltyAmount": "1280.00 CNY",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 50,
            "endMinute": 0
        },
        {
            "airline": "LJ",
            "refundReason": "1",
            "passengerType": "",
            "penaltyAmount": "1280.00 CNY",
            "penaltyPercent": 0,
            "penaltyPercentBase": null,
            "airlineFee": "0",
            "taxRefundable": true,
            "fareRefundable": true,
            "refundableAncillaries": [],
            "startMinute": 0,
            "endMinute": -525600
        }
    ],
    "referenceInformation": {
        "atlasPolicy": null,
        "airline": "LJ",
        "refundReason": "1",
        "airlinePolicy": null
    },
    "orderNo": "TESTA20240903015953777",
    "status": 0,
    "msg": null
}

```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
Please note that the refund quote is valid for 2 hrs.
{% endhint %}
