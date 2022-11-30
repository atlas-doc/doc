# Making requests

Let’s help you with the building blocks to set up your first request.

#### Authentication

You will receive `x-atlas-client-id` and `x-atlas-client-secret` from Atlas before you start development. Whenever you send a request, the header must include the authentication keys. Any request that doesn't include an API key will return an error.

```
x-atlas-client-id: <Your clientid> 
x-atlas-client-secret: <Your client secretid> 
```

#### MIME types

All requests sent to the Atlas API should be in JSON format. When sending a request body, you must include `Content-Type` in the header (i.e. for `POST` and `PUT` requests):

```
Content-Type: application/json
```

#### Compression

API responses can be very large, so we recommend enabling compression for responses returned by the API. Include `Accept-Encoding` in the header to enable compression:

```
Accept-Encoding: gzip 
```

Most HTTP clients will decompress responses. If your client doesn’t have this functionality built in, you'll need to configure it.
