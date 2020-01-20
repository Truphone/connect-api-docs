# Roles

## `RESELLER`

An API client application **outside the context of an end customer**, which resells Truphone connectivity. This role is restricted to connectivity related operations like listing available products, submitting new orders and checking sim subscription/usage data. Clients with a `RESELLER` role will typically use the API to connectivity store/management pages in contexts not exclusive to connectivity.

**Entitled API resources**:
* `order`
* `products`
* `sim`
* `subscriptions`
* `notifications`

## `ACCOUNT_MANAGER`

An API client application, which can authenticate **on behalf of an end customer**, This role allows the application to manage connectivity and customer related data. Clients with an `ACCOUNT_MANAGER` role typically will develop applications where users can purchase connectivity and register their accounts with Truphone, for managing their profile information like email, name, billing address etc.

**Entitled API resources**:
* `order`
* `products`
* `sim`
* `subscriptions`
* `customer`
* `notifications`
