# Release Notes


## 5.9.0

The release comes with one big new feature called Push Install. This adds a new profile installation method to our platform which doesn’t require a QRCode nor direct LPA integration with our SDKs. The way it works is that when ordering a new profile you can specify the EID of the target device, with this information Connect is able to send a push notification to the that same device that triggers the profile installation process for the user. At the moment this will only be supported for iOS devices but we are working on adding support for Android in the future. 

- **Production release date**: 29th June 2020
- **Changes**
  - [Support for push install via order endpoint](#https://truphone.github.io/connect-api-docs/recipes/new-esim.html#push-install-ios-only)
  - EID validation in order request
  - [Added new update endpoint for updating an EID for push install](#https://truphone.github.io/connect-api-docs/reference/sims.html#update-eid)
  - [Added LPA string to order endpoint](#https://truphone.github.io/connect-api-docs/reference/orders.html#properties)
  - [Added LPA string to sim endpoint](#https://truphone.github.io/connect-api-docs/reference/sims.html#properties)
  - General performance improvements and bug fixing 


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


## 5.5.0

- **Staging release date**: 3rd March 2020
- **Production release date**: 17h March 2020
- **Changes**:
  - `product_id` now accepted instead of the deprecated allowanceId
  - Removed the protocol part from the `smdpUrl` field of the order response
  - Partial support for webhook notifications. It is now possible to register webhook urls per SIM/event type. Notifications are still not being sent though.
  - General API stability improvements and bugfixes 


## 5.4.0

- **Staging release date**: 4th February 2020
- **Production release date**: 13th February 2020
- **Changes**:
  - New product footprint will be added to some partners
  - Existing products will be removed
- **Notes**:
  - Product ids have changed. Please ensure product catalogues are not cached, or if so the catalogue is refreshed frequently