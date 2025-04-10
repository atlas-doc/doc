# Query Refund Status 

### Dependency

No preceding function needs to be carried out.

### Endpoint {% debug uid="RefundQuery_1.0" %}{% enddebug %}
    
[https://sandbox.atriptech.com/queryRefundOrders.do](https://sandbox.atriptech.com/queryRefundOrders.do)

## Request

{% tabs %}
{% tab title="Schema" %}
## **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Original order number.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"ZNMKU20220119160129691"`  

## **airlinePNR**
- **Type:** String  
- **Required:** No  
- **Description:** The record locator of the airline. Either `orderNo` or `airlinePNR` is required for the request.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"S24933"`  

## **carrier**
- **Type:** String  
- **Required:** No  
- **Description:** 2-character IATA airline code.  
- **Constraints:** Must be a valid 2-letter airline code.  
- **Default:** None  
- **Example:** `"G9"`  

## **refundCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** The code of the refund transaction received in the refund.do response.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"7961ab5b202642628e9595498ffea083"`  

## **displayCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** Alternative currency in which the fare and taxes should be displayed. The display currency remains unchanged throughout the refund process.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"EUR"`
    
{% endtab %}

{% tab title="Samples" %}
```json
{
  "orderNo": "TEST20220209163159425",
  "airlinePNR":"S24933",
  "carrier":"G9",
  "refundCode": "202407-0028",
  "displayCurrency": "EUR"
}
```
{% endtab %}
{% endtabs %}

## Response

{% hint style="info" %}

### Deprecated Fields
Please note that the below fields are now deprecated. New fields have been introduced to fulfill their function.
- currency
- originalTotalAncillaryAmount
- originalTotalAmount
- airlinePenaltyAmountForFare
- airlinePenaltyAmountForAncillaries
- airlinePenaltyAmount
- estimatedRefundAmount
- transactionFee
- Journey
- airlinePenaltyAmountForFare
- airlinePenaltyAmountForAncillaries
- airlinePenaltyAmount
  
{% endhint %}

{% tabs %}
{% tab title="Schema" %}
## **refundStatus**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** The present status of the refund process. If the ticket is paid by deposit: the status can be 0,1,2,3,4. If the ticket is paid by VCC pass through: the status can be 0,1,4,5,6. Withdrew is only in the refund claim.
- **Constraints:** Possible values:
  - `0`: Atlas Processing
  - `1`: Airline Processing (Submitted to airline by Atlas)
  - `2`: Refunded
  - `3`: Airline Refunding
  - `4`: Rejected
  - `5`: Fulfillment Done
  - `6`: Withdrew  
- **Default:** None  
- **Example:** `2`

## **refundOrders**
- **Type:** Array  
- **Required:** Yes  
- **Description:** List of refund orders requested.  
- **Constraints:** Must contain at least one refund order.  
- **Default:** None  
- **Example:** See `refundTickets` array below.  

## **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Original order number.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"ZNMKU20220119160129691"`  

## **refundCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Refund order number generated for this refund request.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"7961ab5b202642628e9595498ffea083"`  

## **currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** The currency of the fares and amounts below.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"USD"`  

## **displayCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** Alternative currency for displaying fare and tax amounts.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"EUR"`  

## **expectedConfirmationDate**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expected date of receiving airline refund confirmation.  
- **Constraints:** Format `YYYYMMDD`.  
- **Default:** None  
- **Example:** `"20241217"`  

## **expectedRefundDate**
- **Type:** String  
- **Required:** Yes  
- **Description:** Expected date of refund processing completion.  
- **Constraints:** Format `YYYYMMDD`.  
- **Default:** None  
- **Example:** `"20241220"`  

## **refundQuoteType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of refund quote.  
- **Constraints:** Possible values:
  - `AccurateQuote`: Based on the calculated amount.
  - `CannotQuote`: Refund amount is unknown, based on airline rates.
  - `NonRefundable`: Ticket is non-refundable.  
- **Default:** None  
- **Example:** `"AccurateQuote"`  

## **refundTickets**
The refund calculation for each of the passengers whose refund quote has been requested.

### **refundTickets[].firstName**
- **Type:** String  
- **Required:** Yes  
- **Description:** First name of the passenger requesting a refund.  
- **Constraints:** Alphabetic characters only.  
- **Default:** None  
- **Example:** `"SAN"`  

### **refundTickets[].lastName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Last name of the passenger requesting a refund.  
- **Constraints:** Alphabetic characters only.  
- **Default:** None  
- **Example:** `"ZHANG"`  

### **refundTickets[].ticketNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Ticket number received from the airline.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"S43484"`  

## **refundFareAmount**
The refund calculation for fl.

### **refundFareAmount.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency used for the refund calculations.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"USD"`  

### **refundFareAmount.originalFareAmount**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The original fare amount before refund calculations.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `200.00`  

### **refundFareAmount.estimatedRefundAmount**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The estimated refundable amount after deductions.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `150.00`  

### **refundFareAmount.displayOriginalFareAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** The original fare amount displayed in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `250.00`  

### **refundFareAmount.displayEstimatedRefundAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** The estimated refundable amount displayed in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `180.00`  

## **refundPostTicketingServiceAmounts**
The refund calculation for Post-ticketing Servrice, including baggage, seat, etc. Each post-ticketing order will be present as an object.

### **refundPostTicketingServiceAmounts[].postTicketingOrderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number for post-ticketing services such as baggage or seat selection.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"BAFAU20241220110246534"`  

### **refundPostTicketingServiceAmounts[].currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency for post-ticketing service calculations.  
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
- **Description:** The estimated refund amount for the post-ticketing service.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`  

### **refundPostTicketingServiceAmounts[].displayPostTicketingServiceAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** The original post-ticketing service amount displayed in the display currency.  
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
### **serviceFee.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency used for service fee calculations.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"USD"`  

### **serviceFee.transactionFee**
- **Type:** Number  
- **Required:** Yes  
- **Description:** The transaction fee applied to the refund.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `5.00`  

### **serviceFee.displayTransactionFee**
- **Type:** Number  
- **Required:** No  
- **Description:** The transaction fee displayed in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `5.50`


## **refundRules**
### **refundRules[].airline**
- **Type:** String  
- **Required:** No  
- **Description:** The airline associated with the refund rule.  
- **Constraints:** 2-letter IATA airline code.  
- **Default:** None  
- **Example:** `"LJ"`

## **passengerType**
- **Type:** String  
- **Required:** No  
- **Description:** Type of passenger for which the refund applies.  
- **Constraints:** Possible values: `ADT` (Adult), `CHD` (Child), `INF` (Infant).  
- **Default:** None  
- **Example:** `"ADT"`

### **refundRules[].refundReason**
- **Type:** String  
- **Required:** No  
- **Description:** The reason for the refund request.  
- **Constraints:** Predefined reason codes such as `0` (Involuntary), `1` (Voluntary), `4` (Void).  
- **Default:** None  
- **Example:** `"1"`  

### **refundRules[].penaltyAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** The penalty amount charged for the refund.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `480.00`  

### **refundRules[].penaltyPercent**
- **Type:** Number  
- **Required:** No  
- **Description:** The percentage penalty applied to the refund.  
- **Constraints:** Must be a positive number.  
- **Default:** `0.0`  
- **Example:** `0.0`  

### **refundRules[].penaltyPercentBase**
- **Type:** String or Null  
- **Required:** No  
- **Description:** The base amount on which the penalty percentage is applied.  
- **Constraints:** Can be `fare`, `fare+tax`.  
- **Default:** `null`  
- **Example:** `null`  

### **refundRules[].airlineFee**
- **Type:** Number  
- **Required:** No  
- **Description:** Additional airline fee for processing the refund.  
- **Constraints:** Positive number.  
- **Default:** `0.0`  
- **Example:** `0.0`  

### **refundRules[].taxRefundable**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Indicates whether the tax is refundable.  
- **Constraints:** `true` or `false`.  
- **Default:** None  
- **Example:** `true`  

### **refundRules[].fareRefundable**
- **Type:** Boolean  
- **Required:** No  
- **Description:** Indicates whether the fare is refundable.  
- **Constraints:** `true` or `false`.  
- **Default:** None  
- **Example:** `true`  

### **refundRules[].refundableAncillaries**
- **Type:** Array  
- **Required:** No  
- **Description:** List of refundable ancillary services, if any.  
- **Constraints:** Array of service identifiers or empty if none.  
  The options are:

	- StandardCheckInBaggage
	- CabinBaggage
	- CabinBaggageUnderSeat
	- CabinBaggageOverheadLocker
- **Default:** `[]`  
- **Example:** `[CabinBaggageUnderSeat]`  

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

## **cancelReason**
- **Type:** String  
- **Required:** No  
- **Description:** Reason for refund rejection.  
- **Constraints:** Predefined reasons such as:
  - Does not match airline policy.
  - No schedule change from the airline.
  - Non-refundable cancellation.
  - Voucher refund only.
  - Request canceled by user.
  - Travel already completed.
  - Refund not received from the airline yet.  
- **Default:** None  
- **Example:** `"Does not match airline policy."`  

## **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Status code of the request.  
- **Constraints:** `0`: Success, `2`: System error.  
- **Default:** None  
- **Example:** `0`  

## **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Error message describing the response.  
- **Constraints:** Should not be used to determine success or failure (use `status` instead).  
- **Default:** None  
- **Example:** `"Invalid request format."`

{% endtab %}

{% tab title="Samples" %}
```json
{
    "refundStatus": 0,
    "refundCode": "202408-0006",
    "cancelReason": "",
    "currency": "USD",
    "displayCurrency": "EUR",
    "refundQuoteType": "AccurateQuote",
        "refundTickets": [
        {
            "lastName": "ZHANG",
            "firstName": "SAN",
            "ticketNo": "S43484",
        }
    ],
   "refundPostTicketingServiceAmounts": [
        {
            "postTicketingOrderNo":"BAFAU20241220110246534"
            "currency": "USD",
            "originalPostTicketingServiceAmount": 141.19,
            "estimatedRefundAmount": 74.99,
            "displayPostTicketingServiceAmount": 241.19,
            "displayEstimatedRefundAmount": 74.99
        },
        {
            "postTicketingOrderNo":"BAFAU20241222111924553"
            "currency": "USD",
            "originalPostTicketingServiceAmount": 141.19,
            "estimatedRefundAmount": 74.99,
            "displayPostTicketingServiceAmount": 241.19,
            "displayEstimatedRefundAmount": 74.99
        }
    ],
   "refundAncillariesAmount": 
        {
            "currency": "USD",
            "originalAncillariesAmount": 141.19,
            "estimatedRefundAmount": 74.99,
            "displayOriginalAncillariesAmount": 241.19,
            "displayEstimatedRefundAmount": 74.99
        },
    "serviceFee": 
        {
            "currency": "USD",
            "transactionFee": 1.00,
            "displayTransactionFee": 1.50
        },
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
        "airlinePolicy": null,
        "ruleAccuracy": null,
        "atlasFulfillmentDuration": null,
        "airlineRefundDuration": null
    },
    "status": 0,
    "msg": null
}

```
{% endtab %}
{% endtabs %}
