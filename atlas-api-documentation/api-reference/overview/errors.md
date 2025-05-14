# Errors

Atlas uses the following **Enum** to store the **error codes** and corresponding **error messages**.

#### General Error Codes
| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">-1</mark> | Common error     |  | Atlas will investigate and add the relevant error code. |
| <mark style="color:blue;">100</mark> | Missing required request data     | Missing mandatory parameters. | Check the mandatory parameters. |
| <mark style="color:blue;">900</mark> | Unauthorized access | Incorrect credentials Or the account status is incorrect Or try to access other customer's data. | Check credentials. If the error still persists, contact your account manager. |
| <mark style="color:blue;">901</mark> |  illegal request data                               | Check the format of request. | The request format should be Json. |
| <mark style="color:blue;">902</mark>  |  Access denied   | Incorrect credentials Or the account status is incorrect Or you are trying to access other customer's data. | Check credentials. If the error still persists, contact your account manager. |
| <mark style="color:blue;">9999</mark> | System error                              |  This is unexpected error. | Atlas will investigate and add the relevant error code. |


#### Search Error Codes
| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">101</mark> | Illegal request data                         | Check the format of request. | The format should be Json. |
| <mark style="color:blue;">102</mark> | Illegal request param: {0}                           | Please check the messages below.  |  |
|  | The adult count should not be less than 1 | The adult count is "0". | Add an adult passenger type. |   
|  | Allow up to 9 passengers | The total number of passengers are more than 9. | Reduce the total number of passengers to a maximum of 9. | 
|  | Unknown city code | The city code is incorrect. | Check and correct the city code. | 
|  | The fromCity or fromAirport must not be empty | The destination from where the fare needs to be searched is empty. | Add the city or airport code. | 
|  | The toCity or toAirport must not be empty | The destination to where the fare needs to be searched is empty. | Add the city or airport code. | 
|  | The fromDate must not be empty | The travel start date is empty. | Add the travel start date. | 
|  | The retDate should not be empty | The return date is empty for a fare with tripType 2. | Add the return date. | 
|  | Invalid fromDate format | The date format is incorrect. | Change the format to YYYYMMDD. | 
| <mark style="color:blue;">103</mark> | Round-trip search is not supported                               | Only one-way itineraries can be searched. | Check with your account manager if there is a restriction to your account.|
| <mark style="color:blue;">104</mark> | Round-trip search is not allowed                               | Only one-way fares will be returned. A customer cannot use the tag "2) for "tripType" in search. | Check with your account manager if there is a restriction to your account. |
| <mark style="color:blue;">105</mark> | OD is not in client's round-trip white list                               |  This city pair has not been whitelisted. | Check with your account manager if there is a restriction to your account. |
| <mark style="color:blue;">106</mark> | Search is not allowed                               |  | Check with your account manager if there is a restriction to your account.|
| <mark style="color:blue;">107</mark> | Insufficient balance                               |  The account balance is below the agreed threshold. | Top-up your account on a priority. |
| <mark style="color:blue;">108</mark> | Route is restricted / System limitations   |  The airline has flights and quotations, but Atlas has closed sales for some reasons. The reasons can be 1) The sales were manually closed 2) The system has detected a risk of sold out 3) Prohibitions on nearby flights. | Try booking after some time. |
| <mark style="color:blue;">109</mark> | The number of searches exceeded the limit                               |  The searches per day have exceeded the allowed limit. | Check with your account manager if there is a restriction to your account. |
| <mark style="color:blue;">110</mark> | Too many concurrent requests                               | The QPS (Queries Per Second) is higher than the allowed limit. | If your business requires more resources, please contact your account manager. |
| <mark style="color:blue;">111</mark> | Real time search is not allowed                               | This feature is not activated for your account. | Connect with your account manager if you require this service. | 
| <mark style="color:blue;">112</mark> | Timed out                               | The search request has timed-out. | For further details please refer to FAQs --> Atlas API General Information. |
| <mark style="color:blue;">113</mark> | Airline is under maintenance                               | Airline is in "Inactive" or "Maintenance" status with Atlas. This does not necessarily mean that there is an issue with the Airline website itself. | Wait for the status to change to “active”. |
| <mark style="color:blue;">114</mark> | No flights present                               | "This may happen when: - The airline does not fly on that date for the searched city pair." | Check the airline website to see if the flight is operational for that date. |
| <mark style="color:blue;">115</mark> | Unexpected results                               |  System error. | Try again. If the error persists, raise a service request. | 
| <mark style="color:blue;">116</mark> | Search data not captured                             | An error was reported during the search data stoprage at Atlas' end. | If this error is not constantly reported, you can try trying again. If the error persists, then it is necessary to contact the account manager. |
| <mark style="color:blue;">123</mark> |  Too many requests but too few paid orders                     |  The service has been blocked as the search requests are too many and the paid orders are very less. | Ony search the required city pairs. |
| <mark style="color:blue;">124</mark> |  Unsupported settlement currency           |  The settlement currency is different than what is accepted by Atlas. | Change the currency to the currency accepted by Atlas for settlement. |
| <mark style="color:blue;">126</mark> |  requestId does not exist or has already ended.  |  An incorrect requestId has been used or the requestId is no longer valid. | Check the requestId or conduct a new Smart Search and use the new requestId. |
| <mark style="color:blue;">127</mark> |  Search timeout  |  The search has timed-out. | Conduct a new search. |


