# Order Resource

* Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
* Base URL: `v1/order`

## New eSIM

## Topup

## Input parameters

| Parameter Name               | Mandatory     | Default Value                   |
| :--------------------------: | :-----------: | :-----------------------------: |
| operationType                | yes           |                                 |
| countryCode                  | yes           |                                 |
| subscriptions                | yes           |                                 |
| subscriptions.id             | yes           |                                 |
| subscriptions.type           | no            | REGULAR                         |
| subscriptions.activationDate | no            | Current timestamp               |
| subscriptions.autoRenew      | no            | false                           |
| subscriptions.dataValue      | no            | Allowance data value            |
| subscriptions.dataUnit       | no            | Allowance data unit             |
| subscriptions.price          | no            | Allowance price                 |
| subscriptions.currency       | no            | Allowance currency              |
| device                       | yes           |                                 |
| device.type                  | yes           |                                 |
| device.model                 | no            |                                 |
| device.id                    | yes           |                                 |
| device.uicc                  | no            |                                 |
| device.imei                  | no            |                                 |
| customer                     | yes           |                                 |
| customer.email               | yes           |                                 |
| customer.firstName           | no            | Equals to the email value       |
| customer.lastName            | no            |                                 |
| customer.language            | no            | EN                              |
| customer.countryOfResidence  | no            |                                 |
| esim                         | no            |                                 |
| esim.iccid                   | no            |                                 |

## New eSIM
The customer does not own neither an eSIM nor a data plan subscription. Calling the order endpoint with this configuration will provision a new eSIM/ICCID and add a data plan to the provisioned eSIM. If the customer does not exist, it will also be created.

## Aditional rules and validations

- `operationType` - Needs to be `NEW_ESIM`
- `subscriptions.id` - Needs to be an id that belongs to the product catalog of the customer
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
                "id": "123456789",
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

### Response
```json
{
  "externalId": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "status": "ACCEPTED"
}
```
The externalId identifies the order on truphone's end and should be used to check the status and output of the order by the client.  This will always be unique to each order.

### Response codes

| HTTP Status code | Error message code         | Description                                  |
| :--------------: | :------------------------: | :------------------------------------------: |  
| 201              |                            | Order created successfully                   |
| 400              | INVALID_REQUEST_PARAMS     | Bad input parameters                         |            
| 422              | PRODUCT_NOT_FOUND          | Product was not found for given id           |             
| 500              | INTERNAL_ERROR             | There was a error trying to create the order |             

### Error codes
| Error code                | Description                                     |
| :-----------------------: | :---------------------------------------------: | 
| PRODUCT_NOT_FOUND         | The product was not found for given id          |


## Topup
The customer already owns an eSIM and wants to perform a topup operation.

## Aditional rules and validations

- `operationType` - Needs to be `TOPUP` (preferred) or `TOPUP_ACTIVATION` (deprecated)
- `subscriptions.id` - Needs to be an id that belongs to the product catalog of the customer
- `subscriptions.activationDate` - Can not be a date in the past
- `subscriptions.price` - If is sent, it must be sent in pair with `subscriptions.currency`
- `subscriptions.currency` - If is sent, it must be sent in pair with `subscriptions.price` and needs to be one of the currencies supported by the customer
- `device.type` - Must be one of the following values `ios` or `android`

In order to call this endpoint, both the `customer.email` and `esim.iccid` nodes are mandatory and must match each other, otherwise the topup won't be performed:

- `esim` and `esim.iccid` are mandatory
- `customer.email` - the email used to order the first eSIM;
- `esim.iccid` - the iccid obtained when the first eSIM was ordered.

### Request
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
                "id": "123456789",
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
```json
{
  "externalId": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "status": "ACCEPTED"
}
```
The externalId identifies the order on truphone's end and should be used to check the status and output of the order by the client.

