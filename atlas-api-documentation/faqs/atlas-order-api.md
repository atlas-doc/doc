# Atlas Order API

**Does the `OrderAPI` hold the inventory? If yes, then for how long?**

We allow you to hold the inventory and guarantee the price for 30 mins after an order is generated. If the payment is not made during these 30 minutes, the price guarantee is void.



**Can we release the inventory which is on hold at our end?**

The Atlas API holds the inventory after the `OrderAPI` calls. We have a built-in mechanism to release the inventory after 30 minutes have passed. Different airlines have different mechanisms to release inventory; hence we cannot provide partner agencies with a function to request the release of inventory.



**Can we use our VCC to book a round-trip itinerary created by 2 one-way fares?**

Atlas uses 2 one-way fares to construct round-trip journeys when 2 one-way fares are cheaper than a real round-trip. When our customers use VCC for their bookings, it is their intent to use the same for the return journeys constructed using 2 one-way fares also.

This can be achieved with the below process:

The element 'allowGenerateMultipleOrders' has been added to the "order.do" request.

**`allowGenerateMultipleOrders`  **<mark style="color:blue;">**boolean**</mark>**  **<mark style="color:green;">**Optional**</mark>

true: Allow

false: Not allowed (default)

When the "allowGenerateMultipleOrders= true" element is sent in the "order.do" request for roundtrip bookings, the workflow will be as below: 

-	Atlas will check if we can also issue a roundtrip fare for this booking. If yes, then we will follow the already existing workflow and logic to give you the response.

-	If we CANNOT issue a roundtrip for this booking, then we will generate two orders for you, with the 'orderNo' format as "TBASA20220123212500763, KYASA20220123212500764". Please use comma to split the order number.


The "queryOrderDetails" function can be called to get the details of each booking. The "supportCreditTransPayment" tag can still be checked to identify if this new booking accepts credit card or not.

**`supportCreditTransPayment`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

1: Prepayment Only

3: Both Credit Card Payment and Prepayment Available

When the customer finishes the payment at your end, you can call pay function for both orders (one call for each) to finish the payment to Atlas and waiting for the ticket to be issued.

The flow will be as below:

Order

Then, 
Retrieve booking1 --> Payment1

Retrieve booking2 --> Payment2


{% tabs %}
{% tab title="Request Sample" %}
```

{
    "cid": "tviin65428",
    
    "sessionId": "baea976c-b5cb-4374-9a21-3adddf39c854",
    
    "passengers": [
    
        {
            "name": "shao/tingjun",
            "passengerType": 0,
            "birthday": "19910105",
            "gender": "M",
            "cardNum": "330226199101051272",
            "cardType": "PP",
            "cardIssuePlace": "CN",
            "cardExpired": "20220413",
            "nationality": "CN"
        }
        
    ],
    "contact": {
        "name": "tingjunshao",
        "address": "",
        "postcode": "",
        "email": "490743607@qq.com",
        "mobile": "+8615951711432"
    },
    "useAtlasMailForContact": true,
    "allowGenerateMultipleOrders": true
}

{% endtab %}

{% tab title="Response Sample" %}
```

