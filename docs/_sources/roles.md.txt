# Roles

## `RESELLER`

An API client application **outside the context of an end customer**, which resells Truphone connectivity. This role is restricted to connectivity related operations like listing available products, submitting new orders and checking sim subscription/usage data. Clients with a `RESELLER` role will typically use the API to connectivity store/management pages in contexts not exclusive to connectivity. Example: Bob purchases an eSIM with a 3GB data plan from the ACME Air company website, which presented him with this option as a plus product at the end of the flight purchase journey. Bob can use the ACME Air company website or a dedicated app to check his eSIM Data usage, and will later be billed by ACME Air company. Bob has no direct relation with Truphone.

**Entitled API resources**:
* `order`
* `products`
* `sim`
* `subscriptions`

## `ACCOUNT_MANAGER`

An API client application, which can authenticate **on behalf of an end customer**, This role allows the application to manage connectivity and customer related data. Clients with an `ACCOUNT_MANAGER` role typically will develop applications where users can purchase connectivity and register their accounts with Truphone, for managing their profile information like email, name, billing address etc. Example: Alice purchases a connectet camera from the ACME IoT Camera Store. When later using the camera for the first time, Later on, Alice creates an account in the ACME IoT Connectivity Portal, activates her camera's eSIM, and adds a 3GB data plan to it. Alice is a Truphone customer, and therefore will be billed by Truphone.

**Entitled API resources**:
* `order`
* `products`
* `sim`
* `subscriptions`
* `customer`
* `notifications`
