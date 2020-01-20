# Notification Preferences Resource

The Connect API supports sending several types of notifications when significant events happen in the backend. In order to be able to receive notifications, the user must first set his notification preferences. Currently all of the notifications are associated with the SIM, and therefore, subscription is made via the [`sim`](sim.md) resource.

**Properties**

| Property Name |                    Description                    |
| :-----------: | :-----------------------------------------------: |
|     type      |             the type of notification              |
|  webhook_url  | The url to call if this notification is a webhook |

**Possible notification types**

| Notification Type |                       Description                        |
| :---------------: | :------------------------------------------------------: |
| SUBSCRIPTION_END  |          A subscription has depleted or expired          |
|  USAGE_THRESHOLD  |             A subscription reached 80% usage             |
|   AUTO_RENEWED    | A new subscription was purchased to renew a depleted one |


## Webhook notifications

Currently the only type of notification supported, the webhook notification requires the developer to set up a public endpoint, to which the connect API will `POST` a notification.

**Shared notification payload**

| Property Name |    Description    |
| :-----------: | :---------------: |
|      id       |    Identifier     |
|     type      | Notification type |

**Usage Threshold notification**

|  Property Name  |    Description    |
| :-------------: | :---------------: |
|      iccid      | SIM Profile ICCID |
| subscription_id |  subscription_id  |
|    threshold    |   Data capacity   |

**Subscription End notification**

|  Property Name  |    Description    |
| :-------------: | :---------------: |
|      iccid      | SIM Profile ICCID |
| subscription_id |  subscription_id  |

**Auto Renew notification**

|    Property Name    |     Description     |
| :-----------------: | :-----------------: |
|        iccid        |  SIM Profile ICCID  |
|   subscription_id   |   subscription_id   |
| new_subscription_id | new_subscription_id |

**Example payloads**
```javascript
{
    "id": "1234-56789",
    "type": "SUBSCRIPTION_END",
    "iccid": 893000000002391231,
    "subscription_id": "ZHNhc2Rhc2Q="
}

{
    "id": "1234-56789",
    "type": "USAGE_THRESHOLD",
    "iccid": 893000000002391231,
    "subscription_id": "ZHNhc2Rhc2Q=",
    "threshold": 80
}

{
    "id": "1234-56789",
    "type": "AUTO_RENEW",
    "iccid": 893000000002391231,
    "subscription_id": "ZHNhc2Rhc2Q="
    "auto_renew_subscription_id": "ZHNhc2Rhc2kjhkhQ="
}
```
