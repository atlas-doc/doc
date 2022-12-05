# Errors

Atlas uses the following **Enum** to store the **error codes** and corresponding **error messages**.

#### General Error codes

| Value   | Description                         |
| ------- | ----------------------------------- |
| <mark style="color:blue;">1</mark> | Data check error                    |
| <mark style="color:blue;">2</mark>  | System error                        |
| <mark style="color:blue;">3</mark>  | Unauthorized access                 |
| <mark style="color:blue;">4</mark>  | Empty data error                    |
| <mark style="color:blue;">5</mark>  | Data encryption verification error  |
| <mark style="color:blue;">900</mark> | Unauthorized access                        |
| <mark style="color:blue;">9999</mark> | System error                              |


#### Search error codes
| Code                                 | Description                                |
| ------------------------------------ | ------------------------------------------ |
| <mark style="color:blue;">100</mark> | Missing required request data                               |
| <mark style="color:blue;">101</mark> | Illegal request data                         |
| <mark style="color:blue;">102</mark> | Illegal request param: {0}                           | 
| <mark style="color:blue;">103</mark> | Round-trip search is not supported                               |
| <mark style="color:blue;">104</mark> | Round-trip search is not allowed                               |
| <mark style="color:blue;">105</mark> | OD is not in client's round-trip white list                               |
| <mark style="color:blue;">106</mark> | Search is not allowed                               |
| <mark style="color:blue;">107</mark> | Insufficient balance                               |
| <mark style="color:blue;">108</mark> | Route is restricted                               |
| <mark style="color:blue;">109</mark> | The number of searches exceeded the limit                               |
| <mark style="color:blue;">900</mark> | Unauthorized access                              |


#### Verify error codes

| Code                                 | Description                                |
| ------------------------------------ | ------------------------------------------ |
| <mark style="color:blue;">200</mark> | Illegal routing identifier                               |
| <mark style="color:blue;">201</mark> | Invalid routing                           |
| <mark style="color:blue;">202</mark> | Routing identifier expired                           |
| <mark style="color:blue;">203</mark> | Airline closed                |
| <mark style="color:blue;">204</mark> | The airline does not support the current interface           |
| <mark style="color:blue;">205</mark> | Timed out           |
| <mark style="color:blue;">206</mark> | No flights                         |
| <mark style="color:blue;">207</mark> | The target flight does not exist                          |
| <mark style="color:blue;">208</mark> | Cabin changed        |
| <mark style="color:blue;">299</mark> | Verify failed |

#### Order error codes

| Code                                 | Description                                |
| ------------------------------------ | ------------------------------------------ |
| <mark style="color:blue;">300</mark> | Invalid session information                |
| <mark style="color:blue;">301</mark> | Session does not exist or timed out        |
| <mark style="color:blue;">302</mark> | The target flight does not exist           |
| <mark style="color:blue;">303</mark> | Airline closed                             |
| <mark style="color:blue;">304</mark> | Verify failed                              |
| <mark style="color:blue;">305</mark> | Invalid routing                            |
| <mark style="color:blue;">306</mark> | Cabin changed                              |
| <mark style="color:blue;">307</mark> | Illegal request parameters                 |
| <mark style="color:blue;">308</mark> | Price changed                              |
| <mark style="color:blue;">309</mark> | Ancillary not found                        |

#### Payment  error codes
| Code                                 | Description                                |
| ------------------------------------ | ------------------------------------------ |
| <mark style="color:blue;">400</mark> | Illegal request param                               |
| <mark style="color:blue;">401</mark> | Time out of payment                          |
| <mark style="color:blue;">402</mark> | Order status does not support payment                        |
| <mark style="color:blue;">403</mark> | Unsupported payment method               |
| <mark style="color:blue;">404</mark> | The order is already paid            |
| <mark style="color:blue;">405</mark> | Illegal transaction state            |
| <mark style="color:blue;">406</mark> | Payment operation is in progress            |
| <mark style="color:blue;">407</mark> | Pax info invalid            |
| <mark style="color:blue;">408</mark> | Passenger can not board alone            |
| <mark style="color:blue;">409</mark> | Additional baggage does not match the flight segmemt            |
| <mark style="color:blue;">800</mark> | Order not exists:            |
| <mark style="color:blue;">900</mark> | Unauthorized access            |

#### Ticket error codes

| Code                                 | Description                                |
| ------------------------------------ | ------------------------------------------ |
| <mark style="color:blue;">601</mark> | Price change                               |
| <mark style="color:blue;">602</mark> | Flight not found                           |
| <mark style="color:blue;">603</mark> | Flight sold out                           |
| <mark style="color:blue;">604</mark> | Payment declined by airline                |
| <mark style="color:blue;">605</mark> | Incorrect passenger information            |
| <mark style="color:blue;">606</mark> | Inconsistent flight information            |
| <mark style="color:blue;">607</mark> | Fare not available                         |
| <mark style="color:blue;">608</mark> | Duplicate booking                          |
| <mark style="color:blue;">609</mark> | Contact email is blocked by airline        |
| <mark style="color:blue;">610</mark> | Error happened during payment with airline |
| <mark style="color:blue;">614</mark> | Wrong age |
| <mark style="color:blue;">615</mark> | Payment completed but failed to get the PNR number from the airline |
| <mark style="color:blue;">616</mark> | 3DS Authetication |
| <mark style="color:blue;">617</mark> | Insufficient balance |
| <mark style="color:blue;">698</mark> | Technical error on the airline side - !!! PAYMENT STATUS UNKNOWN !!! - PLEASE CONTACT THE AIRLINE BEFORE TRYING TO BOOK AGAIN.|
| <mark style="color:blue;">699</mark> | Unknown error                              |




#### Query order error codes
| Code                                 | Description                                |
| ------------------------------------ | ------------------------------------------ |
| <mark style="color:blue;">800</mark> | Order does not exist                           |
