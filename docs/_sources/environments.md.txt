# Environments

Truphone provides both Production and Staging environments for the Truphone Connect API:

- Production: services.truphone.com
- Staging: services-bit.truphone.com

Usage examples will work for both Staging and Production environments. Moreover, in both environments it is possible to install profiles and test connectivity in end devices. However, Staging is intended for developing, integrating and testing against the API and Production to provide service to real-customers at scale. 

Additionally, Staging will also recycle resources in order to optimise usage and reduce storage needs of the environment. As such, every day at 4am GMT the system will clean all resources which have not been used for two or more days. 

Please note that both environments are isolated and therefore data such as user and product ids will change from one environment to the other.