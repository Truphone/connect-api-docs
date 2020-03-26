# Subscriptions

## Subscription resource

A connectivity plan subscription, associated to a Truphone SIM/Subscriber. In order to add subscriprions to a SIM, API users must first place an order using the [order](orders.md) resource.

### Properties

|        Property Name         |                           Description                           |
| :--------------------------: | :-------------------------------------------------------------: |
|              id              |                   The subscription identifier                   |
|            status            |                     The subscription status                     |
|        initialBalance        |           The subscription initial capacity in bytes            |
|         spentBalance         |            The subscription spent capacity in bytes             |
|        activationDate        | The date when the subscription was or will activate (ISO 8601)  |
|        expirationDate        | The date whe the subscription expired or will expire (ISO 8601) |
|         createdDate          |   The date whe the subscription was first created (ISO 8601)    |
|          product.id          |                     The original product id                     |
|         product.name         |                    The original product name                    |

**Possible values for `status`**

| Property Name |                     Description                     |
| :-----------: | :-------------------------------------------------: |
|   DEPLETED    |     Subscription ednded because data is used up     |
|    ACTIVE     |            Subscription is still active             |
|    EXPIRED    | Subscription expired because expiry date has passed |

## Get the Subscription Details

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `v1/subscription/{subscriptionId}`
- METHOD: `GET`

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/subscription/MzEyMzMwOTIxNzgzZDIK \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
{
  "status": "DEPLETED",
  "id": "Njc1NzY1NzY1ZDIK",
  "initialBalance": "314572800",
  "spentBalance": "314572800",
  "activationDate": "2019-08-01T09:09:33Z",
  "expirationDate": "2019-08-02T09:09:33Z",
  "product": {
    "id": "MzA5MjE3ODMwOTEyCg==",
    "name": "Prepaid data 30GB"
  }
}
```

## Activate Subscriptions

Orders can be placed for plans with activation dates in the future. The end user has the option to override those dates by activating a plan. This will change the activation date to now() and the plan will become active shortly after this endpoint being called

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL:
  - `v1/subscription/{subscriptionId}/activate`
  - `v1/status/subscription/{subscriptionId}/activate` [Deprecated]
- METHOD: `POST`

### Example request

```bash
curl -X POST \
  https://services.truphone.com/esim/v1/subscription/Njc1NzY1NzY1ZDIK/activate \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

## Get SIM Subscriptions

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL:
  - `v1/sim/{iccid}/subscriptions`
  - `v1/status/subscriptions?iccid={iccid}` [Deprecated]
- METHOD: `GET`

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/sim/8944474600000109251/subscriptions \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
[
  {
    "status": "DEPLETED",
    "id": "Njc1NzY1NzY1ZDIK",
    "initialBalance": "314572800",
    "spentBalance": "314572800",
    "activationDate": "2019-08-01T09:09:33Z",
    "expirationDate": "2019-08-02T09:09:33Z",
    "product": {
      "id": "MzA5MjE3ODMwOTEyCg==",
      "name": "Prepaid data 30GB"
    }
  }
]
```

## Get SIM Subscriptions by filtering

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL:
  - `v1/subscriptions`
- Allowed filters (in the form of query parameters):
    - iccid
    - email
    - product-id
    - before (date in the format yyyy-MM-dd'T'HH:mm:ssZ)
    - after (date in the format yyyy-MM-dd'T'HH:mm:ssZ)
    - size (for pagination purposes)
    - page (for pagination purposes)
- METHOD: `GET`

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/subscriptions?before=2020-04-24T15:39:02.002Z&size=10&page=2 \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
[
    {
        "id": "a3pM0000000npCoIAI",
        "subscriptionId": "901672804",
        "quotaId": "901672804",
        "activationDate": "2020-04-01T12:00:00Z",
        "expirationDate": "2020-04-16T12:00:00Z",
        "msisdn": "447559451024448",
        "iccid": "8944478600000244484",
        "allowanceId": "a3mM0000000dglEIAQ",
        "allowanceName": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
        "createdDate": "2020-03-19T15:51:41Z",
        "clientId": "TRUPHONEINTERNAL",
        "imei": "123456778",
        "autoRenew": "false"
    },
    {
        "id": "a3pM0000000nqCEIAY",
        "subscriptionId": "901673109",
        "quotaId": "901673109",
        "activationDate": "2020-03-24T12:55:46Z",
        "expirationDate": "2020-04-08T12:55:46Z",
        "msisdn": "447559451024659",
        "iccid": "8944478600000246596",
        "allowanceId": "a3mM0000000dglEIAQ",
        "allowanceName": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
        "createdDate": "2020-03-24T12:55:54Z",
        "clientId": "TRUPHONEINTERNAL",
        "imei": "123456789",
        "autoRenew": "false"
    },
    {
        "id": "a3pM0000000nqCJIAY",
        "subscriptionId": "901673110",
        "quotaId": "901673110",
        "activationDate": "2020-03-24T12:58:17Z",
        "expirationDate": "2020-04-08T12:58:17Z",
        "msisdn": "447559451024660",
        "iccid": "8944478600000246604",
        "allowanceId": "a3mM0000000dglEIAQ",
        "allowanceName": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
        "createdDate": "2020-03-24T12:58:21Z",
        "clientId": "TRUPHONEINTERNAL",
        "imei": "123456789",
        "autoRenew": "false"
    },
    {
        "id": "a3pM0000000nqCOIAY",
        "subscriptionId": "901673111",
        "quotaId": "901673111",
        "activationDate": "2020-03-24T13:00:07Z",
        "expirationDate": "2020-04-08T13:00:07Z",
        "msisdn": "447559451024659",
        "iccid": "8944478600000246596",
        "allowanceId": "a3mM0000000dglEIAQ",
        "allowanceName": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
        "createdDate": "2020-03-24T13:00:09Z",
        "clientId": "TRUPHONEINTERNAL",
        "imei": "123456789",
        "autoRenew": "false"
    },
    {
        "id": "a3pM0000000nqSTIAY",
        "subscriptionId": "901673304",
        "quotaId": "901673304",
        "activationDate": "2020-03-25T16:39:42Z",
        "expirationDate": "2020-04-09T16:39:42Z",
        "msisdn": "447559451024748",
        "iccid": "8944478600000247487",
        "allowanceId": "a3mM0000000dglEIAQ",
        "allowanceName": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
        "createdDate": "2020-03-25T16:39:47Z",
        "clientId": "TRUPHONEINTERNAL",
        "imei": "123456789",
        "autoRenew": "false"
    },
    {
        "id": "a3pM0000000nqSiIAI",
        "subscriptionId": "901673307",
        "quotaId": "901673307",
        "activationDate": "2020-03-25T17:46:09Z",
        "expirationDate": "2020-04-09T17:46:09Z",
        "msisdn": "447559451024747",
        "iccid": "8944478600000247479",
        "allowanceId": "a3mM0000000dglEIAQ",
        "allowanceName": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
        "createdDate": "2020-03-25T17:46:13Z",
        "clientId": "TRUPHONEINTERNAL",
        "imei": "123456789",
        "autoRenew": "false"
    }
]
```