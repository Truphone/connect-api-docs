# Customer

## Customer Resource

## Creating a new customer

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer`
- METHOD: `POST`

### Input parameters

|   Parameter Name   |  Mandatory   | Default Value |
| :----------------: | :----------: | :-----------: |
|       email        |     yes      |               |
|        type        |     yes      |   PERSONAL    |
|     firstName      |      no      |               |
|      lastName      |      no      |               |
|      language      |      no      |      EN       |
| countryOfResidence | configurable |               |
|    phoneNumber     |      no      |               |
|  defaultCurrency   |      no      |               |
|      verified      |      no      |               |
|   billingAddress   |      no      |               |
|  shippingAddress   |      no      |               |
|    companyName     |  dependable  |               |
|   companyNumber    |  dependable  |               |
|      jobTitle      |  dependable  |               |

### Additional rules and validations

- The `type` parameter must have one of the following values: `PERSONAL` or `BUSINESS`.
- If `type` equals to `BUSINESS` then the input parameters are the same as `PERSONAL` plus:
  - companyName
  - companyNumber
  - jobTitle

### Example request

#### Personal

```bash
curl -X POST \
  https://services.truphone.com/esim/v1/customer \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'X-Correlation-ID: unique-id-from-requester-123' \
  -d '{
        "email": "john@doe.com",
        "firstName": "John",
        "lastName": "Doe",
        "countryOfResidence": "US",
        "language": "EN",
        "phoneNumber": "0044102938120",
        "defaultCurrency": "EUR",
        "type": "PERSONAL",
        "verified": true,
        "billingAddress" : {
          "streetAddress1" : "Rua das flores",
          "streetAddress2" : "Primeiro Esquerdo",
          "city": "Lisboa",
          "state": "Lisboa",
          "postCode": "1234-567",
          "country": "Portugal"
        },
        "shippingAddress" : {
          "streetAddress1" : "Rua das flores",
          "streetAddress2" : "Primeiro Esquerdo",
          "city": "Lisboa",
          "state": "Lisboa",
          "postCode": "1234-567",
          "country": "Portugal"
        }
      }'
```

#### Business

```bash
curl -X POST \
  https://services.truphone.com/esim/v1/customer \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'X-Correlation-ID: unique-id-from-requester-123' \
  -d '{
        "email": "john@doe.com",
        "firstName": "John",
        "lastName": "Doe",
        "countryOfResidence": "US",
        "language": "EN",
        "phoneNumber": "0044102938120",
        "defaultCurrency": "EUR",
        "type": "BUSINESS",
        "verified": true,
        "companyName": "TruExample",
        "companyNumber": "123456789",
        "jobTitle": "Software Engineer",
        "billingAddress" : {
          "streetAddress1" : "Rua das flores",
          "streetAddress2" : "Primeiro Esquerdo",
          "city": "Lisboa",
          "state": "Lisboa",
          "postCode": "1234-567",
          "country": "Portugal"
        },
        "shippingAddress" : {
          "streetAddress1" : "Rua das flores",
          "streetAddress2" : "Primeiro Esquerdo",
          "city": "Lisboa",
          "state": "Lisboa",
          "postCode": "1234-567",
          "country": "Portugal"
        }
      }'
```

### Response codes

| HTTP Status code |    Error message code     |          Description          |
| :--------------: | :-----------------------: | :---------------------------: |
|       201        |                           | Customer created successfully |
|       400        |  INVALID_REQUEST_PARAMS   |     Bad input parameters      |
|       422        | UNABLE_TO_CREATE_CUSTOMER |   Unable to create customer   |

### Error codes

|        Error code         |        Description        |
| :-----------------------: | :-----------------------: |
| UNABLE_TO_CREATE_CUSTOMER | Email already registered. |

## Retrieving customer details

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer`
- METHOD: `GET`

### Input parameters

| Parameter Name | Mandatory | Default Value |
| :------------: | :-------: | :-----------: |
|     email      |    yes    |               |

### Example request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/customer?email=tests.contoso@email.com
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Response Body

```json
{
  "email": "john@doe.com",
  "firstName": "John",
  "lastName": "Doe",
  "countryOfResidence": "US",
  "language": "EN",
  "phoneNumber": "0044102938120",
  "defaultCurrency": "EUR",
  "type": "BUSINESS",
  "verified": true,
  "companyName": "TruExample",
  "companyNumber": "123456789",
  "jobTitle": "Software Engineer",
  "billingAddress": {
    "streetAddress1": "Rua das flores",
    "streetAddress2": "Primeiro Esquerdo",
    "city": "Lisboa",
    "state": "Lisboa",
    "postCode": "1234-567",
    "country": "Portugal"
  },
  "shippingAddress": {
    "streetAddress1": "Rua das flores",
    "streetAddress2": "Primeiro Esquerdo",
    "city": "Lisboa",
    "state": "Lisboa",
    "postCode": "1234-567",
    "country": "Portugal"
  }
}
```

### Response codes

| HTTP Status code | Error message code |       Description       |
| :--------------: | :----------------: | :---------------------: |
|       200        |                    |     Customer found      |
|       404        | CUSTOMER_NOT_FOUND | Customer does not exist |