#### Verify Error Codes

| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">200</mark> | Illegal routing identifier                               |The "routingIdentifier" tag's information does not match the routing identifier received in the search response. | Check the routing identifier and resend the verification request with the correct “routingIdentifier”. |
| <mark style="color:blue;">201</mark> | Invalid routing                           | The airline has flights and quotations, but Atlas has closed sales for some reasons. The reasons can be 1) The sales were manually closed 2) The system has detected a risk of sold out 3) Prohibitions on nearby flights. | Try booking after some time. |
| <mark style="color:blue;">202</mark> | Routing identifier expired                           | The "routingIdentifier" has a validity of 6 hrs. If the “routingIdentifier” is used after this time period, then this error is displayed. | Conduct “Search” again and use the new “routingIdentifier”. |
| <mark style="color:blue;">203</mark> | Airline closed                |  The airline is no longer is business. |  |
| <mark style="color:blue;">205</mark> | Timed out           | There is a time-out set at Atlas’ end for the verify response. The verify response has taken a longer time. | For further details please refer to FAQs --> Atlas API General Information. |
| <mark style="color:blue;">206</mark> | No flights                         | The required flight cannot be found from the airline's side, possibly due to the flight being sold out. | Conduct the search again. |
| <mark style="color:blue;">207</mark> | The target flight does not exist                          | The required flight cannot be found from the airline's side, possibly due to the flight being sold out | Conduct the search again. |
| <mark style="color:blue;">208</mark> | Cabin changed        | Booking class changed. | Conduct the search again. |
| <mark style="color:blue;">209</mark> | Seat Strong Verify failed        | Seat verification during price verification has been enabled.  | Contact yopur account manager. |
| <mark style="color:blue;">210</mark> | Fare Family sold out | The flight or the fare family is no longer available with the airline. | Conduct the search again and rebook. |
| <mark style="color:blue;">211</mark> |  Flight or FareFamily not found |  The flight or the fare family is no longer available with the airline. | Conduct the search again and rebook. |
| <mark style="color:blue;">212</mark> | Illegal Request Parameter        |  Some parameter missing or additional. | Check the verify request. |
| <mark style="color:blue;">299</mark> | Verify failed | This is an error for which Atlas needs to take action. In some uncontrollable situations, such as network issues, upgrades, and restarts, 299 errors may occur. It is possible that the airline is not available or there are challenges at Atlas' end. Atlas needs to handle these errors internally. | Retry verification. If you get the same error, then start from search. If the error still persists, escalate to Atlas. |


#### Order Error Codes

| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">300</mark> | Invalid session information                | The "sessionID" is not the right one. | Check the session ID and enter the correct one. 
| <mark style="color:blue;">301</mark> | Session does not exist or timed out        | The "sessionID" has a validity of 2 hrs. If the “sessionID” is used after this time period, then this error is displayed | Check the session ID and enter the correct one. If the timeframe is over 2 hrs, then start from the verify stage (if less than 6 hrs. of verification response) |
| <mark style="color:blue;">302</mark> | The target flight does not exist           | "In the period between verify and book, the flight has been sold out. This can also be due to the number of passengers booked. The number of pax when booking and the number of pax when verifying may be different. When create a booking, the price is verified based on the actual number of pax booked. | Conduct the search again and rebook. |
| <mark style="color:blue;">303</mark> | Airline closed                             | Airline has either ceased to exist or not operational. |  |
| <mark style="color:blue;">304</mark> | Verify failed                              | In some uncontrollable situations, such as network issues, upgrades, and restarts, 304 error may occur, but not many. If there are many 304 errors, it is possible that the airline is not available or some technical issue at Atlas' end. | Contact your account manager if this error keeps on repeating. |
| <mark style="color:blue;">305</mark> | Invalid routing                            | When generating an order, the system found that the flight was no longer sold for various reasons, such as 1) L2B 2) The system has identified that there may be a risk of the flight being sold out 3) The airline's sales have been closed | Conduct the search again and rebook. |
| <mark style="color:blue;">306</mark> | Cabin changed                              | Booking class changed. | Conduct the search again. |
| <mark style="color:blue;">307</mark> | Illegal booking request parameters:        | One request parameter has a problem. Please check the message. | Check the error message. Correct the same and resubmit the booking. |
|                                      | passengers->name                           | The passenger name seems incorrect. | Check the passenger name, correct it and resubmit the booking. |
|                                      | passengers->passengerType                  | The passenger type is incorrect. | Check the passenger name, correct it and resubmit the booking. |
|                                      | passengers->birthday                       | The date of birth is in incorrect format or missing. | Correct the format and resubmit the booking. |
|                                      | passengers->gender                         | The gender is incorrect or missing. | Correct or add the information and resubmit the booking. |
|                                      | passengers->cardExpired                    | The identity card expiry date format is incorrect or missing. | Correct or add the information and resubmit the booking. |
|                                      | Additional baggage exceeds limit. Max allowed: 1 | The amount of ancillary baggage is more than the allowed limit. | Correct the baggage quantity and resubmit the booking. |
|                                      | Ancillaries not equal to the number of segments(inbound) | The number of segments and ancillaries do not match. | Check the ancillaries and segments and resubmit the booking. |
|                                      | XXX field not valid | The field is not correctly entered. | Check the field and resubmit the request. |
| <mark style="color:blue;">308</mark> | Price changed                              |   | Regenerate booking or create an entirely new booking. |
| <mark style="color:blue;">309</mark> | Ancillary not found                        | Incorrect ancillary product code has been entered. | Check and enter the correct ancillary product code. |
| <mark style="color:blue;">310</mark> | Infant not allowed                         |  | Create a new booking without infant passenger type. The infant passenger can be added “offline” via the airline website. |
| <mark style="color:blue;">311</mark> |  Seat Strong Verify failed                 | Check verify response for maximum seats allowed. | Adjust the passenger numbers as per the verification response and create a new booking. |
| <mark style="color:blue;">312</mark> | Too many seats booked                      | The number of pax booked exceeds the remaining (or allowed) seats on the current flight. | Rebook the itinerary. |
| <mark style="color:blue;">313</mark> | Fare family sold out                       |   | Create a new booking. |
| <mark style="color:blue;">314</mark> | Unable to regenerate order: The original order is ticketing or ticketed                         |  | Check the order with the same passenger and flight details. |
| <mark style="color:blue;">315</mark> | Not enough seats                           | Seats have been sold out | Rebook the itinerary |
| <mark style="color:blue;">316</mark> | Timed out                                  |  There is a time-out error at the airline’s end. Please check the FAQs (General Information) for more details regarding timeouts. | Rebook the itinerary. |
| <mark style="color:blue;">317</mark> | Booking unsuccessful with Airline          | An error has happened at the airline’s end. | Rebook the itinerary. |
| <mark style="color:blue;">318</mark> | Duplicate Booking                          |  | Check if a booking with the same passenger details and flight numbers exists. After confirming, ignore this booking.|
| <mark style="color:blue;">320</mark> | The requested seats were not found or they are already occupied.                      |  | Rebook seats and submit a new order.|
| <mark style="color:blue;">324</mark> | Airline system issues                    |  | Retry after some time. If the issue persists, please contact our operations team.|
| <mark style="color:blue;">326</mark> | Your account balance on the airline side is insufficient  | The deposit balance for the BYOA customer is invalid in the account held with the relevant airline. | Top-up the balance and then retry after the balance has been updated.|
| <mark style="color:blue;">327</mark> | Passenger information does not meet the requirements.  | All the mandatory requirements have not been fulfilled. | Check the booking requirements from the verfy response and ensure that all the requirements have been fulfilled.|
| <mark style="color:blue;">410</mark> | Use the correct format \"XXXX-XXXXXXXX\" for contact phone. Example: 0001-87291810, 0086-13928109091                         | Incorrect phone number format. | Check the phone number format and rectify the same.|
| <mark style="color:blue;">6051</mark> | The passenger is on government-imposed credit blacklist    | The passenger is on "No fly" list of the government. | Inform the passenger and cancel the order.|


