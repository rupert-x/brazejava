
### See Email Template Information <a name="list"></a>

> Use this endpoint to get information on your email templates. 
  

To use this endpoint, you’ll need to generate an API key with the `templates.email.info` permission.

> **Important:** Templates built using the drag-and-drop editor for email are not accepted. 
  

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "email_template_id": (string) your email template's API Identifier,
  "template_name": (string) the name of your email template,
  "description": (string) email template description,
  "subject": (string) the email template subject line,
  "preheader": (optional, string) the email preheader used to generate previews in some clients),
  "body": (optional, string) the email template body that may include HTML,
  "plaintext_body": (optional, string) a plaintext version of the email template body,
  "should_inline_css": (optional, boolean) whether there is inline CSS in the body of the template - defaults to the css inlining value for the App Group,
  "tags": (string) tag names,
  "created_at": (string, in ISO 8601),
  "updated_at": (string, in ISO 8601)
}

```

Images in this response will show in the `body` variable as HTML.

**API Endpoint**: `GET /templates/email/info`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `email_template_id` | ✗ | (Required) String  See [email template's API identifier](https://www.braze.com/docs/api/identifier_types/). | `"{{email_template_id}}"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.templates.email.info.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.templates().email().info().list(ListRequest
                .builder()
                .emailTemplateId("{{email_template_id}}")
                .build());
```
