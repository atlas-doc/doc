# Errors

Atlas uses standard [HTTP response codes](https://httpstatuses.com/) to indicate the success or failure of API requests.&#x20;

#### Status codes&#x20;

| Code                                 | Reason                                                 | Description                                                                                                                                                                                      |
| ------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| [200](https://httpstatuses.com/200)  | **Ok**                                                 | <p>The request was successful. </p><p> </p>                                                                                                                                                      |
| [201 ](https://httpstatuses.com/201) | <p><strong>Created</strong> </p><p> </p>               | <p>The request was successful, and a new resource was created. </p><p> </p>                                                                                                                      |
| [204](https://httpstatuses.com/204)  | <p><strong>No Content</strong> </p><p> </p>            | <p>The request was successful, but there is no response to send back. </p><p> </p>                                                                                                               |
| [400 ](https://httpstatuses.com/400) | <p><strong>Bad Request</strong> </p><p> </p>           | <p>The request was invalid, for example, due to missing headers. </p><p> </p>                                                                                                                    |
| [401 ](https://httpstatuses.com/401) | <p><strong>Unauthorized</strong> </p><p> </p>          | <p>An access token wasn't provided, or the provided token was invalid. </p><p> </p>                                                                                                              |
| [403](https://httpstatuses.com/403)  | <p><strong>Forbidden</strong> </p><p> </p>             | <p>A valid access token was provided, but it didn't have sufficient permissions. </p><p> </p>                                                                                                    |
| [404](https://httpstatuses.com/404)  | <p><strong>Not Found</strong> </p><p> </p>             | <p>The requested resource doesn't exist. </p><p> </p>                                                                                                                                            |
| [406](https://httpstatuses.com/406)  | <p><strong>Not Acceptable</strong> </p><p> </p>        | <p>The response type you requested with your Accept header isn't supported. </p><p> </p>                                                                                                         |
| [422](https://httpstatuses.com/422)  | <p><strong>Unprocessable Entity</strong> </p><p> </p>  | <p>A validation error occurred. </p><p> </p>                                                                                                                                                     |
| [429 ](https://httpstatuses.com/429) | <p><strong>Too Many Requests</strong> </p><p> </p>     | <p>You made too many requests to the API in a short period of time. </p><p> </p>                                                                                                                 |
| [500](https://httpstatuses.com/500)  | <p><strong>Internal Server Error</strong> </p><p> </p> | <p>Something went wrong on our side. Contact support or try again later. </p><p> </p>                                                                                                            |
| [502](https://httpstatuses.com/502)  | <p><strong>Bad Gateway</strong> </p><p> </p>           | <p>The server, while acting as a gateway or proxy, received an invalid response from an inbound server it accessed while attempting to fulfill the request. </p><p> </p>                         |
| [503](https://httpstatuses.com/503)  | <p><strong>Service Unavailable</strong> </p><p> </p>   | <p>The server is currently unable to handle the request due to a temporary overload or scheduled maintenance, which will likely be alleviated after some delay. Try again later. </p><p> </p>    |
| [504](https://httpstatuses.com/504)  | <p><strong>Gateway Timeout</strong> </p><p> </p>       | <p>The server, while acting as a gateway or proxy, did not receive a timely response from an upstream server it needed to access in order to complete the request. Try again later. </p><p> </p> |

#### Error codes

Atlas uses the following **Enum** to store the **error codes** and corresponding **error messages**.&#x20;

| Value   | Description                         |
| ------- | ----------------------------------- |
| **`1`** | Data check error                    |
| **`2`** | System error                        |
| **`3`** | Unauthorized access                 |
| **`4`** | Empty data error                    |
| **`5`** | Data encryption verification error  |
| **`6`** | Fare change error while booking     |

### &#x20;<a href="#status-codes" id="status-codes"></a>
