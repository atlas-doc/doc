---
description: Create an order request to search for flights with multiple farefamilies.
---

# Search

### Dependency

No preceding function needs to be called before `Search`, if you want to return all flights and all farefamilies prices at once.

The search function can be called prior to this call, if you want to first obtain the lowest price for all flights at once, and then specify flights to return the prices for farefamilies.

### Endpoint {% debug uid="search_1.0" %}{% enddebug %}

[https://sandbox.atriptech.com/multipleFareFamilySearch.do](https://sandbox.atriptech.com/multipleFareFamilySearch.do)

### Request

{% tabs %}
{% tab title="Schema" %}

**`cid`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Identifier of client and user.

**`tripType`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

1: Oneway

2: Return Trip

**`adultNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Adult passenger count, the number can be 1-9

**`childNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:green;">**Required**</mark>

Child passenger count, the number can be 0-8

**`infantNum`  **<mark style="color:blue;">**int**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Infant passenger count, no more than the number of adult

**`fromCity`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

IATA Code of departure city or airport

**`toCity`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

IATA Code of arrival city or airport

**`fromDate`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:green;">**Required**</mark>

Departure date, the format is YYYYMMDD

**`retDate`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Return date, the format is YYYYMMDD

Must not be earlier than fromDate. And it can be blank if tripType=1.

**`airlines`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

An array of IATA Codes of airlines. The result will only contain the airlines specified in the search request.

**`fromFlightNumbers`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Outbound Flight Numbers. The result will only contain the flight numbers specified in the search request. The format of connection flights should be "VJ904,VJ938".

**`retFlightNumbers`  **<mark style="color:blue;">**array**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Inbound Flight Numbers. The result will only contain the flight numbers specified in the search request. The format of connection flights should be "VJ904,VJ938".

**`requestSource`  **<mark style="color:blue;">**string**</mark>**  **<mark style="color:orange;">**Optional**</mark>

Identify the source of the search traffic, E.g. Google Flights, Oganic Search, SkyScanner.

{% endtab %}

{% tab title="Samples" %}
```
{
  "cid": "XXXXXXXXX",
  "tripType": 2,
	"adultNum": 1,
	"childNum": 1,
	"infantNum": 1,
	"fromCity": "BKK",
	"toCity": "OSA",
	"fromDate": "20231118",
	"retDate": "20231128",
  "fromFlightNumbers": ["VJ904,VJ938"],
  "retFlightNumbers": ["VZ567"]
	"requestSource": "Organic"
}
```
{% endtab %}
{% endtabs %}






