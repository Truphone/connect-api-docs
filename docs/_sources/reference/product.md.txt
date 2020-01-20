# Product Resource

A sellable connectivity unit

**Properties**

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

## Product list

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `/v1/product`
- METHOD: `GET`
- PARAMETERS:

| Parameter Name |                 Description                  | Required | Default |
| :------------: | :------------------------------------------: | :------: | :-----: |
|    currency    | The currency in which the price is presented |    no    |   EUR   |

**Example request**

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/products?currency=USD \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

**Example response**

```javascript
[
  {
    id: "a3m*********gIAK",
    name: "PrePaid Data 3GB 30-Day",
    description: "PrePaid Data 3GB 30-Day",
    period: 30,
    data: {
      value: 3,
      unit: "GB"
    },
    footprint: ["AG", "...", "VN"],
    activeCountries: ["ALL"],
    pricing: {
      USD: 42.0
    }
  }
  // .. more products
];
```

## Product details [NOT IMPLEMENTED]

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `/v1/product/{id}`
- METHOD: `GET`
- PARAMETERS:

| Parameter Name |                 Description                  | Required | Default |
| :------------: | :------------------------------------------: | :------: | :-----: |
|    currency    | The currency in which the price is presented |    no    |   EUR   |

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/products/ZHNhZGFzZGFz/?currency=USD \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

**Example response**

```javascript
{
    "id":"a3m*********gIAK",
    "name":"PrePaid Data 3GB 30-Day",
    "description":"PrePaid Data 3GB 30-Day",
    "period":30,
    "data":{
        "value":3,
        "unit":"GB"
    },
    "footprint":[
        "AG",
        "...",
        "VN"
    ],
    "activeCountries":[
        "ALL"
    ],
    "pricing":{
        "USD":42.0
    },
}
```
