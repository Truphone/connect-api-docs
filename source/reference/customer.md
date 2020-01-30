# Customer

A Truphone connectivity end user

**Properties**

|   Property Name    |                Description                |
| :----------------: | :---------------------------------------: |
|       email        |               Email address               |
|        type        |   Customer type (BUSSINESS or PERSONAL)   |
|     firstName      |                First Name                 |
|      lastName      |                 Last Name                 |
|      language      |                 Language                  |
| countryOfResidence |           Country of Residence            |
|    phoneNumber     |               Phone Number                |
|  defaultCurrency   |            Preferred Currency             |
|   billingAddress   | Billing Address (see Address Properties)  |
|  shippingAddress   | Shipping Address (see Address Properties) |
|    companyName     |    Company name for BUSINESS customers    |
|   companyNumber    |  Employee number for BUSINESS customers   |
|      jobTitle      |     Job title for BUSINESS customers      |

**Address Properties**

| Property Name  |   Description    |
| :------------: | :--------------: |
| streetAddress1 | Street Address 1 |
| streetAddress2 | Street Address 2 |
|      city      |       City       |
|     state      |      State       |
|    postCode    |    Post Code     |
|    country     |     Country      |

## Creating a new customer

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer`
- METHOD: `POST`

### Example Request

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
        "companyName": "TruExample",
        "companyNumber": "123456789",
        "jobTitle": "Software Engineer",
        "billingAddress" : {
          "streetAddress1" : "25 Cobbleton Square Appartments",
          "streetAddress2" : "Cupertino",
          "city": "San Jose",
          "state": "California",
          "postCode": "12345",
          "country": "United States"
        },
        "shippingAddress" : {
          "streetAddress1" : "25 Cobbleton Square Appartments",
          "streetAddress2" : "Cupertino",
          "city": "San Jose",
          "state": "California",
          "postCode": "12345",
          "country": "United States"
        },
      }'
```



## Retrieving customer details

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer`
- METHOD: `GET`

### Input parameters

| Parameter Name | Mandatory | Default Value |
| :------------: | :-------: | :-----------: |
|     email      |    yes    |               |

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/customer?email=john@doe.com
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
{
  "id": "29asdaA3801b4789asdA235=",
  "email": "john@doe.com",
  "firstName": "John",
  "lastName": "Doe",
  "countryOfResidence": "US",
  "language": "EN",
  "phoneNumber": "0044102938120",
  "defaultCurrency": "EUR",
  "type": "BUSINESS",
  "companyName": "TruExample",
  "companyNumber": "123456789",
  "jobTitle": "Software Engineer",
  "billingAddress": {
    "streetAddress1": "25 Cobbleton Square Appartments",
    "streetAddress2": "Cupertino",
    "city": "San Jose",
    "state": "California",
    "postCode": "12345",
    "country": "United States"
  },
  "shippingAddress": {
    "streetAddress1": "25 Cobbleton Square Appartments",
    "streetAddress2": "Cupertino",
    "city": "San Jose",
    "state": "California",
    "postCode": "12345",
    "country": "United States"
  }
}`
```



## Updating customer details

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/customer/{id}`
- METHOD: `PATCH`

### Input parameters

All fields are optional. Not sending a field will not change its value, and sending `null` values will delete the corresponding fields.

|   Parameter Name   | Mandatory | Default Value |
| :----------------: | :-------: | :-----------: |
|       email        |    no     |               |
|        type        |    no     |               |
|     firstName      |    no     |               |
|      lastName      |    no     |               |
|      language      |    no     |               |
| countryOfResidence |    no     |               |
|    phoneNumber     |    no     |               |
|  defaultCurrency   |    no     |               |
|      verified      |    no     |               |
|   billingAddress   |    no     |               |
|  shippingAddress   |    no     |               |
|    companyName     |    no     |               |
|   companyNumber    |    no     |               |
|      jobTitle      |    no     |               |

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
    "last_digits": "1234",
    "expiry_month": "12",
    "expiry_year": "1234",
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
|  last_digits   |    yes    |               |
|  expiry_month  |    yes    |               |
|  expiry_year   |    yes    |               |
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
            "last_digits" : "1234",
            "expiry_month" : "12",
            "expiry_year" : "1234",
            "gateway" : "TRUPHONE"
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