#### Payment Error Codes
| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">400</mark> | Illegal request param                               | The request parameters are illegal, and the error scenarios include 1) Invalid VCC validity period 2) Lack of VCC cardholder information | Regenerate the existing order or create a new booking and update the VCC details. |
| <mark style="color:blue;">401</mark> | Time out of payment                          | Payment for the booking was initiated later than the payment deadline. The default payment deadline is 30 minutes after creating the order. | Regenerate the existing order or create a new booking. |
| <mark style="color:blue;">402</mark> | Order status does not support payment                        |  The order status maybe “ticketing” or “ticketed” where the payment has already been made. | Check if the order has been paid. If “yes”, do not send the payment request. |
| <mark style="color:blue;">403</mark> | Unsupported payment method               |  The payment method is not supported for this airline. | Change to an alternative payment method. |
| <mark style="color:blue;">404</mark> | The order is already paid            |  The order has already been paid. | Check if the order has been paid. If “yes”, do not send the payment request. |
| <mark style="color:blue;">405</mark> | Illegal transaction state            | The order status is not correct. | Check the order status and either regenerate the booking or ignore the request. |
| <mark style="color:blue;">406</mark> | Payment operation is in progress            |  The previous payment request is still in process. | Wait for the airline PNR to be received in the PNR details response. |
| <mark style="color:blue;">407</mark> | Some error messages indicating incorrect passenger information            | Some mandatory element for the passenger has not been submitted. | Check the information and correct the same and resubmit. |
| <mark style="color:blue;">408</mark> | Passenger can not board alone            | Only a child passenger is booked in this order. | Create a new order and add an adult passenger with the child passenger. |
| <mark style="color:blue;">409</mark> | Additional baggage does not match the flight segmemt            |  The “productCode” of the additional baggage does not match the product codes available for this flight. | Check the “productCode” and update it with the correct code. |
| <mark style="color:blue;">410</mark> | Use the correct format \"XXXX-XXXXXXXX\" for contact phone. Example: 0001-87291810, 0086-13928109091                        |  The contact information is not in the correct format. | Check the contact information and confirm that it matches the required format. |
| <mark style="color:blue;">411</mark> | Generic payment error          | The error happened when we checked your account. For example, “not enough balance”. | Check the balance or as per the message received in the error. |
| <mark style="color:blue;">413</mark> | Payment verification error      | Please check the messages below |  |
|  | Credit card pass through to the airline is not supported for this order.      | This order can't be paid with VCC. | Use Deposit to pay this order. |
|  | cardNumber must be 13 to 19 digits    | The cardNumber is incorrect. | Input the correct cardNumber. |
|  | Card number is invalid of luhn    | The cardNumber is incorrect. | Input the correct cardNumber. |
|  | Card is declined due to risk control.    | The card number is failed over 5 times in 30 minutes. | Please use another card to pay. |
|  | cardExpireMonth must be 1 to 2 digits.    | The cardExpiryMonth does not have the correct format. | Input the correct cardExpireMonth. |
|  | cardExpireYear must be 2 to 4 digits.    | The cardExpiryYear does not have the correct format. Example: 2025 or 25. | Input the correct cardExpireYear. |
|  | Invalid expiration date.    | The card Expire Date can't be less than today's date. | Input the correct cardExpire date. |
|  | cardCVV must be 3 to 4 digits.    | The CVV format is not correct. | Input the correct CVV. |
|  | cardHolderFirstName invalid characters in string.    |  | Only use A-Z、a-z、-、À-Ö、Ø-ö、ø-ÿ. |
|  | cardHolderLastName invalid characters in string.    |  | Only use A-Z、a-z、-、À-Ö、Ø-ö、ø-ÿ. |
|  | cardHolderCountry must be two letters long.    | If this field is not null, it must be two characters and in ISO 3166 format. | The card HolderCountry must in IOS 3166 format. |
|  | cardHolderCountry invalid ISO 3166 country code.    | If this field is not null, it cannot only use digits. | Input the correct cardHoldCountry. |
|  | cardHolderProvince must be two letters long.    | If this field is not null, it cannot only use digits. | Input the correct cardHolderProvince. |
|  | cardHolderCity cannot be purely numeric.    | If this field is not null, it can not be only numeric. | Input the correct cardHolderCity. |
|  | cardHolderPostCode can be only numeric or alphanumeric and must exceed 4 letters.    | If this field is not null, it must be only numeric or alphanumeric and must exceed 4 letters. | Input the correct cardHoldPostCode. |
|  | cardHolderAddress must exceed 6 characters in length.   | If this field is not null, it must exceed 6 characters in length | Input the correct cardHolderAddress. |


