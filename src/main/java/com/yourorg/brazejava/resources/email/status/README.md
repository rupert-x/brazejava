
### Change Email Subscription Status <a name="create"></a>

> Use this endpoint to set the email subscription state for your users. Users can be `opted_in`, `unsubscribed`, or `subscribed` (not specifically opted in or out). 
  

You can set the email subscription state for an email address that is not yet associated with any of your users within Braze. When that email address is subsequently associated with a user, the email subscription state that you uploaded will be automatically set.

To use this endpoint, you’ll need to generate an API key with the `email.status` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `email` | Required | String or array | String email address to modify, or an array of up to 50 email addresses to modify. |
| `subscription_state` | Required | String | Either “subscribed”, “unsubscribed”, or “opted_in”. |

**API Endpoint**: `POST /email/status`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `EmailStatusCreateBody.builder().email("example@braze.com").subscriptionState("subscribed").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.EmailStatusCreateBody;
import com.yourorg.brazejava.resources.email.status.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.email().status().create(CreateRequest
                .builder()
                .data(EmailStatusCreateBody
                      .builder()
                      .email("example@braze.com")
                      .subscriptionState("subscribed")
                      .build())
                .build());
```
