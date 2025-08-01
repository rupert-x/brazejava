
### List User's Subscription Group - SMS <a name="list"></a>

> Use this endpoint to list and get the subscription groups of a certain user. 
  

To use this endpoint, you’ll need to generate an API key with the `subscription.groups.get` permission.

If there are multiple users (multiple external IDs) who share the same email address, all users will be returned as a separate user (even if they have the same email address or subscription group).

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

**API Endpoint**: `GET /subscription/user/status`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `external_id` | ✗ | (Required*) String  The `external_id` of the user (must include at least one and at most 50 `external_ids`). | `"{{external_id}}"` |
| `limit` | ✗ | (Optional) Integer  The limit on the maximum number of results returned. Default (and max) limit is 100. | `100` |
| `offset` | ✗ | (Optional) Integer  	Number of templates to skip before returning the rest of the templates that fit the search criteria. | `1` |
| `phone` | ✗ | (Required*) String in [E.164](https://en.wikipedia.org/wiki/E.164) format  The phone number of the user. Must include at least one phone number (with a max of 50). | `"+11112223333"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.subscription.user.status.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.subscription().user().status().list(ListRequest
                .builder()
                .externalId("{{external_id}}")
                .limit(100)
                .offset(1)
                .phone("+11112223333")
                .build());
```