#### Seat Availability Codes

| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">214</mark> | Session ID invalid or expired                               | Session ID invalid or expired. | Send a new seat availability request |
| <mark style="color:blue;">216</mark> | Seat selection failed         | Fail to get seat availability information. | Try after some time. If the problem persists, please raise a service request. |
| <mark style="color:blue;">217</mark> | Unknown error         | Unknown error |  |  
| <mark style="color:blue;">218</mark> | The airline don’t support seat selection currently  | Seat selection is not available for this airline at the moment | Check with your account manager when seat availability will be supported for this airline |  

#### Ticket Error Codes

| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">601</mark> | Fare changed                               |  |  |
| <mark style="color:blue;">602</mark> | Flight not found                           | The flight is no longer available on the airlines platform. | Create a new booking. |
| <mark style="color:blue;">603</mark> | Flight sold out                            | The flight is sold out, and there are no available seats. This occurred after the payment was completed but before the ticket was issued. | Create a new booking. |
| <mark style="color:blue;">604</mark> | Pass-through card payment failed               | VCC not accepted by the airline. | Try a different card for payment. |
| <mark style="color:blue;">605</mark> | Incorrect passenger information            | The information in the "passengers" array is incorrect. | Check the passenger details and resubmit after correction. |  
| <mark style="color:blue;">606</mark> | Flight information updated          | Between search and book, the airline made a schedule change for the same flight number. | Start from search again. |
| <mark style="color:blue;">607</mark> | Seat sold out                       |  | Start from search again. |
| <mark style="color:blue;">608</mark> | Duplicate booking                          |  | Check if a booking with the same passenger details and flight numbers exists. After confirming, ignore this booking.|
| <mark style="color:blue;">609</mark> | Contact email is blocked by airline        |  Airline has blocked your email id as per their policy. | Create a new booking with a different email id OR provide authority to Atlas to use Atlas’ email id. Please refer to “Atlas API Order” FAQs for further details. |
| <mark style="color:blue;">611</mark> | PNR canceled or expired        |  The PNR has been cancelled by the airline or the payment exceeds the time-limit. | Start from search again. |
| <mark style="color:blue;">613</mark> | Rejected by Airline Risk Control | The airline has blocked the order as per their business rules. | Try making a payment with a different VCC. If the issue persists, due the "deposit" to make the payment. |
| <mark style="color:blue;">614</mark> | Wrong age | The age of the child passenger is not correct. | Check the age and resubmit the booking. |
| <mark style="color:blue;">615</mark> | Payment completed but failed to get the PNR number from the airline | Sometimes for the VCC payment, the airline fails to respond and hence the PNR is not received. In such a scenario, Atlas will deal with the airline manually and get the PNR and add it to the booking. |  |
| <mark style="color:blue;">616</mark> | 3DS Authetication |  The card used requires a 3DS authentication. Atlas does not support this feature at the moment. | Use a different card which does not have 3DS authentication OR pay via deposit mode of payment. |
| <mark style="color:blue;">617</mark> | Insufficient balance |  The deposit balance is below the minimum threshold. | Check your balance and top-up on a priority. |
| <mark style="color:blue;">618</mark> | Baggage weight cannot match with airline |  The weight of the baggage does not include one of the options which the airline has. | Check with the Atlas ops team |
| <mark style="color:blue;">619</mark> | Missing payment information |  Some information in the pay.do request is missing/incorrect. | Check the pay.do request and resubmit. |
| <mark style="color:blue;">620</mark> | Abnormal return fare type |  Roundtrip fares are limited to basic by the airline and cannot be combined with other fare types. | Book only one-way itineraries or create 1 booking per direction. |
| <mark style="color:blue;">621</mark> | Infant not supported |  Atlas does not suppport the "infant" passenger type for this airline. | Create a new booking without the infant passenger. |
| <mark style="color:blue;">623</mark> | Insufficient card balance/card consumption limit |  The VCC provided has insufficient balance/card consumption limit. | Please pay using a different VCC with sufficient card balance. |
| <mark style="color:blue;">624</mark> | Round trip is not supported temporarily |  Roundtrip functionality for this airline is currently not supported | Book 2 one way as separate orders. |
| <mark style="color:blue;">625</mark> | ffp Manual Issuance. | Frequent flyer is not supported and at the moment and can only be handled manually.  |  |
| <mark style="color:blue;">626</mark> | There are unpaid services in the current order. | The airline identied that there were unpaid transactions under this PNR, leading to subsequent business operations failure..  | Make payment for any unpaid orders |
| <mark style="color:blue;">627</mark> | The current order does not support post-ticketing ancillary purchase. | Post-ticketing ancillaries are not allowed for this order.  | Remove the ancillaries and create a new order. |
| <mark style="color:blue;">628</mark> | The flight information of the post-ticketing ancillary purchase order does not match the original flight. | The flight details are incorrect.  | Check the flight details and create a new order. |
| <mark style="color:blue;">631</mark> | Baggage fare changed. | The baggage price has changed at the time of fulfillment.  | Start the process from verify. |
| <mark style="color:blue;">632</mark> | Baggage fare changed. | Ticketing failed due to airline risk control.  | Start the process from verify. If the problem still exists please contact our operations team. |
| <mark style="color:blue;">633</mark> | Payment declined by airline. | Payment declined due to airline risk control.  | Use "deposit" as the payment mode and retry. |
| <mark style="color:blue;">634</mark> | Airline system issues                    |  | Create a new order. If the issue persists, please contact our operations team.|
| <mark style="color:blue;">699</mark> | System issues. |   | Retry after some time. If the issue persists, please contact support. |


