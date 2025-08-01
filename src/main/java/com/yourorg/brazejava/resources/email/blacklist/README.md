
### Blacklist Email Addresses <a name="create"></a>

> Use this endpoint to unsubscribe a user from email and mark them as hard bounced. 
  

To use this endpoint, you’ll need to generate an API key with the `email.blacklist` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `email` | Required | String or array | String email address to blacklist, or an array of up to 50 email addresses to blocklist. |

**API Endpoint**: `POST /email/blacklist`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `EmailBlacklistCreateBody.builder().email(List.of("blacklist_email1","blacklist_email2")).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.EmailBlacklistCreateBody;
import com.yourorg.brazejava.resources.email.blacklist.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.email().blacklist().create(CreateRequest
                .builder()
                .data(EmailBlacklistCreateBody
                      .builder()
                      .email(List.of(
                                 "blacklist_email1",
                                 "blacklist_email2"
                             ))
                      .build())
                .build());
```
