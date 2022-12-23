# Register Webhook

## Request

{% tabs %}
{% tab title="Schema" %}
*   #### cid                          <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Identifier of client and user.
*   #### url                           <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    The url address to receive webhook message.
{% endtab %}

{% tab title="Sample" %}
```json
{
    "cid": "XXXXXXXX",
    "url": "https://xxx.com/xxxx"
}
```
{% endtab %}
{% endtabs %}

## Response

{% tabs %}
{% tab title="Schema" %}
*   #### status                                  <mark style="color:blue;">int</mark>                                                                                                       <mark style="color:green;">Required</mark>

    0: success

    2: System error
*   #### msg                                      <mark style="color:blue;">string</mark>                                                                                                 <mark style="color:green;">Required</mark>

    Error message.
    
    The 'msg' element is for description of the results. Please DO NOT use this field to check the success or failure of the request. Only use the 'status' code to         check the result.
{% endtab %}

{% tab title="Sample" %}
```
{
    "status": 0,
    "msg": "success"
}
```


{% endtab %}
{% endtabs %}