#### Query Order Error Codes
| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">701</mark> | Multi-order are identified, please request again with extra parameters added     | More than 1 order having the same Record Locator has been identified. | Add the additional parameters and try again. |
| <mark style="color:blue;">702</mark> | airlinePNR and carrier are mandatory to fill in for order retrieval, please check and request again   | The record locator and the airline code are mandatory in the request. | Add the mentioned parameters and try again. |
| <mark style="color:blue;">703</mark> | No order found, please check the parameter   | The order number does not seem to be correct. | Check the order number and try again. |
| <mark style="color:blue;">704</mark> | Parameters don't match, please check and retry  | The parameters entered are not correct. | Check the parameters, correct them and try again. |
| <mark style="color:blue;">705</mark> | Timeout  | The response has timed-out | Try again after some time. If the issue persists, please contact support. |
| <mark style="color:blue;">800</mark> | Order does not exist                           | The relevant order does not exist. | Please re-check the order number and retry. |

#### Refund Quotation Error Codes
| Code | Description                    | Explanation                    | Solution                    |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">801</mark> | Order does not exist              | Incorrect order number has been entered. | Check the order number and enter the correct one. |
| <mark style="color:blue;">802</mark> | Children cannot travel alone     | Only ADT pax cannot be refunded. The CHD pax should also be refunded together. | Request refund for the full order including child passenger. |
| <mark style="color:blue;">803</mark> | The passengers have already submitted a refund for a pax and/or segment | Incorrect order number has been entered. | Check the order number and enter the correct one. |
| <mark style="color:blue;">807</mark> | Passenger does not exist. | Incorrect passenger name has been entered. | Check the passenger name and correct the same, if required. |
| <mark style="color:blue;">809</mark> | Order not ticketed.  | The ticket issuance for this order is under process or the payment has not been made. | Wait for the order to be ticketed or make a payment for this order. | 
| <mark style="color:blue;">810</mark> | Illegal request param: xxx | One of the request parameters is incorrect. | Check the request and correct the required parameter.  | 
| <mark style="color:blue;">811</mark> | Completed itineraries are not entered. Please enter the full itinerary and retry. | This can happen due to a variety of reasons. | Check if any of the scenarios listed below are applicable and take relevant action. | 
|  |     | For a roundtrip itinerary, the full ticket needs to be refunded. | If the ticket is fully unused, please enter details of the whole itinerary and retry.  | 
|  |     | For connecting flights, both the segments need to be refunded together. | Check if both the segments are available in the request and retry.  | 
|  |     | One sector has been flown in the journey. | Check with the airline. Atlas does not support the refund for "partially" flown itineraries. | 
| <mark style="color:blue;">812</mark> | Unable to match pax xxx with order. | The name of the passenger does not match with the order. | Check the rpassenger name and resubmit the request.|
| <mark style="color:blue;">815</mark> | Ticket not found. |  | Check the ticket number and retry.|
| <mark style="color:blue;">824</mark> | Refund not supported for ancillary orders. Please provide the original order number. | Only the main order is allowed for refund. | Check and confirm whether the order number is of the original order.|
| <mark style="color:blue;">902</mark> | Access denied.|  |  |
| <mark style="color:blue;">8041</mark> | Segment does not exist. | One of the segments in the request does not exist. | Check the segments and only provide the segments for that refund request.| 


