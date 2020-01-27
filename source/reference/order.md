# Order Resource

A purchase order for data plans and eSIMs

**Properties**

|   Property Name   |            Description             |
| :---------------: | :--------------------------------: |
|    externalId     |        The order identifier        |
|      status       |          The order status          |
|       input       | Data required to process the order |
|      output       |  Produced output after completed   |
| output.matchingId |      The eSIM activation code      |
|   output.iccid    |       The profile identifier       |
|  output.smdpUrl   |            The rsp URL             |

**Possible values for `status`**

| Property Name |      Description       |
| :-----------: | :--------------------: |
|   COMPLETED   |     Order complete     |
|    FAILED     |      Order Failed      |
|  FULFILLING   | Order still processing |

## Ordering a new eSIM

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `v1/order`
- METHOD: `POST`

### Rules and validations

- If the customer does not exist it will be created
- `operationType` - Needs to be `NEW_ESIM`
- `subscriptions.product_id` (preferred) or `subscriptions.allowanceId` (deprecated) - Needs to be an id that belongs to the product catalog of the customer
- `subscriptions.activationDate` - Can not be a date in the past
- `subscriptions.price` - If is sent, it must be sent in pair with `subscriptions.currency`
- `subscriptions.currency` - If is sent, it must be sent in pair with `subscriptions.price` and needs to be one of the currencies supported by the customer
- `device.type` - Must be one of the following values: `iot`, `ios` or `android`

### Example Request

```bash
curl -X POST \
  https://services.truphone.com/esim/v1/order \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'X-Correlation-ID: unique-id-from-requester-123' \
  -d '{
      	"input": {
            "operationType": "NEW_ESIM",
            "countryCode": "PT",
            "customer": {
                "email": "john@doe.com",
                "countryOfResidence": "US"
            },
            "device": {
                "product_id": "123456789",
                "model": "iPhone",
                "type": "ios"
            },
      	    "subscriptions": [{
      	        "id": "a3u3z000000PZBhAAO",
      	        "activationDate": "2019-09-13T12:00:00Z",
      	        "price": 10,
      	        "currency": "USD"
      	    }]
      	}
      }'
```

### Example Response

```javascript
{
  "externalId": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "status": "ACCEPTED"
}
```

The externalId identifies the order on truphone's end and should be used to check the status and output of the order by the client. This will always be unique to each order.


## Topping up an existing eSIM

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `v1/order`
- METHOD: `POST`

### Rules and validations

- The customer must already exist
- `operationType` - Needs to be `TOPUP` (preferred) or `TOPUP_ACTIVATION` (deprecated)
- `subscriptions.product_id` (preferred) or `subscriptions.allowanceId` (deprecated) - Needs to be an id that belongs to the product catalog of the customer
- `subscriptions.activationDate` - Can not be a date in the past
- `subscriptions.price` - If is sent, it must be sent in pair with `subscriptions.currency`
- `subscriptions.currency` - If is sent, it must be sent in pair with `subscriptions.price` and needs to be one of the currencies supported by the customer
- `device.type` - Must be one of the following values `ios` or `android`

In order to call this endpoint, both the `customer.email` and `esim.iccid` nodes are mandatory and must match each other, otherwise the topup won't be performed:

- `esim` and `esim.iccid` are mandatory
- `customer.email` - the email used to order the first eSIM;
- `esim.iccid` - the iccid obtained when the first eSIM was ordered.

### Example Request

```bash
curl -X POST \
  https://services.truphone.com/esim/v1/order \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'X-Correlation-ID: unique-id-from-requester-123' \
  -d '{
      	"input": {
            "operationType": "TOPUP_ACTIVATION",
            "countryCode": "PT",
            "customer": {
                "email": "john@doe.com",
                "countryOfResidence": "US"
            },
            "device": {
                "product_id": "123456789",
                "model": "iPhone",
                "type": "ios"
            },
            "subscriptions": [{
      	        "id": "a3u3z000000PZBhAAO",
      	        "activationDate": "2019-09-13T12:00:00Z",
      	        "price": 10,
      	        "currency": "USD"
      	    }],
      	    "esim": {
      	        "iccid": "123456789"
      	    }
      	}
      }'
```

### Response

```javascript
{
  "externalId": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "status": "ACCEPTED"
}
```

The externalId identifies the order on truphone's end and should be used to check the status and output of the order by the client.
