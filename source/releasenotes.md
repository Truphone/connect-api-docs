# Release Notes

## 5.5.0 - 27th February 10:00 UTC

- Changes:
  - `product_id` now accepted instead of the deprecated allowanceId
  - Removed the protocol part from the `smdpUrl` field of the order response
  - Partial support for webhook notifications. It is now possible to register webhook urls per SIM/event type. Notifications are still not being sent though.
  - General API stability improvements and bugfixes 

## 5.4.0 - 13th February 14:00 UTC

- Changes:
  - New product footprint will be added to some partners
  - Existing products will be removed
- Notes:
  - Product ids have changed. Please ensure product catalogues are not cached, or if so the catalogue is refreshed frequently