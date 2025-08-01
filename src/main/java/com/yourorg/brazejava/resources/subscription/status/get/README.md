
### List User's  Subscription Group Status - SMS <a name="list"></a>

> Use this endpoint to get the subscription state of a user in a subscription group. 
  

To use this endpoint, you’ll need to generate an API key with the `subscription.status.get` permission.

These groups will be available on the **Subscription Group** page. The response from this endpoint will include the external ID and either subscribed, unsubscribed, or unknown for the specific subscription group requested in the API call. This can be used to update the subscription group state in subsequent API calls or to be displayed on a hosted web page.

\*Either `external_id` or `phone` are required. When both are submitted, only the external_id is used for querying and the phone number is applied to that user.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

All successful responses will return `subscribed`, `unsubscribed`, or `unknown` depending on status and user history with the subscription group.

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "status": {
    "1": "Unsubscribed",
    "2": "Subscribed"
  },
  "message": "success"
}

```

**API Endpoint**: `GET /subscription/status/get`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `external_id` | ✗ | (Required*) String  The `external_id` of the user (must include at least one and at most 50 `external_ids`).  When both an `external_id` and `phone` are submitted, only the external_id(s) provided will be applied to the result query.  | `"{{external_identifier}}"` |
| `phone` | ✗ | (Required*) String in [E.164](https://en.wikipedia.org/wiki/E.164) format  The phone number of the user (must include at least one phone number and at most 50 phone numbers). | `"+11112223333"` |
| `subscription_group_id` | ✗ | (Required) String  The `id` of your subscription group. | `"{{subscription_group_id}}"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.subscription.status.get.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.subscription().status().get().list(ListRequest
                .builder()
                .externalId("{{external_identifier}}")
                .phone("+11112223333")
                .subscriptionGroupId("{{subscription_group_id}}")
                .build());
```
