
### Blocklist Email Addresses <a name="create"></a>

> Use this endpoint to unsubscribe a user from email and mark them as hard bounced. 
  

To use this endpoint, you’ll need to generate an API key with the `email.blacklist` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `email` | Required | String or array | String email address to blacklist, or an array of up to 50 email addresses to blocklist. |

**API Endpoint**: `POST /email/blocklist`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `EmailBlocklistCreateBody.builder().email(List.of("blocklist_email1","blocklist_email2")).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.EmailBlocklistCreateBody;
import com.yourorg.brazejava.resources.email.blocklist.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.email().blocklist().create(CreateRequest
                .builder()
                .data(EmailBlocklistCreateBody
                      .builder()
                      .email(List.of(
                                 "blocklist_email1",
                                 "blocklist_email2"
                             ))
                      .build())
                .build());
```
