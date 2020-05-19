# Environments

Truphone provides a Production and a Pre-Production environments for the Connect API. Usage examples will work for all environments and it will be possible to install profiles and test connectivity on end devices.

## Production

Base URL: https://services.truphone.com/connect-api
Base URL: https://services.truphone.com/esim [DEPRECATED]

The main environment. Should only be used for live traffic. Releases on this environment happen on a scheduled basis and will be communicated to partners.

## Pre-Production

Base URL: https://services.truphone.com/connect-api-preprod

The Pre-Production environment was created to replace the Staging environment. It has production grade support and throughput, but the data created in this environment will be marked as test data, and therefore will not be shared with the production environment. The main goal is to allow App developers to develop and test integration with the Connect API, as well as to execute connectivity tests. A few considerations to have when using Pre-Production:
- API Version is always the release candidate, with the next big changes to be deployed on the next release
- SIM, Subscription and Customer Data is isolated from Production and marked as Test Data
- The product catalogs are shared between Production and Pre-Production
- Pre-production will still use test sims and the current commercial agreements and rules around resource recycling will be kept
- In order to access the pre-production environment you can use same the same credentials as production
- Resources are Recycled in order to optimise usage and reduce storage needs of the environment. As such, every day at 4am GMT the system will clean all resources which have not been used for two or more days.


## Staging [DEPRECATED] - To be decommissioned by June 24th

Base URL: https://services-bit.truphone.com/connect-api
Base URL: https://services-bit.truphone.com/esim [DEPRECATED]

The Staging environment was initially intended for development and integration purposes. It is a copy of the production environment but it doesn't share any resource. This environment is currently considered in deprecation stage. We will maintain it up and running for a period of time in order to allow a smooth transition to Pre-Production.

 - Staging environment is isolated and therefore data such as user and product ids will change from one environment to the other.
 - Resources are Recycled in order to optimise usage and reduce storage needs of the environment. As such, every day at 4am GMT the system will clean all resources which have not been used for two or more days.

		

	


 

