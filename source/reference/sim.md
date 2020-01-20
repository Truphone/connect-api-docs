# SIM Resource

A Truphone network profile.

**Properties**

| Property Name  |                  Description                  |
| :------------: | :-------------------------------------------: |
|     iccid      |             The SIM profile ICCID             |
|  matching_id   |    The profile activation code (eSIM only)    |
| profile_status | The install status of the profile (eSIM only) |

**Possible values for `profile_status`**

|   Status    |               Description               |
| :---------: | :-------------------------------------: |
|  Released   | Ready to be reinstalled by the customer |
| Downloaded  | Downloaded in eUICC of customer device  |
|  Installed  |  Installed in eUICC of customer device  |
| Unavailable |  Deleted from eUICC of customer device  |

## SIM details

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/sim/{iccid}`
  - [Deprecated] `v1/status/sim/{iccid}`
- METHOD: `GET`

**Example Request**

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/sim/8944474600000109251 \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

**Example response**

```javascript
{
  "iccid": "8944474600000063847",
  "matching_id": "O-17QF0-MJVBIN",
  "profile_status": "Released"
}
```

## SIM Subscriptions

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/sim/{iccid}/subscriptions`
  - [Deprecated] `v1/status/subscriptions?iccid={iccid}`
- METHOD: `GET`

**Example request**

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/sim/8944474600000109251/subscriptions \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

**Example response**

```javascript
[
  {
    status: "DEPLETED",
    id: "Njc1NzY1NzY1ZDIK",
    initialBalance: "314572800",
    spentBalance: "314572800",
    activationDate: "2019-08-01T09:09:33Z",
    expirationDate: "2019-08-02T09:09:33Z",
    product: {
      id: "MzA5MjE3ODMwOTEyCg==",
      name: "Prepaid data 30GB"
    },
    autoRenewFirstSubscriptionId: "MzEyMzMwOTIxNzgzZDIK"
  }
  // more subscriptions
];
```

## SIM notification preferences [NOT IMPLEMENTED]

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/sim/{iccid}/notification_preferences`
- METHOD: `GET`

**Example request**

```bash
curl -X GET \
  https://services.truphone.com/esim/v1/sim/8944474600000109251/notification_preferences \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

**Example response**

```javascript
[
  {
    type: "SUBSCRITPION_END"
    webhook_url: "http://acme-flights.com/notifications/handler"
  }
  // more active notification subscriptions
];
```

## Register for notifications [NOT IMPLEMENTED]

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/sim/{iccid}/notification_preferences/{type}`
- METHOD: `POST`
- PARAMETERS:

| Parameter Name |                                Description                                 | Required | Default |
| :------------: | :------------------------------------------------------------------------: | :------: | :-----: |
|  webhook_url   | A webhook url to call. Currently the only supported notification supported |    no    |   --    |

**Example request**

```bash
curl -X POST \
  https://services.truphone.com/esim/v1/sim/8944474600000109251/notification_preferences/SUBSCRIPTION_END \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
   -d '{
       "webhook_url": http://acme-flights.com/notifications/handler
   }'
```

## Unregister from notifications [NOT IMPLEMENTED]

- Allowed roles: `ACCOUNT_MANAGER`
- URL: `v1/sim/{iccid}/notification_preferences/{type}`
- METHOD: `DELETE`

**Example request**

```bash
curl -X DELETE \
  https://services.truphone.com/esim/v1/sim/8944474600000109251/notification_preferences/SUBSCRIPTION_END \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```