## Updating customer details

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer/{id}`
- METHOD: `PATCH`

### Input parameters

All fields are optional. Not sending a field will not change its value, and sending `null` values will delete the corresponding fields.

|   Parameter Name   |  Mandatory   | Default Value |
| :----------------: | :----------: | :-----------: |
|       email        |     yes      |               |
|        type        |     yes      |   PERSONAL    |
|     firstName      |      no      |               |
|      lastName      |      no      |               |
|      language      |      no      |      EN       |
| countryOfResidence | configurable |               |
|    phoneNumber     |      no      |               |
|  defaultCurrency   |      no      |               |
|      verified      |      no      |               |
|   billingAddress   |      no      |               |
|  shippingAddress   |      no      |               |
|    companyName     |  dependable  |               |
|   companyNumber    |  dependable  |               |
|      jobTitle      |  dependable  |               |

## Additional rules and validations

- The `type` parameter must have one of the following values: `PERSONAL` or `BUSINESS`.
- If `type` equals to `BUSINESS` then the input parameters are the same as `PERSONAL` plus:
  - companyName
  - companyNumber
  - jobTitle

### Example request

#### Personal

```bash
curl -X PATCH \
  https://services.truphone.com/esim/v1/customer?id=a0xM0000004y000 \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'X-Correlation-ID: unique-id-from-requester-123' \
  -d '{
              "email": "john@doe.com",
              "firstName": "John",
              "lastName": "Doe",
              "countryOfResidence": "US",
              "language": "EN",
              "phoneNumber": "0044102938120",
              "defaultCurrency": "EUR",
              "type": "PERSONAL",
              "verified": true,
              "billingAddress" : {
                "streetAddress1" : "Rua das flores",
                "streetAddress2" : "Primeiro Esquerdo",
                "city": "Lisboa",
                "state": "Lisboa",
                "postCode": "1234-567",
                "country": "Portugal"
              },
              "shippingAddress" : {
                "streetAddress1" : "Rua das flores",
                "streetAddress2" : "Primeiro Esquerdo",
                "city": "Lisboa",
                "state": "Lisboa",
                "postCode": "1234-567",
                "country": "Portugal"
              }
            }'
```

#### Business

```bash
curl -X PATCH \
  https://services.truphone.com/esim/v1/customer?id=a0xM0000004y000 \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H 'Cache-Control: no-cache' \
  -H 'Content-Type: application/json' \
  -H 'X-Correlation-ID: unique-id-from-requester-123' \
  -d '{
              "email": "john@doe.com",
              "firstName": "John",
              "lastName": "Doe",
              "countryOfResidence": "US",
              "language": "EN",
              "phoneNumber": "0044102938120",
              "defaultCurrency": "EUR",
              "type": "BUSINESS",
              "verified": true,
              "companyName": "TruExample",
              "companyNumber": "123456789",
              "jobTitle": "Software Engineer",
              "billingAddress" : {
                "streetAddress1" : "Rua das flores",
                "streetAddress2" : "Primeiro Esquerdo",
                "city": "Lisboa",
                "state": "Lisboa",
                "postCode": "1234-567",
                "country": "Portugal"
              },
              "shippingAddress" : {
                "streetAddress1" : "Rua das flores",
                "streetAddress2" : "Primeiro Esquerdo",
                "city": "Lisboa",
                "state": "Lisboa",
                "postCode": "1234-567",
                "country": "Portugal"
              }
            }'
```

### Response codes

| HTTP Status code | Error message code |       Description       |
| :--------------: | :----------------: | :---------------------: |
|       200        |                    | Customer record updated |

## Get available payment methods

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer/{customerId}/payment-method`
- METHOD: `GET`

### Example request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/customer/KS27CmTTmaoh7e318ek0CA==/payment-method
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example response body

```json
[
  {
    "token": "1238",
    "name": "John Doe",
    "type": "VISA",
    "lastDigits": "1234",
    "expiryMonth": "12",
    "expiryYear": "1234",
    "gateway": "CYBERSOURCE"
  }
]
```

### Response codes

| HTTP Status code |      Error message code       |    Description     |
| :--------------: | :---------------------------: | :----------------: |
|       200        |                               |         OK         |
|       422        | UNABLE_TO_GET_PAYMENT_METHODS | Customer not found |

## Add a Payment Method

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer/{customerId}/payment-method`
- METHOD: `POST`

### Input parameters

| Parameter Name | Mandatory | Default Value |
| :------------: | :-------: | :-----------: |
|     token      |    yes    |               |
|      name      |    no     |               |
|      type      |    yes    |               |
|   lastDigits   |    yes    |               |
|  expiryMonth   |    yes    |               |
|   expiryYear   |    yes    |               |
|    gateway     |    yes    |               |

### Example request

```bash
curl -X POST \
  https://services.truphone.com/esim/v1/customer/KS27CmTTmaoh7e318ek0CA==/payment-method
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
   -d '{
            "token" : "1238",
            "name" : "John Doe",
            "type" : "VISA",
            "lastDigits" : "1234",
            "expiryMonth" : "12",
            "expiryYear" : "1234",
            "gateway" : "CYBERSOURCE"
       }'
```

### Example response body

```json
{
  "id": "a3jM0000001keW8IAI"
}
```

### Response codes

| HTTP Status code |       Error message code        |    Description     |
| :--------------: | :-----------------------------: | :----------------: |
|       201        |                                 |      Created       |
|       422        | UNABLE_TO_CREATE_PAYMENT_METHOD | Customer not found |

## Delete a Payment Method

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer/{customerId}/payment-method/{paymenMethodId}`
- METHOD: `DELETE`

### Example request

```bash
curl -X DELETE \
  https://services.truphone.com/esim/v1/customer/a0xM0000004yhOV/payment-method/a3jM0000001keW8IAI
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Response codes

| HTTP Status code |       Error message code       |       Description        |
| :--------------: | :----------------------------: | :----------------------: |
|       200        |                                |         Deleted          |
|       422        | UNABLE_TO_DELETE_PAYMENT_TOKEN |    Customer not found    |
|       422        | UNABLE_TO_DELETE_PAYMENT_TOKEN | Payment method not found |
