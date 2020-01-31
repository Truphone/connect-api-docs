# Products

## Product resource

A sellable/purchaseable connectivity unit. Each API client is entitled to its own product catalog. Typical connectivity storefronts are built by requesting the list of products available and then placing an [order](orders.md) with the desired product ids.

Currently, the product catalog of an API client typically changes by requesting Truphone directly, which can eventually happen outside the app development loop. Moreover, due to compatibility reasons, the product id format might change in the future and therefore, developers are discouraged from caching the results of requests to this endpoint.

### Properties

|   Property Name    |             Description             |
| :----------------: | :---------------------------------: |
|         id         |             Identifier              |
|        name        |                Name                 |
|    description     |             Description             |
|       period       |          Product duration           |
|     data.value     |            Data capacity            |
|     data.unit      |              Data unit              |
|     footprint      |  Countries where the product works  |
|  active_countries  | Countries where the product is sold |
| pricing.\$CURRENCY |     Product Price per currency      |

## Get the Product Catalog

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `/v1/product`
- METHOD: `GET`

### Parameters

| Parameter Name |                 Description                  | Required | Default |
| :------------: | :------------------------------------------: | :------: | :-----: |
|    currency    | The currency in which the price is presented |    no    |   EUR   |

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/products?currency=USD \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
[
  {
    "id": "a3m*********gIAK",
    "name": "PrePaid Data 3GB 30-Day",
    "description": "PrePaid Data 3GB 30-Day",
    "period": 30,
    "data": {
      "value": 3,
      "unit": "GB"
    },
    "footprint": ["AG", "...", "VN"],
    "activeCountries": ["ALL"],
    "pricing": {
      "USD": 42.0
    }
  }
]
```

## Get the Product's Details

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `/v1/product/{id}`
- METHOD: `GET`

### Parameters

| Parameter Name |                 Description                  | Required | Default |
| :------------: | :------------------------------------------: | :------: | :-----: |
|    currency    | The currency in which the price is presented |    no    |   EUR   |

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/products/ZHNhZGFzZGFz/?currency=USD \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
{
  "id": "a3m*********gIAK",
  "name": "PrePaid Data 3GB 30-Day",
  "description": "PrePaid Data 3GB 30-Day",
  "period": 30,
  "data": {
    "value": 3,
    "unit": "GB"
  },
  "footprint": ["AG", "...", "VN"],
  "activeCountries": ["ALL"],
  "pricing": {
    "USD": 42.0
  }
}
```
