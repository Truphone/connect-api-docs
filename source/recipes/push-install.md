# Push Install

A collection of some use cases and a tutorial on how to achieve them.

## Ordering an eSIM (with and without push install support)

More rules and details on the **Order** section.

### Example Request (without push install support)

It's a pretty straightforward request, filling the necessary fields.

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
            },
      	    "subscriptions": [{
      	        "product_id": "a3u3z000000PZBhAAO",
      	        "activationDate": "2019-09-13T12:00:00Z",
      	        "price": 10,
      	        "currency": "USD"
      	    }]
      	}
      }'
```

### Example Request (with push install support)

For supporting push install, the `device.type` must be `ios`. If it is, we simply need to add the EID value on the `device.eid` field.
If the `device.type` is not `ios` and the `device.eid` field has a value, it is ignored.

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
                "type": "ios",
                "eid": "89001012012341234012345678901224"
            },
      	    "subscriptions": [{
      	        "product_id": "a3u3z000000PZBhAAO",
      	        "activationDate": "2019-09-13T12:00:00Z",
      	        "price": 10,
      	        "currency": "USD"
      	    }]
      	}
      }'
```

### Example Response (for both scenarios)

```json
{
  "id": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "externalId": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "status": "ACCEPTED"
}
```

## Getting the details of a SIM

We just need to invoke the get details endpoint, sending the iccid that is associated with the SIM on the URL.

Depending if it's an eSIM or SIM, and depending also on the device type, there are some fields that may or may not be present. For more details on which fields should be present, please refer to the
**Sims** section 

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/connect-api/v1/sim/8944474600000109251 \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
{
  "iccid": "8944474600000063847",
  "matching_id": "O-17QF0-MJVBIN",
  "status": "Released",
  "eid": "89001012012341234012345678901224",
  "last_modified": "2019-08-02T09:09:33Z"
}
```