
### Export Canvas Details <a name="list"></a>

> Use this endpoint to export metadata about a Canvas, such as the name, time created, current status, and more. 
  

To use this endpoint, you’ll need to generate an API key with the `canvas.details` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

Note: All Canvas steps have a next_paths field, which is an array of `{name, next_step_id}` data. For full steps and Message steps, the `next_step_ids` field will be present, but will not contain data for other Canvas Flow steps.

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "created_at": (string) date created as ISO 8601 date,
  "updated_at": (string) date updated as ISO 8601 date,
  "name": (string) Canvas name,
  "description": (string) Canvas description,
  "archived": (boolean) whether this Canvas is archived,
  "draft": (boolean) whether this Canvas is a draft,
  "schedule_type": (string) type of scheduling action,
  "first_entry": (string) date of first entry as ISO 8601 date,
  "last_entry": (string) date of last entry as ISO 8601 date,
  "channels": (array of strings) step channels used with Canvas,
  "variants": [
    {
      "name": (string) name of variant,
      "id": (string) API identifier of the variant,
      "first_step_ids": (array of strings) API identifiers for first steps in variant,
      "first_step_id": (string) API identifier of first step in variant (deprecated in November 2017, only included if the variant has only one first step)
    },
    ... (more variations)
  ],
  "tags": (array of strings) tag names associated with the Canvas,
  "steps": [
    {
      "name": (string) name of step,
      "id": (string) API identifier of the step,
      "next_step_ids": (array of strings) API identifiers of steps following step,
      "channels": (array of strings) channels used in step,
      "messages": {
          "message_variation_id": (string) {  // <=This is the actual id
              "channel": (string) channel type of the message (eg., "email"),
              ... channel-specific fields for this message, see Campaign Details Endpoint API Response for example message responses ...
          }
      }
    },
    ... (more steps)
  ],
  "message": (required, string) the status of the export, returns 'success' when completed without errors
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://desktop.postman.com/?desktopVersion=9.19.0&userId=16580579&teamId=409325).

**API Endpoint**: `GET /canvas/details`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `canvas_id` | ✗ | (Required) String  See [Canvas API Identifier](https://www.braze.com/docs/api/identifier_types/)  | `"{{canvas_identifier}}"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.canvas.details.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.canvas().details().list(ListRequest
                .builder()
                .canvasId("{{canvas_identifier}}")
                .build());
```
