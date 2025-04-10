# Make a Refund

### Dependency

Refund quotation function should be called in prior of this call

### Endpoint {% debug uid="refund_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/refund.do](https://sandbox.atriptech.com/refund.do)

## Request

{% tabs %}
{% tab title="Schema" %}

## **orderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Original order number. You can choose request orderNo or airlinePNR.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"ZNMKU20220119160129691"`  

## **airlinePNR**
- **Type:** String  
- **Required:** No  
- **Description:** The record locator of the airline. You can choose to requst either orderNo or airlinePNR.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"S24933"`  

## **carrier**
- **Type:** String  
- **Required:** No  
- **Description:** Airline carrier code.  
- **Constraints:** 2-letter airline code.  
- **Default:** None  
- **Example:** `"G9"`  

## **refundOfferId**
- **Type:** String  
- **Required:** No  
- **Description:** Get this from the refund quotation response. You can request with refundOfferId or refundRequest.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"7961ab5b202642628e9595498ffea083"`  

## **refundRequestList**
Ticket selection of the passengers and flights which is going to refund.

### **refundRequestList[].lastName**
- **Type:** String  
- **Required:** Yes  
- **Description:** Last name of the passenger requesting a refund.  
- **Constraints:** Alphabetic characters only.  
- **Default:** None  
- **Example:** `"ZHANG"`  

### **refundRequestList[].firstName**
- **Type:** String  
- **Required:** Yes  
- **Description:** First name of the passenger requesting a refund.  
- **Constraints:** Alphabetic characters only.  
- **Default:** None  
- **Example:** `"SAN"`  

### **refundRequestList[].segments**

#### **refundRequestList[].segments[].depDate**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure date of the segment which the passenger wants to refund.  
- **Constraints:** Format `YYYYMMDD`.  
- **Default:** None  
- **Example:** `"20240827"`  

#### **refundRequestList[].segments[].flightNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Flight number of the segment which the passenger wants to refund.  
- **Constraints:** Alphanumeric flight number.  
- **Default:** None  
- **Example:** `"LJ820"`  

#### **refundRequestList[].segments[].depAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** Departure airport of the segment which the passenger wants to refund.  
- **Constraints:** 3-letter airport code.  
- **Default:** None  
- **Example:** `"PVG"`  

#### **refundRequestList[].segments[].arrAirport**
- **Type:** String  
- **Required:** Yes  
- **Description:** Arrival airport of the segment which the passenger wants to refund.
- **Constraints:** 3-letter airport code.  
- **Default:** None  
- **Example:** `"CJU"`  

### **refundRequestList[].refundReason**
- **Type:** String  
- **Required:** Yes  
- **Description:** Code representing the reason for the refund request. 
- **Constraints:** Numeric string.  
	- 0: Involuntary
	- 1: Voluntary
	- 4: Void 
- **Default:** None  
- **Example:** `"1"`  

## **displayCurrency**
- **Type:** String  
- **Required:** No  
- **Description:** The alternative currency in which the fare and taxes amount needs to be displayed. The 3-letter currency code should be entered. The display currency requested when making a refund remains unchanged throughout the entire refund process.  
- **Constraints:** 3-letter ISO currency code.  
- **Default:** None  
- **Example:** `"EUR"`

{% endtab %}

