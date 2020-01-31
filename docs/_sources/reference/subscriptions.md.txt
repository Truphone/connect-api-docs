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
| autoRenewFirstSubscriptionId |     The previous subscription, if this one is an auto renew     |
|          auto_renew          |     Whether this subscription has auto renew active or not      |

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
  },
  "autoRenewFirstSubscriptionId": "MzEyMzMwOTIxNzgzZDIK",
  "auto_renew": true
}
```

## Update the Subscription Details

Update the properties of a given subscription. Currently only supports toggling the auto renew state.

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `v1/subscription/{subscriptionId}/activate`
- METHOD: `PATCH`

### Example Request

```bash
curl -X PATCH \
  https://services.truphone.com/esim/v1/subscription/Njc1NzY1NzY1ZDIK \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
   -d '{
     "auto_renew" : true
   }'
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
    },
    "autoRenewFirstSubscriptionId": "MzEyMzMwOTIxNzgzZDIK"
  }
]
```
