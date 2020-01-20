# Subscription Resource

A data allowance

**Properties**

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

## Subscription details [NOT IMPLEMENTED]

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/subscription/{subscriptionId}`
- METHOD: `GET`

**Example request**

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/subscription/MzEyMzMwOTIxNzgzZDIK \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

**Example response**

```javascript
{
    "status": "DEPLETED",
    "id": "Njc1NzY1NzY1ZDIK",
    "initialBalance": "314572800",
    "spentBalance": "314572800",
    "activationDate": "2019-08-01T09:09:33Z",
    "expirationDate": "2019-08-02T09:09:33Z",
    "product" : {
      "id":"MzA5MjE3ODMwOTEyCg==",
      "name": "Prepaid data 30GB"
    },
    "autoRenewFirstSubscriptionId": "MzEyMzMwOTIxNzgzZDIK",
    "auto_renew": true
}
```

## Subscription details update [NOT IMPLEMENTED]

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/subscription/{subscriptionId}/activate`
- METHOD: `PATCH`

Update the properties of a given subscription. currently only supports toggling the auto renew state.

**Example request**

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

## Subscription activation

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/subscription/{subscriptionId}/activate`
  - [Deprecated] `v1/status/subscription/{subscriptionId}/activate`
- METHOD: `POST`

**Example request**

```bash
curl -X POST \
  https://services.truphone.com/esim/v1/subscription/Njc1NzY1NzY1ZDIK/activate \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```