{% tab title="Samples" %}
```json
{
    "orderNo": "ZNMKU20220119160129691",
    "airlinePNR":"S24933",
    "carrier":"G9",
    "refundOfferId":"7961ab5b202642628e9595498ffea083",
    "refundRequestList":[
        {
            "lastName":"ZHANG",
            "firstName":"SAN",
            "segments":[
                {
                    "depDate":"20240827",
                    "flightNo":"LJ820",
                    "depAirport":"PVG",
                    "arrAirport":"CJU"
                },
                {
                    "depDate":"20240828",
                    "flightNo":"LJ819",
                    "depAirport":"CJU",
                    "arrAirport":"PVG"
                }
                ],
            "refundReason":"1"
        }
     ]
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
- originalTotalFareAmount
- originalTotalAncillaryAmount
- originalTotalAmount
- airlinePenaltyAmountForFare
- airlinePenaltyAmountForAncillaries
- airlinePenaltyAmount
- estimatedRefundAmount
- transactionFee
- Journey
  
{% endhint %}

{% tabs %}
{% tab title="Schema" %}

## **refundStatus**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** The present status of the refund.  
- **Constraints:** Possible values:
	- `0`: Atlas Processing
	- `1`: Airline Processing (Submitted to airline by Atlas)
	- `2`: Refunded
	- `3`: Airline Refunding
	- `4`: Rejected
	- `5`: Fulfillment Done
	- `6`: Withdrew

If the ticket is paid by deposit: `0,1,2,3,4`

If the ticket is paid by VCC pass-through: `0,1,4,5,6`

`6` (Withdrew) is only used in refund claims.  
- **Default:** None  
- **Example:** `2`  

## **status**
- **Type:** Integer  
- **Required:** Yes  
- **Description:** Response status code.  
- **Constraints:** Possible values:
  - `0`: Success
  - `2`: System error  
- **Default:** None  
- **Example:** `0`  

## **msg**
- **Type:** String  
- **Required:** No  
- **Description:** Error message describing the response. Please do not use this field to check the success or failure of the request. Only use the ‘status’ code to check the result.  
- **Constraints:** None  
- **Default:** None  
- **Example:** `"Invalid request"`  

## **isRefundable**
- **Type:** Boolean  
- **Required:** Yes  
- **Description:** Indicates if the ticket is refundable.  
- **Constraints:** `true`: Refundable, `false`: Non-refundable.  
- **Default:** None  
- **Example:** `true`  

## **currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency used for fare and amounts.  
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

## **refundQuoteType**
- **Type:** String  
- **Required:** Yes  
- **Description:** Type of refund quote.  
- **Constraints:** Possible values:
  - `AccurateQuote`: Based on the calculated amount.
  - `CannotQuote`: Refund amount unknown, dependent on airline rates.
  - `NonRefundable`: The ticket is non-refundable.  
- **Default:** None  
- **Example:** `"AccurateQuote"`  

## **refundFareAmount**
The refund calculation for flight fare and inflow ancillaries.

### **refundFareAmount.currency**
- **Type:** String  
- **Required:** Yes  
- **Description:** Currency used for refund calculations.  
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
- **Description:** Estimated refundable amount.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`  

### **refundFareAmount.displayOriginalFareAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** Original fare amount in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `241.19`  

### **refundFareAmount.displayEstimatedRefundAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** Estimated refund amount in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`  

## **refundPostTicketingServiceAmounts**
The refund calculation for Post-ticketing Servrice, including baggage, seat, etc. Each post-ticketing order will be present as an object.

### **refundPostTicketingServiceAmounts[].postTicketingOrderNo**
- **Type:** String  
- **Required:** Yes  
- **Description:** Unique order number for post-ticketing services (e.g., baggage, seat selection).  
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
- **Description:** Original amount charged for the post-ticketing service.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `141.19`  

### **refundPostTicketingServiceAmounts[].estimatedRefundAmount**
- **Type:** Number  
- **Required:** Yes  
- **Description:** Estimated refund amount for the post-ticketing service.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`  

### **refundPostTicketingServiceAmounts[].displayPostTicketingServiceAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** Displayed original post-ticketing service amount in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `241.19`  

### **refundPostTicketingServiceAmounts[].displayEstimatedRefundAmount**
- **Type:** Number  
- **Required:** No  
- **Description:** Displayed estimated refund amount in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `74.99`


## **serviceFee**
Service fee of refund.

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
- **Description:** Transaction fee applied to the refund.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `1.00`  

### **serviceFee.displayTransactionFee**
- **Type:** Number  
- **Required:** No  
- **Description:** Transaction fee displayed in the display currency.  
- **Constraints:** Positive number.  
- **Default:** None  
- **Example:** `1.50`  

## **refundOfferId**
- **Type:** String  
- **Required:** Yes  
- **Description:** Refund offer ID used for future refund requests.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"7961ab5b202642628e9595498ffea083"`  

## **refundCode**
- **Type:** String  
- **Required:** Yes  
- **Description:** Refund order number generated for the request.  
- **Constraints:** Alphanumeric string.  
- **Default:** None  
- **Example:** `"R123456789"`  

## **cancelReason**
- **Type:** String  
- **Required:** No  
- **Description:** The reason for canceling the ticket or service.  
- **Constraints:** Predefined cancellation reason codes or free text depending on the system's requirements.  
The reason why the refund was cancelled.

- The cancel reasons are:
    -    Does not match airline policy
    -    There is no schedule change from the airline side. Please refer the ticket Fare Rules available in ATRIP flight deck for cancellation charges.
     untary Cancellation - Non-Refundable
    -    As per airline policy, only voucher refund is available for the ticket
    -    Refund request cancelled by the user
    -    Travel has been completed by the passenger
    -    Refund not yet received from the airline. Please try again later.
- **Default:** None  
- **Example:** `"Customer Request"`

## **refundReason**
- **Type:** Integer  
- **Required:** No  
- **Description:** Reason code for the refund.  
- **Constraints:** Possible values:
  - `0`: Involuntary
  - `1`: Voluntary
  - `4`: Void  
- **Default:** None  
- **Example:** `1`  
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
