# Atlas API API Search

**Can our users change the currency to see ticket prices in their local currency with Atlas?**&#x20;

Currently, your users can only see ticket prices in the currency we will settle with you. We don't offer the option to change currency at this time. If you have specific needs, get in touch with us and let’s find a solution together. &#x20;

&#x20;

**Can we control/filter the carriers in search response with Atlas?**&#x20;

Currently the API doesn’t allow for this feature. We are working to add this feature so our partner agencies can limit the search results to include only their preferred airlines. This functionality is in our roadmap for Q2/2022.&#x20;

 &#x20;

**Why is the tax break up not provided for tickets in the search results?**&#x20;

We don't provide tax breakup currently because many LCCs don't supply this information during the booking process or in the PNR. We are working to include the tax breakup for airlines who provide us with the split.&#x20;

 &#x20;

**Can you explain the use of `TransactionFeePerPax` element?**&#x20;

We charge a technical service fee for every ticket, on top of the airfare and tax. This fee is non-refundable.&#x20;

 &#x20;

**Why are critical nodes such as `booking`  `class` and `fare basis` missing from the `segment element schema`?**&#x20;

Contrary to Global Distribution Systems (GDSs), most LCCs do not provide cabin class and fare basis. Hence, these nodes are not mandatory for creating a PNR. Please refer to the cabin element; the booking code information is only available for airlines who provide it to us.&#x20;

 &#x20;

**How many results does the search query return, and what is the default sorting order?**&#x20;

By default, Atlas API will return all available offers in the search response. We will soon add functionality to let you control the number of search results by modifying the API. The default sort order is from lowest fare to highest fare.&#x20;

 &#x20;

**Does Atlas support special fares with passenger restrictions?**&#x20;

The special fare functionality, with passenger restrictions such as age and nationality, is currently not supported. We plan to support this functionality starting Q2 2022.&#x20;

&#x20;

**What does the `seatCount` element denote in the search response?**&#x20;

This element returns the remaining seats for the fare. Many LCCs have a high reservation error rate when the passenger count is greater than 4, so Atlas limits the maximum seat count to 4. Please avoid sending more than 4 passengers in the search request.&#x20;

 &#x20;

**What is the maximum time gap allowed between `search` and `revalidation`?**&#x20;

We allow for a maximum time gap of 2 hours. But when the time gap is longer, the possibility of price change is higher.&#x20;

 &#x20;

**What is the maximum time gap between `revalidation` and `order`?**&#x20;

We allow for a maximum time gap of 30 mins. But when the time gap is longer, the possibility of price change is higher.&#x20;

 &#x20;

**Can we allow users to change the passenger count in the order step from what they entered in the search and revalidation steps?**&#x20;

Yes, you can. Provided the user has entered at least 1 Adult traveller (ADT) for search and revalidation, you can allow your users to change number of passengers during the order step. However, if you're using other options, it's better to keep the count same throughout the search, revalidation and order. Revalidation is a real-time search with the airline and hence it impacts the inventory. If the count changes after the revalidation process, there is a high chance of failure due to seat availability.&#x20;
