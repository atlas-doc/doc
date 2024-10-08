# Seat Availability

To get seats availability, characteristic and price.

### Dependency

Verify function should be called in prior to this call.

### Endpoint {% debug uid="seatAvailability_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/seatAvailability.do](https://sandbox.atriptech.com/seatAvailability.do)

## Request

{% tabs %}
{% tab title="Schema" %}
*   **sessionId **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

    Identifier of the search response.

{% endtab %}

{% tab title="Samples" %}
```json
{
    "sessionId": "eb3c94a7-ede4-4675-a7bb-a99ba1e10223"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   **segmentIndex **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Required**</mark>

    Flight segment for which seat map is returned.
*   **cabin **<mark style="color:blue;">**Array**</mark>**  **<mark style="color:green;">**Required**</mark>

    This is a list and will be repeated once for upper deck and once for the main deck when the requested cabin is spread across the upper and main deck.
*   **deck **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>

    “Upper deck”: Upper deck

    “Main”: Main deck (default)
*   **cabinType **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Cabin type

    Examples: First Class, Business Class
*   **cabinLayout **<mark style="color:blue;">**Array**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Cabin layout detail.
*   **columns **<mark style="color:blue;">**Object**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Contains columns and seat information for seat display purposes. Returns the characteristics for each column.
*   **designator **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>

    identify a seat column position on an aircraft

    **Example**: A,B,C,D,E,F
*   **characteristics **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Characteristics of column

    A: column by the aisle

    M: middle column

    W: column by the window
*   **rows **<mark style="color:blue;">**Array**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Contains rows and seat information for seat display purposes. Returns the starting end row position for each column.
*   **first **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>
    Contains rows and seat information for seat display purposes. Returns the starting end row position for each column.

    First row number

    **Example**: 20
*   **last **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>

    last row number

    **Example**: 43
*   **exitRowPosition **<mark style="color:blue;">**Array**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Returns the exit row information, if applicable. This must be returned regardless of whether exit row seats are open or are returned as valid seats.
*   **first **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Exit seat starting row position

    **Example**: 29
*   **last **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Exit seat ending row position

    **Example**: 30
*   **rows **<mark style="color:blue;">**Array**</mark>**  **<mark style="color:green;">**Required**</mark>

    Seat row, containing individual Seat instances.
*   **number **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Required**</mark>

    Seat row number.

    **Example**: 2
*   **seat **<mark style="color:blue;">**Array**</mark>**  **<mark style="color:green;">**Required**</mark>

    Seat column to identify a particular seat position on an aircraft.
*   **column **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Required**</mark>

    Seat column.

    **Example**: A
*   **seatStatus **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Required**</mark>

    Seat status

    F: Free

    O: Occupied
*   **seatCharacteristics **<mark style="color:blue;">**Array**</mark>**  **<mark style="color:green;">**Optional**</mark>

    Seat Characteristic

    E: Exit row seat

    I: Seat suitable for adult with an infant

    W: Window seat

    A: Aisle seat

    L: Leg space seat

    **Example**: refer to IATA definition from codeset 9825
*   **price **<mark style="color:blue;">**Decimal**</mark>**  **<mark style="color:green;">**Required**</mark>

    Price of the seat
*   **currency **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Required**</mark>

    Currency of the price.
*   **vendorPrice **<mark style="color:blue;">**Decimal**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The price charged by the vendor for the seat.
*   **vendorCurrency **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Optional**</mark>

    The currency in which your customers will do transaction with you.
*   **productCode **<mark style="color:blue;">**String**</mark>**  **<mark style="color:green;">**Required**</mark>

    Ancillary product code of seat, used in order

    **Example**: SCI_SEAT_C3_FR_KRK_LTN

{% endtab %}

{% tab title="Samples" %}
```json
{
  "segmentIndex": 1,
  "cabin": {
    "deck": "Mock",
    "cabinType": "Mock",
    "cabinLayout": {
      "columns": [
        {
          "designator": "A",
          "characteristics": "W"
        },
        {
          "designator": "B",
          "characteristics": "M"
        },
        {
          "designator": "C",
          "characteristics": "A"
        },
        {
          "designator": "D",
          "characteristics": "W"
        }
      ],
      "rows": {
        "first": 2,
        "last": 25
      },
      "exitRowPositions": null
    },
    "rows": [
      {
        "number": 2,
        "seats": [
          {
            "column": "A",
            "seatStatus": "F",
            "seatCharacteristics": [
              "L",
              "W",
              "I"
            ],
            "price": 13.25,
            "currency": "USD",
            "vendorPrice": 200.50025,
            "vendorCurrency": "PLN",
            "productCode": "SCI_SEAT_A2_FR_KRK_LTN"
          },
          {
            "column": "B",
            "seatStatus": "F",
            "seatCharacteristics": [
              "L",
              "W",
              "I"
            ],
            "price": 7.62,
            "currency": "USD",
            "vendorPrice": 115.331656,
            "vendorCurrency": "PLN",
            "productCode": "SCI_SEAT_B2_FR_KRK_LTN"
          },
          {
            "column": "C",
            "seatStatus": "F",
            "seatCharacteristics": [
              "L",
              "W",
              "I"
            ],
            "price": 4.15,
            "currency": "USD",
            "vendorPrice": 62.751688,
            "vendorCurrency": "PLN",
            "productCode": "SCI_SEAT_C2_FR_KRK_LTN"
          },
          {
            "column": "D",
            "seatStatus": "F",
            "seatCharacteristics": [
              "L",
              "W",
              "I"
            ],
            "price": 6.54,
            "currency": "USD",
            "vendorPrice": 98.900416,
            "vendorCurrency": "PLN",
            "productCode": "SCI_SEAT_D2_FR_KRK_LTN"
          }
        ]
      },
      {
        "number": 3,
        "seats": [
          {
            "column": "A",
            "seatStatus": "F",
            "seatCharacteristics": [
              "L",
              "W",
              "I"
            ],
            "price": 14.53,
            "currency": "USD",
            "vendorPrice": 219.86564,
            "vendorCurrency": "PLN",
            "productCode": "SCI_SEAT_A3_FR_KRK_LTN"
          },
          {
            "column": "B",
            "seatStatus": "F",
            "seatCharacteristics": [
              "L",
              "W",
              "I"
            ],
            "price": 22.95,
            "currency": "USD",
            "vendorPrice": 347.285994,
            "vendorCurrency": "PLN",
            "productCode": "SCI_SEAT_B3_FR_KRK_LTN"
          },
          {
            "column": "C",
            "seatStatus": "F",
            "seatCharacteristics": [
              "L",
              "W",
              "I"
            ],
            "price": 21.53,
            "currency": "USD",
            "vendorPrice": 325.729772,
            "vendorCurrency": "PLN",
            "productCode": "SCI_SEAT_C3_FR_KRK_LTN"
          },
          {
            "column": "D",
            "seatStatus": "F",
            "seatCharacteristics": [
              "L",
              "W",
              "I"
            ],
            "price": 18.43,
            "currency": "USD",
            "vendorPrice": 278.822494,
            "vendorCurrency": "PLN",
            "productCode": "SCI_SEAT_D3_FR_KRK_LTN"
          }
        ]
      }
    ]
  },
  "status": 0,
  "msg": "Success"
}
```
{% endtab %}
{% endtabs %}  
