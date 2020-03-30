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
    - `v1/subscription`
- Allowed filters (in the form of query parameters):
    - `iccid`
    - `email`
    - `product-id`
    - `before` (date in the format yyyy-MM-dd'T'HH:mm:ssZ)
    - `after` (date in the format yyyy-MM-dd'T'HH:mm:ssZ)
    - `size` (for pagination purposes)
    - `page` (for pagination purposes)
- METHOD: `GET`
- Response might have the following headers:
    - `X-Previous-Page` (url of the previous page. Only present if there is a previous page)
    - `X-Next-Page` (url of the next page. Only present if there is a next page)

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/subscription?before=2020-04-24T15:39:02.002Z&size=10&page=2 \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
[
    {
            "id": "xoCdHNs78yvyOSmdn0eaD6FHRIO572_lPNyUxDGgLnI=",
            "activationDate": "2020-04-01T12:00:00Z",
            "expirationDate": "2020-04-16T12:00:00Z",
            "createdDate": "2020-03-19T15:51:41Z",
            "product": {
                "id": "Q-hzHc6EErZPQcgw2L02_nDdruGtr6lDrM-jmja_xuE=",
                "name": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
                "period": 0,
                "period_unit": "DAYS"
            },
            "device_id": "12345657",
            "auto_renew": "false"
        },
        {
            "id": "mEbXDbnruRowxX1ybirQK-adwS0edrvcUs4VKW9QWlM=",
            "activationDate": "2020-03-24T12:55:46Z",
            "expirationDate": "2020-04-08T12:55:46Z",
            "createdDate": "2020-03-24T12:55:54Z",
            "product": {
                "id": "Q-hzHc6EErZPQcgw2L02_nDdruGtr6lDrM-jmja_xuE=",
                "name": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
                "period": 0,
                "period_unit": "DAYS"
            },
            "device_id": "123456789",
            "auto_renew": "false"
        },
        {
            "id": "tl_6a2eO00tBm67k5l-HAqX1Oswd0gaSC-ucQRcTpcw=",
            "activationDate": "2020-03-24T12:58:17Z",
            "expirationDate": "2020-04-08T12:58:17Z",
            "createdDate": "2020-03-24T12:58:21Z",
            "product": {
                "id": "Q-hzHc6EErZPQcgw2L02_nDdruGtr6lDrM-jmja_xuE=",
                "name": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
                "period": 0,
                "period_unit": "DAYS"
            },
            "device_id": "123456789",
            "auto_renew": "false"
        },
        {
            "id": "eJWIyFew88qMPz7ymEJ1fQh6LnlniH3ixbPG0VynPYA=",
            "activationDate": "2020-03-24T13:00:07Z",
            "expirationDate": "2020-04-08T13:00:07Z",
            "createdDate": "2020-03-24T13:00:09Z",
            "product": {
                "id": "Q-hzHc6EErZPQcgw2L02_nDdruGtr6lDrM-jmja_xuE=",
                "name": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
                "period": 0,
                "period_unit": "DAYS"
            },
            "device_id": "123456789",
            "auto_renew": "false"
        },
        {
            "id": "mKDI7e30fYGKTIQwKZvYnixEhsvSQYBE2523XapjgHk=",
            "activationDate": "2020-03-25T16:39:42Z",
            "expirationDate": "2020-04-09T16:39:42Z",
            "createdDate": "2020-03-25T16:39:47Z",
            "product": {
                "id": "Q-hzHc6EErZPQcgw2L02_nDdruGtr6lDrM-jmja_xuE=",
                "name": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
                "period": 0,
                "period_unit": "DAYS"
            },
            "device_id": "123456789",
            "auto_renew": "false"
        },
        {
            "id": "p5N_LjvSxfdtVv9Rfi7nDi8zc_QPiVus6L-k6kk6lNQ=",
            "activationDate": "2020-03-25T17:46:09Z",
            "expirationDate": "2020-04-09T17:46:09Z",
            "createdDate": "2020-03-25T17:46:13Z",
            "product": {
                "id": "Q-hzHc6EErZPQcgw2L02_nDdruGtr6lDrM-jmja_xuE=",
                "name": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
                "period": 0,
                "period_unit": "DAYS"
            },
            "device_id": "123456789",
            "auto_renew": "false"
        },
        {
            "id": "yLCLVb967QI3TrCTL4vDlAes8TGQD9AFlwL6JfGVQP8=",
            "activationDate": "2020-03-26T16:26:05Z",
            "expirationDate": "2020-04-10T16:26:05Z",
            "createdDate": "2020-03-26T16:26:09Z",
            "product": {
                "id": "Q-hzHc6EErZPQcgw2L02_nDdruGtr6lDrM-jmja_xuE=",
                "name": "1GB 15-Day - Truphoneinternal - Tier2 Data Bundle",
                "period": 0,
                "period_unit": "DAYS"
            },
            "device_id": "123456789",
            "auto_renew": "false"
        }
]
```