# Atlas API Search&Booking

**Can our users change the currency to see ticket prices in their local currency with Atlas?**

Currently, your users can only see ticket prices in the currency we will settle with you. We don't offer the option to change currency at this time. If you have specific needs, get in touch with us and let’s find a solution together.



**Why is the tax break up not provided for tickets in the search results?**

We don't provide tax breakup currently because many LCCs don't supply this information during the booking process or in the PNR. We are working to include the tax breakup for airlines who provide us with the split.



**Can you explain the use of `TransactionFeePerPax` element?**

We charge a technical service fee for every ticket, on top of the airfare and tax. This fee is non-refundable.



**Why are critical nodes such as`booking`  `class`and`fare basis`missing from the`segment element schema`?**

Contrary to Global Distribution Systems (GDSs), most LCCs do not provide cabin class and fare basis. Hence, these nodes are not mandatory for creating a PNR. Please refer to thecabinelement; the booking code information is only available for airlines who provide it to us.



**How many results does the search query return, and what is the default sorting order?**

By default, Atlas API will return all available offers in the search response. We will soon add functionality to let you control the number of search results by modifying the API. The default sort order is from lowest fare to highest fare.


**What does the `seatCount`element denote in the search response?**

This element returns the remaining seats for the fare. Many LCCs have a high reservation error rate when the passenger count is greater than 4, so Atlas limits the maximum seat count to 4. Please avoid sending more than 4 passengers in the search request.



**What is the maximum time gap allowed between`search`and`revalidation`?**

We allow for a maximum time gap of 2 hours. But when the time gap is longer, the possibility of price change is higher.



**What is the maximum time gap between`revalidation`and`order`?**

We allow for a maximum time gap of 30 mins. But when the time gap is longer, the possibility of price change is higher.



**Can we allow users to change the passenger count in the order step from what they entered in the search and revalidation steps?**

Yes, you can. Provided the user has entered at least 1 Adult traveller (ADT) for search and revalidation, you can allow your users to change number of passengers during the order step. However, if you're using other options, it's better to keep the count same throughout the search, revalidation and order. Revalidation is a real-time search with the airline and hence it impacts the inventory. If the count changes after the revalidation process, there is a high chance of failure due to seat availability.
