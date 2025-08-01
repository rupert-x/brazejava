
### Export Segment Details <a name="list"></a>

> Use this endpoint to retrieve relevant information on a segment, which can be identified by the `segment_id`. 
  

Note: If you are using our [older navigation](https://www.braze.com/docs/navigation), `segment_id` can be found at **Developer Console > API Settings**.

To use this endpoint, you’ll need to generate an API key with the `segments.details` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
      "message": (required, string) the status of the export, returns 'success' when completed without errors,
      "created_at" : (string) date created as ISO 8601 date,
      "updated_at" : (string) date last updated as ISO 8601 date,
      "name" : (string) segment name,
      "description" : (string) human-readable description of filters,
      "text_description" : (string) segment description, 
      "tags" : (array) tag names associated with the segment
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /segments/details`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `segment_id` | ✗ | (Required) String  See [Segment API identifier](https://www.braze.com/docs/api/identifier_types/).  The `segment_id` for a given segment can be found in your **Settings > Setup and Testing > API Keys** within your Braze account or you can use the [Segment List Endpoint](https://www.braze.com/docs/api/endpoints/export/get_segment/). | `"{{segment_identifier}}"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.segments.details.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.segments().details().list(ListRequest
                .builder()
                .segmentId("{{segment_identifier}}")
                .build());
```
