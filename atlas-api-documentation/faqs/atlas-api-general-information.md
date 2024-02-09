# Atlas API General Information

**Which airlines will our customers be able to book with?**

We partner with over 150 airlines; the complete list of airlines is available [here](https://www.atriptech.com/#/airline/list).We keep adding new airlines to our list as and when we partner with them. You can also view the list of airlines under Airline List on ATRIP.

Once you are on board with us, you should be able to offer all the routes available with our partner airlines almost instantly.



**Can we test the API functionality before we partner with Atlas?**

We want you to test Atlas API functionality before you make a commitment, so take a minute to fill out [this form](https://atlaslovestravel.com/get-started/), and we will get in touch with you within 2 working days. To protect our partner airlines, we need to confirm your details and get you to sign an NDA. As soon as we have verified your identity, your test credentials will be in your inbox. 



**Are there any restrictions on the API functionality for any of the airlines?**

We want to offer maximum opportunities for both our partner airlines and travel agencies, so Atlas API supports all functionalities, as provided by Airlines.



**How much fee does Atlas charge in exchange for its API?**

If you could quickly fill out [this form](https://atlaslovestravel.com/contact/), we can put you in touch with a local Atlas representative to help you understand our pricing model in your country. Due to differences in currencies and regional regulations, the pricing may vary.



**Does Atlas support promotional fare/promotional code-based pricing?**

We are currently providing general promotional fare functionality, and we will soon introduce promo code support to our partners.



**What is the look-to-book (L2B) ratio for Atlas?**

The L2B ratio will be determined as per the commercial agreement between Atlas and your agency.



**Does Atlas deploy cache?**

Atlas API has a general cache pool to save search results data and we can also deploy client-specific cache.



**What should we do if we encounter API failure?**

Atlas will provide a web portal to support ticket booking, ticketing, and post ticketing services in case of API failure. Our developers are currently working hard to build this portal. You can reach out to the API support team or the Customer Service Centre in the interim.



**Does Atlas provide a fare guarantee?**

The fare is guaranteed after the ticket booking is paid to Atlas. Atlas API will automatically issue tickets once the transaction is complete. The entire process usually takes up to 10 minutes; in some rare scenarios, it may go up to 1 hour. Please note that the Atlas Fare Guarantee is only applicable for the transactions done via the "deposit" mode of payment. The Atlas Fare Guarantee is not applicable for VCC pass-through mode of payment.



**Is there a time-out limit for each of Atlas' API?**

The time-out limit for each of the standard API's are:

search.do: no limit/not defined

realTimeSearch.do: 120s

verify.do: 15s

order.do: 15s for normal booking and 120s for real time booking

pay.do: no limit/not defined



**What is the API response time for each of the Atlas APIs?**

The average response times for each of the standard APIs are as below:

search.do: < 500ms (98% of the responses are returned in less than 500ms)

verify.do: 8s (90% of the responses are returned in less than 8s)

order.do: 8s (90% of the responses are returned in less than 8s)

pay.do: 2s(90% of the responses are returned in less than 2s)
