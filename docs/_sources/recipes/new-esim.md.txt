# Getting a new eSIM

## Placing the Order

The first step you need to do in order to get a fresh new eSIM is to place an order (Head over to the [Order](../reference/orders.md) for the full API reference). It is a pretty straightforward request as described in the example below.

> Note: If you have an iOS device and wish to use the push install feature (More details below), you need to specify `device.eid` field. If the `device.type` is not `ios`, the `device.eid` field is ignored.

### Example Request

```bash
curl -X POST \
  https://services.truphone.com/connect-api/v1/order \
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
                "id": "123456789",
                "model": "iPhone",
                "type": "ios"
                # Include EID Parameter for Push Install
                "eid": "89001012012341234012345678901224"**
            },
      	    "subscriptions": [{
      	        "product_id": "cm9kIiwiY2xpZW50QWRkcmVzcyI",
      	        "activationDate": "2019-09-13T12:00:00Z",
      	        "price": 10,
      	        "currency": "USD"
      	    }]
      	}
      }'
```

### Example Response

```json
{
  "id": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "externalId": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "status": "ACCEPTED"
}
```

## Installing the eSIM

As soon as the order is complete (Head over to the [Order](../reference/orders.md) for info on how to check order state), you have 3 options for installing the eSIM:

## QRCode

Using the smdp url (always `rsp.truphone.com`) and the matching id (you can get it either from the [Order](../reference/orders.md) or [Sim](../reference/sims.md) status endpoints) you can generate a QRCode that is recognizable by the target device to start the installation proccess. The QRCode format should be as follows:

``` 
LPA:1$rsp.truphone.com${MATCHINGID}
```

## Push Install (iOS only) 

By providing the EID of the target device as described in the example request, Connect is able to trigger a request which will display a push notification in the target device to trigger the installation.
 

## Connect SDK or Direct Install

Either using our SDKs or via direct eUICC API integration you can use the API information to trigger a local install. Just like in the QRCode method, you need the smdp url and the matching id values to trigger the installation process
