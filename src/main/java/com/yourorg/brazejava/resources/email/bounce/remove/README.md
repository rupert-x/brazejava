
### Remove Hard Bounced Emails <a name="create"></a>

> Use this endpoint to remove email addresses from your Braze bounce list. 
  

We will also remove them from the bounce list maintained by your email provider.

To use this endpoint, you’ll need to generate an API key with the `email.bounce.remove` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `email` | Required | String or array | String email address to modify, or an array of up to 50 email addresses to modify. |

**API Endpoint**: `POST /email/bounce/remove`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `EmailBounceRemoveCreateBody.builder().email("example@braze.com").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.EmailBounceRemoveCreateBody;
import com.yourorg.brazejava.resources.email.bounce.remove.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.email().bounce().remove().create(CreateRequest
                .builder()
                .data(EmailBounceRemoveCreateBody
                      .builder()
                      .email("example@braze.com")
                      .build())
                .build());
```