#### Refund Submission Error Codes
| Code | Description                    | Explanation                    | Solution                    |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">801</mark> | Order does not exist              | Incorrect order number has been entered. | Check the order number and enter the correct one. |
| <mark style="color:blue;">802</mark> | Children cannot travel alone     | Only ADT pax cannot be refunded. The CHD pax should also be refunded together. | Request refund for the full order including child passenger. |
| <mark style="color:blue;">803</mark> | The passengers have already submitted a refund for a pax and/or segment | Incorrect order number has been entered. | Check the order number and enter the correct one. |
| <mark style="color:blue;">805</mark> | RefundOfferId has expired. | The “refundOfferId” has expired. | Send a new refund request to get the latest “refundOfferId”. |
| <mark style="color:blue;">807</mark> | Passenger does not exist. | Incorrect passenger name has been entered. | Check the passenger name and correct the same, if required. |
| <mark style="color:blue;">809</mark> | Order not ticketed.  | The ticket issuance for this order is under process or the payment has not been made. | Wait for the order to be ticketed or make a payment for this order. | 
| <mark style="color:blue;">810</mark> | Illegal request param: xxx | One of the request parameters is incorrect. | Check the request and correct the required parameter.  | 
| <mark style="color:blue;">811</mark> | Completed itineraries are not entered. Please enter the full itinerary and retry. | This can happen due to a variety of reasons. | Check if any of the scenarios listed below are applicable and take relevant action. | 
|  |     | For a roundtrip itinerary, the full ticket needs to be refunded. | If the ticket is fully unused, please enter details of the whole itinerary and retry.  | 
|  |     | For connecting flights, both the segments need to be refunded together. | Check if both the segments are available in the request and retry.  | 
|  |     | One sector has been flown in the journey. | Check with the airline. Atlas does not support the refund for "partially" flown itineraries. | 
| <mark style="color:blue;">812</mark> | Unable to match pax xxx with order. | The name of the passenger does not match with the order. | Check the rpassenger name and resubmit the request.|
| <mark style="color:blue;">814</mark> | The refund submission is in progress. Please wait. | The refund process is in progress. Please wait for some time. | Retry after some time. If the problem keeps on repeating, please contact your account manager.|
| <mark style="color:blue;">815</mark> | Ticket not found. |  | Check the ticket number and retry.|
| <mark style="color:blue;">816</mark> | Refund request already submitted.| The refund request has already been submitted. | No action required. You may check the refund status using the queryRefundOrders.do API request. | 
| <mark style="color:blue;">817</mark> | Atlas refund applied.| The refund request has already been submitted. | No action required. You may check the refund status using the queryRefundOrders.do API request. | 
| <mark style="color:blue;">818</mark> | Refund claim applied.| The refund claim has already been submitted. | No action required. You may check the refund status using the queryRefundOrders.do API request. | 
| <mark style="color:blue;">820</mark> | Ticket status is used.| The sector has already been flown. | Check is the sector has been flown. Contact our ops team if the sector has not been flown. |
| <mark style="color:blue;">821</mark> | Exceed the ticket refund deadline.| The refund submission has been done after the refund deadline. | Contact our ops team if you have any questions. |
| <mark style="color:blue;">822</mark> | Exceed the ticket void deadline.| The void submission has been done after the deadline. | Contact our ops team if you have any questions. |
| <mark style="color:blue;">823</mark> | Void not all pax.|  |  |
| <mark style="color:blue;">824</mark> | Refund not supported for ancillary orders. Please provide the original order number. | Only the main order is allowed for refund. | Check and confirm whether the order number is of the original order.|
| <mark style="color:blue;">902</mark> | Access denied.|  |  |
| <mark style="color:blue;">905</mark> | Submission is too frequent, please try again later.|  |  |
| <mark style="color:blue;">8041</mark> | Segment does not exist. | One of the segments in the request does not exist. | Check the segments and only provide the segments for that refund request.| 


