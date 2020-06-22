# Environments

Truphone provides a Production and a Pre-Production environments for the Connect API. Usage examples will work for all environments and it will be possible to install profiles and test connectivity on end devices.

## Production

Base URL: https://services.truphone.com/connect-api

Base URL: https://services.truphone.com/esim [DEPRECATED]

The main environment. Should only be used for live traffic. Releases on this environment happen on a scheduled basis and will be communicated to partners.

## Pre-Production

Base URL: https://services.truphone.com/connect-api-preprod

The Pre-Production environment was created to replace the Staging environment. It has production grade support and throughput, but the data will not be shared with the production environment. The main goal is to allow App developers to develop and test integration with the Connect API, as well as to execute connectivity tests. A few considerations to have when using Pre-Production:
- SIM, Subscription and Customer Data is isolated from Production
- The product catalogs are shared between Production and Pre-Production
- Pre-production will still use test sims and the current commercial agreements and rules around resource recycling will be kept
- In order to access the pre-production environment you can use same the same credentials as production
- Resources are Recycled in order to optimise usage and reduce storage needs of the environment. As such, every day at 4am GMT the system will clean all resources which have not been used for 72 hours.


	


 

