# Environments

Truphone provides both Production and Staging environments for the Truphone Connect API:
- Production (Stable):  services.truphone.com
- Staging (Release Candidate):  services-bit.truphone.com

Usage examples will work for both Staging and Production environments, however, while the Production environment will always have stable versions, Staging will sometimes contain the latest features, which might be undocumented or unstable. Additionally, Truphone is still making the required adjustments to support the end to end install of an active (connected to the cellular network) eSIM profile. 

We recommend using *Staging for testing/developing API calls and integration*, but for profile installs and *connectivity testing partners will have to use Production* until the Staging environment is ready for connectivity tests.

Please note that both environments are isolated and therefore data such as *user and product ids will change from one environment to the other*.