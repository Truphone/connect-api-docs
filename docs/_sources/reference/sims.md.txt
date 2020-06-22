# SIM

## SIM Resource

A Truphone subscriber. Can be a physical SIM or eSIM and it holds profile related information as well as subscriber specific information. The SIM is usually tied to an individual and a device. It is a requirement to purchase any type of connectivity.

### Properties

| Property Name  |                  Description                  |
| :------------: | :-------------------------------------------: |
|     iccid      |             The SIM profile ICCID             |
|  matching_id   |    The profile activation code (eSIM only)    |
| status | The install status of the profile (eSIM only) |
| eid | The EID associated with an eSIM. It's only present if the eSIM was ordered with an EID. Only applicable in iOS (eSIM only) |
| last_modified | The date of the last status change |


**Possible values for `status`**

|   Status    |               Description               |
| :---------: | :-------------------------------------: |
|  Released   | Ready to be reinstalled by the customer |
| Downloaded  | Downloaded in eUICC of customer device  |
|  Installed  |  Installed in eUICC of customer device  |
| Unavailable |  Deleted from eUICC of customer device  |

## Get SIM details

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL:
  - `v1/sim/{iccid}`
  - `v1/status/sim?iccid={iccid}` [Deprecated]
- METHOD: `GET`

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/connect-api/v1/sim/8944474600000109251 \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
{
  "iccid": "8944474600000063847",
  "matching_id": "O-17QF0-MJVBIN",
  "status": "Released",
  "eid": "89001012012341234012345678901224",
  "last_modified": "2019-08-02T09:09:33Z"
}
```

## SIM Preferences Resource

SIM profiles/subscribers allow configuration of specific preferences which enable/disable features during the connectivity lifecycle. Currently, the only preference we support is registering/unregistering for usage and depletion notifications.

## Get SIM Preferences

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `v1/sim/{iccid}/preferences`
- METHOD: `GET`

### Example Request

```bash
curl -X GET \
  https://services.truphone.com/connect-api/v1/sim/8944474600000109251/preferences \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```

### Example Response

```json
{
  "notifications": [
    {
      "type": "SUBSCRITPION_END",
      "webhook_url": "http://acme-flights.com/notifications/handler"
    },
    {
      "type": "USAGE_THRESHOLD",
      "webhook_url": "http://acme-flights.com/notifications/handler"
    }
  ]
}
```

## Register for notifications

Currently, the only form of notification we support is through webhooks. Each SIM can be registerd for receiving the different types of notifications individually. For information on the notification format, check the [notifications](notifications.md) document

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `v1/sim/{iccid}/preferences/notifications/{type}`
- METHOD: `POST`

### Parameters

| Parameter Name |                                                     Description                                                      | Required | Default |
| :------------: | :------------------------------------------------------------------------------------------------------------------: | :------: | :-----: |
|      type      | The type of notification to subscribe to.<br>Must be one of the following:<br> `SUBSCRITPION_END`, `USAGE_THRESHOLD` |   yes    |   --    |
|  webhook_url   |                                                A webhook url to call                                                 |   yes    |   --    |

### Example request

```bash
curl -X POST \
  https://services.truphone.com/connect-api/v1/sim/8944474600000109251/preferences/notifications/SUBSCRIPTION_END \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
   -d '{
       "webhook_url": http://acme-flights.com/notifications/handler
   }'
```

## Unregister from notifications

- Allowed roles: `RESELLER`, `ACCOUNT_MANAGER`
- URL: `v1/sim/{iccid}/notification_preferences/{type}`
- METHOD: `DELETE`

### Example request

```bash
curl -X DELETE \
  https://services.truphone.com/connect-api/v1/sim/8944474600000109251/preferences/notifications/SUBSCRIPTION_END \
   -H "Authorization: Bearer $ACCESS_TOKEN" \
   -H 'Cache-Control: no-cache' \
   -H 'Content-Type: application/json' \
   -H 'X-Correlation-ID: unique-id-from-requester-123'
```