{
  "sessionId": "9695381e-760b-4bc7-acef-2f7ffce046d5",
  "orderNo": "TESTX20230224163206133,TESTX20230224163206137",
  "originalOrderNo": null,
  "totalPrice": 81.66,
  "totalTransactionFee": 1,
  "currency": "USD",
  "vendorTotalPrice": 8.7,
  "vendorCurrency": "SGD",
  "tktLimitTime": "2023-02-24 17:22:06",
  "pnrCode": "WACAF8,SJCY7D",
  "includeExtraBaggage": 0,
  "paxTicketInfos": [
    {
      "name": "ZHANG/SAN",
      "passengerType": 0,
      "birthday": "19801001",
      "gender": "M",
      "cardNum": "G88888888",
      "cardType": "PP",
      "cardIssuePlace": "CN",
      "cardExpired": "20251001",
      "nationality": "CN",
      "ticketNos": [],
      "airlinePNRs": [],
      "contactEmails": [
        "ZoilaGladue1616@ttjipiao.top"
      ],
      "contactPhones": [
        "0065-81234567"
      ],
      "ancillaries": []
    }
  ],
  "routing": {
    "fid": "Wpa27CBEACqzJq2noy5mHNHfzcJpEGHuVk8I9yfG1ssgNapRQGMCthp9lWtbgddgC85qVLQ-ayM0r0TJ0vzUoMp2aSpLSsAtCI7uC9xQ8-M.",
    "routingIdentifier": "+tqbEsi/1kObovhnSCODSj6gwCTZ+MubvbYh0AEnwFXE9wBPJq8cqfA1+JNMdrF0i6VkoDVmwvar2v2xjaZystvQ7Zy3XpyhTgojXFaRotLPYGBY4KX2gjyhSySssiAH+YMRS4HjlUJ9f2gixGd9JGcFdXYWPbUlSP9MCgy4VAHJxQeak35HxJPHwT8Nz2fjnW8FDmJD0y/j3aeC8bAOb+HngD2xPHBELkSFtpjRAtQwfce9McFFnwOTpavLsxodWAuMOfPt4AXxrRnqVc5OlNI4x1A0P4iiKWG281qtD+O/Rd9YVOspxBzn8cfuq+jicrjCePXCWiAzFQQ39o8wUbeORaFYcLyhXUD6DlDqLk1gJJdqF9B7zz/6kh+QHqwRiD92Dvfu0ngaasgxb0MBKxPwE15OtszuX8EzDUK3Jf93Oi6BAq1BKLCTAqwOtP4ApvLhkjinEuXGLtHBwzN4w7e2GvPwILle2F1vbf2/qBU=",
    "supportCreditTransPayment": "0",
    "currency": "USD",
    "adultPrice": 81.06,
    "adultTax": 0.6,
    "childPrice": 81.06,
    "childTax": 0.6,
    "infantPrice": 42.04,
    "infantTax": 0,
    "infantAllowed": true,
    "transactionFeePerPax": 1,
    "transactionFee": 1,
    "transactionFeeMode": "PER_PAX",
    "nationalityType": 0,
    "nationality": "",
    "suitAge": "",
    "PaxType": "ADT",
    "fromSegments": [
      {
        "carrier": "JT",
        "flightNumber": "JT929",
        "depAirport": "DPS",
        "depTime": "202303090700",
        "arrAirport": "SUB",
        "arrTime": "202303090655",
        "stopCities": "",
        "duration": 55,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 4,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "Economy"
      }
    ],
    "retSegments": [
      {
        "carrier": "JT",
        "flightNumber": "JT920",
        "depAirport": "SUB",
        "depTime": "202303141625",
        "arrAirport": "DPS",
        "arrTime": "202303141820",
        "stopCities": "",
        "duration": 55,
        "codeShare": false,
        "cabin": "",
        "cabinClass": 1,
        "seatCount": 4,
        "aircraftCode": "",
        "depTerminal": "",
        "arrTerminal": "",
        "operatingCarrier": "",
        "operatingFlightnumber": "",
        "fareFamily": "Economy"
      }
    ],
    "combineIndexs": [],
    "rule": {
      "hasBaggage": 1,
      "baggageElements": [
        {
          "segmentNo": 1,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 20
        },
        {
          "segmentNo": 2,
          "baggageType": "StandardCheckInBaggage",
          "passengerType": 0,
          "baggagePiece": 0,
          "baggageWeight": 20
        }
      ],
      "refundRules": [
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "CNY",
          "refNoshow": "T",
          "refNoShowCondition": 48,
          "refNoshowFee": 0,
          "ruleList": [
            {
              "rowId": 1,
              "gmtCreate": "Jun 28, 2021 12:29:21 AM",
              "gmtModified": "Jun 28, 2021 12:29:21 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "JT",
              "ruleType": "self_refund",
              "ruleName": "self_refund_JT_1_RwN0uI",
              "ruleKey": "self_refund_JT_202106280829211",
              "priority": 10,
              "validBeginTime": "Oct 7, 2019 4:00:00 PM",
              "validEndTime": "Jun 9, 2333 3:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": "",
              "arrCountry": "",
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": null,
              "timeRight": 100,
              "ruleExtend": {
                "ruleKey": "self_refund_JT_202106280829211",
                "canRefund": "Y",
                "canChange": null,
                "canRefundTax": "N",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": 100,
                "amountCurrency": "SGD",
                "pricePercent": null,
                "priceItem": null,
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            }
          ]
        },
        {
          "refundType": 0,
          "refundStatus": "T",
          "refundFee": 0,
          "currency": "CNY",
          "refNoshow": "T",
          "refNoShowCondition": 48,
          "refNoshowFee": 0,
          "ruleList": [
            {
              "rowId": 1,
              "gmtCreate": "Jun 28, 2021 12:29:21 AM",
              "gmtModified": "Jun 28, 2021 12:29:21 AM",
              "creator": null,
              "modifier": null,
              "isDeleted": "N",
              "airline": "JT",
              "ruleType": "self_refund",
              "ruleName": "self_refund_JT_1_RwN0uI",
              "ruleKey": "self_refund_JT_202106280829211",
              "priority": 10,
              "validBeginTime": "Oct 7, 2019 4:00:00 PM",
              "validEndTime": "Jun 9, 2333 3:59:59 PM",
              "depCity": null,
              "arrCity": null,
              "depCountry": "",
              "arrCountry": "",
              "bookingCode": null,
              "fareFamily": null,
              "cabinClass": null,
              "timingMode": "depTime",
              "timeLeft": null,
              "timeRight": 100,
              "ruleExtend": {
                "ruleKey": "self_refund_JT_202106280829211",
                "canRefund": "Y",
                "canChange": null,
                "canRefundTax": "N",
                "canRefundPkg": null,
                "canRefundCoupon": null,
                "canMakeUpDiff": null,
                "canNoShowRefund": null,
                "amount": 100,
                "amountCurrency": "SGD",
                "pricePercent": null,
                "priceItem": null,
                "taxItem": null,
                "charge": null,
                "chargeCurrency": null,
                "canExemptSameDay": null,
                "exemptDuration": null,
                "ticketBeginTime": null,
                "ticketEndTime": null,
                "applyBeginTime": null,
                "applyEndTime": null,
                "travelBeginTime": null,
                "travelEndTime": null
              }
            }
          ]
        }
      ],
      "changesRules": [
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "CNY",
          "revNoshow": "T",
          "revNoShowCondition": 48,
          "revNoshowFee": 0,
          "ruleList": []
        },
        {
          "changesType": 0,
          "changesStatus": "T",
          "changesFee": 0,
          "currency": "CNY",
          "revNoshow": "T",
          "revNoShowCondition": 48,
          "revNoshowFee": 0,
          "ruleList": []
        }
      ]
    },
    "ancillaryProductElements": [
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_10KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 12.64,
        "currency": "USD",
        "vendorPrice": 16.89,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 10,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_10KG"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_15KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 17.96,
        "currency": "USD",
        "vendorPrice": 24.01,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 15,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_15KG"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 23.29,
        "currency": "USD",
        "vendorPrice": 31.12,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 20,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_20KG"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_25KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 28.61,
        "currency": "USD",
        "vendorPrice": 38.23,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 25,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_25KG"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_30KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 33.93,
        "currency": "USD",
        "vendorPrice": 45.34,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 30,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_30KG"
      },
      {
        "segmentIndex": 1,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_5KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 7.32,
        "currency": "USD",
        "vendorPrice": 9.78,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 5,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_5KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_10KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 12.64,
        "currency": "USD",
        "vendorPrice": 16.89,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 10,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_10KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_15KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 17.96,
        "currency": "USD",
        "vendorPrice": 24.01,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 15,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_15KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_20KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 23.29,
        "currency": "USD",
        "vendorPrice": 31.12,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 20,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_20KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_25KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 28.61,
        "currency": "USD",
        "vendorPrice": 38.23,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 25,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_25KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_30KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 33.93,
        "currency": "USD",
        "vendorPrice": 45.34,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 30,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_30KG"
      },
      {
        "segmentIndex": 2,
        "endSegmentIndex": null,
        "productCode": "SCI_BAG_5KG",
        "productName": "StandardCheckInBaggage",
        "productType": 1,
        "canPurchaseWithTicket": 1,
        "canPurchasePostTicket": 1,
        "price": 7.32,
        "currency": "USD",
        "vendorPrice": 9.78,
        "vendorCurrency": "SGD",
        "clientTechnicalServiceFee": 0,
        "auxBaggageElement": {
          "piece": 0,
          "weight": 5,
          "isAllWeight": true
        },
        "offerId": null,
        "ancillaryCode": "SCI_BAG_5KG"
      }
    ],
    "vendorFare": null,
    "bundleOptions": [],
    "links": [],
    "separateBookings": false
  },
  "status": 0,
  "msg": null
}
{% endtab %}
{% endtabs %}
