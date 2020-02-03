# Deployment Schedule

Dates and changelog for major API releases. New versions are made available in the staging environment 2 weeks in advance to allow partners to test their integrations. "Estimated dates" will change to "Confirmed dates" 2 days before deployment if the deployment is to proceed.

## 5.4.0 - Product catalog update

- Estimated date: 10th February 10:00 UTC
- Downtime: 0
- Retocompatible: yes
- Changes:
  - New product footprint will be added to some partners
  - Existing products will be removed
- Notes:
  - This will be a breaking change if the product catalogue is cached on the partner side
  - Please ensure product catalogues are not cached, or if so the catalogue is refreshed frequently
  - Truphone will email partners before and after change completion

## 5.5.0 - IoT Features

- Estimated date: 17th February 10:00 UTC
- Downtime: 0
- Retocompatible: yes
- Changes:
  - New endpoints for IoT partners

## 5.6.0 - Auto renew and subscriptions

- Estimated date: 2nd March 10:00 UTC
- Downtime: 0
- Retocompatible: yes
- Changes:
  - Support for auto renewable subscriptions
  - Support for plan expiry and 80% usage notifications
