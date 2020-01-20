# Conventions

Standards and conventions shared by all endpoints

## Headers

- **X-Correlation-ID**: In order to easily identify a request on all of Truphone's subsystems, we require that requesters create a unique identifier that will be sent on every request headers when (`X-Correlation-ID`) using the api. This way we can easily identify a request or a sequence of events between both Truphone and the requester.


## Dates
Dates in requests and responses are treated and stored in the UTC timezone.


## Errors

All errors thrown by Truphone Connect API use the same data model in order to facilitate error handling:

```javascript
{
  "type": "ERROR_TYPE",
  "messages": [
    "error_message_1",
    "error_message_2",
    "..."
  ]
}
```

**Shared error types**

Common error types, shared by all endpoints

- `INVALID_HTTP_MESSAGE` (400) - Parsing of the HTTP request has failed. Usually there's a syntax error in either the JSON body or one of the JSON fields such as dates. 
- `INVALID_REQUEST_PARAMS` (400) - Request was parsed successfully but it contains semantic errors like missing required fields or invalid content like non existing currencies or countries.
- `UNAUTHORISED` (401) - OAuth2 token is missing invalid.
- `ACCESS_DENIED` (403) - Client is trying to access a resource that it doesn't own like esim profiles or customer accounts from other clients.
- `INTERNAL_ERROR` (500) - Something went wrong with the request and the API can't recover. These should not happen on normal circumstances, and partners are advised to report back to Truphone, with the correlation id that generated such error.