### Response codes
| HTTP Status code | Error message code           | Description                                  |
| :--------------: | :--------------------------: | :------------------------------------------: |  
| 201              |                              | Order created successfully                   |
| 400              | INVALID_REQUEST_PARAMS       | Bad input parameters                         |            
| 422              | PRODUCT_NOT_FOUND            | Product was not found for given id           |             
| 422              | EMAIL_AND_ICCID_DO_NOT_MATCH | Email and ICCID do not match each other      |             
| 422              | CUSTOMER_MUST_EXIST          | Does not exist a customer for given email    |             
| 500              | INTERNAL_ERROR               | There was a error trying to create the order |             

### Error codes
| Error code                   | Description                                     |
| :--------------------------: | :---------------------------------------------: | 
| PRODUCT_NOT_FOUND            | The product was not found for given id          |
| EMAIL_AND_ICCID_DO_NOT_MATCH | Email and ICCID do not match each other         |
| CUSTOMER_MUST_EXIST          | Does not exist a customer for given email       |

## Bulk Activation
The customer already owns an eSIM and wants to perform a bulk activation . 
On a single request it's possible to have multiple subscriptions, each one with an unique product to multiple ICCID's.
If the customer does not exist, it will also be created.

Take in consideration if one input parameter is wrong, the order for all subscriptions is canceled.

### Aditional rules and validations

- `operationType` - Needs to be `BULK_ACTIVATION`
- `subscriptions.id` - Needs to be an id that belongs to the product catalog of the client
- `subscriptions.activationDate` - Can not be a date in the past
- `subscriptions.price` - If is sent, it must be sent in pair with `subscriptions.currency`
- `subscriptions.currency` - If is sent, it must be sent in pair with `subscriptions.price` and needs to be one of the currencies supported by the client
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
              "countryCode": "PT",
              "operationType" : "BULK_ACTIVATION",
              "customer": {
              	"type" : "PERSONAL",
              	"countryOfResidence" : "PT",
                  "email": "test_customer_e2e@gmail.com",
                  "firstName" : "tests",
                  "lastName" : "truphone",
                  "language" : "PT"
              },
              "device": {
                  "id": "123456789",
                  "model": "iPhone",
                  "type": "ios",
                  "imei" : "1234"
              },
              "subscriptions": [
                  {
                  	"iccid" : ["8944474600000101811, 8944474600000101811"],
                  	"id" : "a3mM0000000Dcmr",
                    "activationDate" : "2019-12-28T12:00:00Z"
                  },
                  {
                  	"iccid" : ["8944474600000101811, 8944474600000101811"],
                  	"id" : "a3mM0000000Dcmw",
                    "activationDate" : "2019-12-28T12:00:00Z"
                  }
              ],
              "payment" : {
              	"token" : "1234"
              }
          }
      }'
```

### Response
```json
{
  "externalId": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "status": "ACCEPTED"
}
```
The externalId identifies the order on truphone's end and should be used to check the status and output of the order by the client.  This will always be unique to each order.

### Response codes
| HTTP Status code | Error message code         | Description                                  |
| :--------------: | :------------------------: | :------------------------------------------: |  
| 201              |                            | Order created successfully                   |
| 400              | INVALID_REQUEST_PARAMS     | Bad input parameters                         |            
| 422              | PRODUCT_NOT_FOUND          | Product was not found for given id           |             
| 500              | INTERNAL_ERROR             | There was a error trying to create the order |             

## Order status
The customer created an order and is waiting for it to complete.

- URL: `v1/order/{orderId}`
- METHOD: `GET`

### Request
```bash
curl -X GET \
  https://services.truphone.com/esim/v1/order/3a6acf89-1ccf-4611-9424-453930f57ef1 \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Response
```json
{
  "externalId": "3a6acf89-1ccf-4611-9424-453930f57ef1",
  "status": "COMPLETED",
  "output": {
      "iccid": "1234567890",
      "matchingId": "M-123DSA-AS",
      "smdpUrl": "rsp.truphone.com"
  }
}
```
When completed, the order contains the `output` field with the data that is relevant for eSIM installation and subsequent account status queries

### Response codes
| HTTP Status code | Error message code | Description                               |
| :--------------: | :----------------: | :---------------------------------------: |  
| 200              |                    | Order information was retriever           |
| 404              | ORDER_NOT_FOUND    | Order was not found for the giver orderId |
