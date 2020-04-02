# Release Notes


## 5.8.0

- **Staging release date**: 13th April 2020
- **Production release date**: 27th April 2020
- **Changes**
  - Removing and deprecating certain unused parameters in the order API:
    - Remove `dataValue` and `dataUnit` from order request – reason: not applicable to current use-cases
    - Added `id` parameter to order response – this parameter will possess the same value as current “externalId” and should be used instead of it
    - Deprecating `externalId` in order response – parameter will still be available in the response but it will be removed in a future release please migrate to the new `id` parameter
- **Breaking Changes**
    - Removing `type` from subscription response – reason: not applicable to current use-cases
- **Docs**
    - [Get subscriptions history for a specific esim profile](#https://truphone.github.io/connect-api-docs/reference/subscriptions.html#get-sim-subscriptions)
    - [Query for subscription history](#https://truphone.github.io/connect-api-docs/reference/subscriptions.html#get-sim-subscriptions-by-filtering)


## 5.7.0

- **Staging release date**: 30th March 2020
- **Production release date**: 13th April 2020
- **Changes**
  - API now has the the capability to get subscription history, this can be requested per esim profile or fetching the history for the entire user-base:
    - Getting subscription history for a specific profile 
    - Getting subscription history for the entire user-base using filters (afterDate, beforeDate, iccd, product-id, email, etc)
- **Docs**
    - [Get subscriptions history for a specific esim profile](#https://truphone.github.io/connect-api-docs/reference/subscriptions.html#get-sim-subscriptions)
    - [Query for subscription history](#https://truphone.github.io/connect-api-docs/reference/subscriptions.html#get-sim-subscriptions-by-filtering)


## 5.6.0

- **Staging release date**: 3rd March 2020
- **Production release date**: 17h March 2020
- **Changes**
  - API now supports registering/unregistering to received 80% usage threshold and end of plan notifications on subscriptions. This can be used to let customers know their plan is ending or upsell a new plan to customers.
- **Docs**
    - [Register for notifications](#https://truphone.github.io/connect-api-docs/reference/sims.html#register-for-notifications)
    - [Unregister from notifications](#https://truphone.github.io/connect-api-docs/reference/sims.html#unregister-from-notifications)
    - [Receive notifications](#https://truphone.github.io/connect-api-docs/reference/notifications.html)


## 5.5.0 - 27th February 10:00 UTC

- **Staging release date**: 3rd March 2020
- **Production release date**: 17h March 2020
- **Changes**:
  - `product_id` now accepted instead of the deprecated allowanceId
  - Removed the protocol part from the `smdpUrl` field of the order response
  - Partial support for webhook notifications. It is now possible to register webhook urls per SIM/event type. Notifications are still not being sent though.
  - General API stability improvements and bugfixes 


## 5.4.0 - 13th February 14:00 UTC

- **Staging release date**: 4th February 2020
- **Production release date**: 13th February 2020
- **Changes**:
  - New product footprint will be added to some partners
  - Existing products will be removed
- **Notes**:
  - Product ids have changed. Please ensure product catalogues are not cached, or if so the catalogue is refreshed frequently