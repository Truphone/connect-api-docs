# Notifications

The Connect API supports sending several types of notifications when significant events happen in the backend. In order to be able to receive notifications, the end customer must first set his notification preferences. Currently all of the notifications are associated with the SIM, and therefore, subscription is made via the [`sim`](sims.md) resource.

## Receiving Webhook Notifications

In order to handle webhook notifications, API clients will need to implement an endpoint that supports `POST` requests with the payloads described below:

### Usage Threshold

Usage Threshold Notification is currently being sent at 80% plan depletion

|  Property Name  |    Description    |
| :-------------: | :---------------: |
|       id        |    Identifier     |
|      type       | Notification type |
|      iccid      | SIM Profile ICCID |
| subscription_id |  subscription_id  |
|    threshold    |   Data capacity   |

#### Example Request Payload

```json
{
  "id": "1234-56789",
  "type": "USAGE_THRESHOLD",
  "iccid": "893000000002391231",
  "subscription_id": "ZHNhc2Rhc2Q="
}
```

### Subscription End

Subscription end notification is currently being sent when plan expires by time or by data depletion

|  Property Name  |    Description    |
| :-------------: | :---------------: |
|       id        |    Identifier     |
|      type       | Notification type |
|      iccid      | SIM Profile ICCID |
| subscription_id |  subscription_id  |

#### Example Request Payload

```json
{
  "id": "1234-56789",
  "type": "SUBSCRIPTION_END",
  "iccid": "893000000002391231",
  "subscription_id": "ZHNhc2Rhc2Q=",
  "threshold": 80
}
```
