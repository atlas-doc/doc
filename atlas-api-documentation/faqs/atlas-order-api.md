# Atlas Order API

**Does the `OrderAPI` hold the inventory? If yes, then for how long?**&#x20;

We allow you to hold the inventory and guarantee the price for 30 mins after an order is generated. If the payment is not made during these 30 minutes, the price guarantee is void. &#x20;

 &#x20;

**Can we release the inventory which is on hold at our end?**&#x20;

The Atlas API holds the inventory after the `OrderAPI` calls. We have a built-in mechanism to release the inventory after 30 minutes have passed. Different airlines have different mechanisms to release inventory; hence we cannot provide partner agencies with a function to request the release of inventory.&#x20;

&#x20;
