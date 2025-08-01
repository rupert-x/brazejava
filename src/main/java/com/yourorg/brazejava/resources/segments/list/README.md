
### Export Segment List <a name="list"></a>

> Use this endpoint to export a list of segments, each of which will include its name, Segment API identifier, and whether it has analytics tracking enabled. 
  

The segments are returned in groups of 100 sorted by time of creation (oldest to newest by default). Archived segments are not included.

To use this endpoint, you’ll need to generate an API key with the `segments.list` permission.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "segments" : [
        {
            "id" : (string) Segment API Identifier,
            "name" : (string) segment name,
            "analytics_tracking_enabled" : (boolean) whether the segment has analytics tracking enabled,
            "tags" : (array) tag names associated with the segment
        },
        ...
    ]
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /segments/list`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `page` | ✗ | (Optional) Integer  The page of segments to return, defaults to 0 (returns the first set of up to 100). | `1` |
| `sort_direction` | ✗ | (Optional) String  - Sort creation time from newest to oldest: pass in the value `desc`. - Sort creation time from oldest to newest: pass in the value `asc`.  If `sort_direction` is not included, the default order is oldest to newest. | `"desc"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.segments.list.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.segments().list().list(ListRequest
                .builder()
                .page(1)
                .sortDirection("desc")
                .build());
```