#### Refund Query Error Codes
| Code | Description                    | Explanation                    | Solution                    |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">801</mark> | Order does not exist              | Incorrect order number has been entered. | Check the order number and enter the correct one. |
| <mark style="color:blue;">810</mark> | Illegal request param: xxx | One of the request parameters is incorrect. | Check the request and correct the required parameter.  | 
| <mark style="color:blue;">902</mark> | Access denied.|  |  |

#### Post-booking Ancillary Search Error Codes
| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">117</mark> | Baggage is not allowed for this order as it is not in the ticketed status           |  The ticket has still not been issued. | Wait for the status to changhe to "ticketed" and then search for ancillary.|
| <mark style="color:blue;">118</mark> | Atlas currently does not support seat or baggage for this airline         |   | Check with the airline for ancillary baggage or open a Service Request with Atlas for the same.|
| <mark style="color:blue;">119</mark> | Baggage or seat selection is not supported for orders with infants         |  There is an infant passenger in the booking. | Book ancillary baggage directly with the airline or open a Service Request with Atlas for the same|
| <mark style="color:blue;">120</mark> | Baggage or seat selection for the flight has been closed        |  The airline no longer accepts the addition for ancillary for that flight. | Check with the airline or open a Service Request with Atlas for the same.| 


#### Post-booking Ancillary Order Error Codes
| Code | Description                    | Explanation                    | Solution                     |
| ---- | ------------------------------ | ------------------------------ | ------------------------------ |
| <mark style="color:blue;">501</mark> | Add purchase not allowed       |  Ancillary addition is not allowed for this order. | Check with the airline or open a Service Request with Atlas for the same.|
| <mark style="color:blue;">502</mark> | The price has increased, and the order creation has failed. Please perform a new search.      |  There is a price change from the time the ancillary order search was conducted. | Search ancillary order again.|
| <mark style="color:blue;">503</mark> | Incorrect baggage selection    | Please check the messages below. | |
|  | Adding the same type of baggage repeatedly.    | Each passenger can only select one baggage per segment. | Remove duplicate baggage of the same type. |
|  | Baggage for different segments of an itinerary is inconsistent.   | For some airlines in each itinerary, the baggage for each segment must be the same. | Make the baggage for each segment in this itinerary consistent. |
|  | Product code does not match the segment search results.   | The product code must match the segment search results. | Use the correct product code from the search results. |
| <mark style="color:blue;">504</mark> | Additional baggage not allowed. Ancillary baggage already exists in the original order |  Atlas only allows the attachment of ancillary baggage only once | Book ancillary baggage directly with the airline or open a Service Request with Atlas for the same |
| <mark style="color:blue;">505</mark> | Additional baggage not allowed. Baggage already booked as post-ticket ancillary. |  Atlas only allows the attachment of ancillary baggage only once | Book ancillary baggage directly with the airline or open a Service Request with Atlas for the same |
| <mark style="color:blue;">506</mark> | Seat selection is not supported for orders with infants |  There is an infant passenger in the booking. | Book ancillary baggage or seat directly with the airline or open a Service Request with Atlas for the same|


## Error Samples

### 214：Session ID invalid or expired

### Request：
```
{
    "sessionId": "49871954-6aaa-44fa-b768-1a590d21be08"
}
```

### Response:
```
{
    "cabins": null,
    "status": 214,
    "msg": "Session ID invalid or expired"
}
```

### 216: Seat selection failed

### Request：
```
{
    "mockError": "mockSeatError", 
    "sessionId": "31f1c47c-1fbb-4cfd-8620-49e73ab26f60"
}
```

### Response:
```
{
    "cabins": null,
    "status": 216,
    "msg": "Seat selection failed"
}
```

### 217: Unknown error

System fallback exception, which is typically not triggered

### Response:
```
{
    "cabins": null,
    "status": 217,
    "msg": "Unknown error"
}
```
