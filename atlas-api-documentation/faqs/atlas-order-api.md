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

Order Request:

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
