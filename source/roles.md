# Roles

## `RESELLER`

An API client application **outside the context of an end customer**, which can resell Truphone connectivity. This role is restricted to non-personal data like a product catalog or account creation. Clients with a `RESELLER` role will typically use the API to build a storefront and a checkout page. Example: ACME Air company sells Truphone connectivity at the end of the flight ticket purchase journey.

**Entitled API resources**:
* `order`
* `products`

## `ACCOUNT_MANAGER`

An API client application, authenticated **on behalf of an end customer**, which can purchase Truphone connectivity, but also manage the account data of the authenticated customer. Clients with an `ACCOUNT_MANAGER` role typically implement profile and subscription management pages in addition to the `RESELLER` functionality. Example: Alice creates an account after purchasing Truphone connectivity on the ACME Air company website. She then logs in to her account and is able to topup her data plan, check the current data usage, add/remove payment methods and change her billing address.

**Entitled API resources**:
* `order`
* `products`
* `sim`
* `subscriptions`
* `customer`
* `notifications`
