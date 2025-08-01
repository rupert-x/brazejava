
### List Available Email Templates <a name="list"></a>

> Use this endpoint to get a list of available templates in your Braze account. 
  

To use this endpoint, you’ll need to generate an API key with the `templates.email.list` permission.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Response

> **Important:** Templates built using the Drag & Drop Editor for email are not provided in this response. 
  

``` json
{
  "count": number of templates returned
  "templates": [template with the following properties]:
    "email_template_id": (string) your email template's API Identifier,
    "template_name": (string) the name of your email template,
    "created_at": (string, in ISO 8601),
    "updated_at": (string, in ISO 8601),
    "tags": (array of strings) tags appended to the template
}

```

**API Endpoint**: `GET /templates/email/list`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `limit` | ✗ | (Optional) Positive Number  Maximum number of templates to retrieve. Default to 100 if not provided, with a maximum acceptable value of 1000. | `1` |
| `modified_after` | ✗ | (Optional) String in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)  Retrieve only templates updated at or after the given time. | `"2020-01-01T01:01:01.000000"` |
| `modified_before` | ✗ | (Optional) String in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)  Retrieve only templates updated at or before the given time. | `"2020-02-01T01:01:01.000000"` |
| `offset` | ✗ | (Optional) Positive Number  Number of templates to skip before returning rest of the templates that fit the search criteria. | `123` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.templates.email.list.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.templates().email().list().list(ListRequest
                .builder()
                .limit(1)
                .modifiedAfter("2020-01-01T01:01:01.000000")
                .modifiedBefore("2020-02-01T01:01:01.000000")
                .build());
```
