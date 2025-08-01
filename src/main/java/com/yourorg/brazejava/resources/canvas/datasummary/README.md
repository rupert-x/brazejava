
### Export Canvas Data Analytics Summary <a name="list"></a>

> Use this endpoint to export rollups of time series data for a Canvas, providing a concise summary of a Canvas’ results. 
  

To use this endpoint, you’ll need to generate an API key with the `canvas.data_summary` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "data": {
    "name": (string) Canvas name,
    "total_stats": {
      "revenue": (float),
      "conversions": (int),
      "conversions_by_entry_time": (int),
      "entries": (int)
    },
    "variant_stats": (optional) {
      "00000000-0000-0000-0000-0000000000000": (API identifier for variant) {
        "name": (string) name of variant,
        "revenue": (float),
        "conversions": (int),
        "entries": (int)
      },
      ... (more variants)
    },
    "step_stats": (optional) {
      "00000000-0000-0000-0000-0000000000000": (API identifier for step) {
        "name": (string) name of step,
        "revenue": (float),
        "conversions": (int),
        "conversions_by_entry_time": (int),
        "messages": {
          "android_push": (name of channel) [
            {
              "sent": (int),
              "opens": (int),
              "influenced_opens": (int),
              "bounces": (int)
              ... (more stats for channel)
            }
          ],
          ... (more channels)
        }
      },
      ... (more steps)
    }
  },
  "message": (required, string) the status of the export, returns 'success' when completed without errors
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://desktop.postman.com/?desktopVersion=9.19.0&userId=16580579&teamId=409325).

**API Endpoint**: `GET /canvas/data_summary`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `canvas_id` | ✗ | (Required) String   See [Canvas API identifier](https://www.braze.com/docs/api/identifier_types/). | `"{{canvas_id}}"` |
| `ending_at` | ✗ | (Required) Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string) Date on which the data export should end. Defaults to time of the request | `"2018-05-30T23:59:59-5:00"` |
| `include_deleted_step_data` | ✗ | (Optional) Boolean  Whether or not to include step stats for deleted steps (defaults to false). | `true` |
| `include_step_breakdown` | ✗ | (Optional) Boolean  Whether or not to include step stats (defaults to false). | `true` |
| `include_variant_breakdown` | ✗ | (Optional) Boolean  Whether or not to include variant stats (defaults to false). | `true` |
| `length` | ✗ | (Optional*) Integer  Max number of days before `ending_at` to include in the returned series. Must be between 1 and 14 (inclusive).  *Either `length` or `starting_at` is required. | `5` |
| `starting_at` | ✗ | (Optional*) Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string)  Date on which the data export should begin.  *Either `length` or `starting_at` is required. | `"2018-05-28T23:59:59-5:00"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.canvas.datasummary.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.canvas().dataSummary().list(ListRequest
                .builder()
                .canvasId("{{canvas_id}}")
                .endingAt("2018-05-30T23:59:59-5:00")
                .includeDeletedStepData(true)
                .includeStepBreakdown(true)
                .includeVariantBreakdown(true)
                .length(5)
                .startingAt("2018-05-28T23:59:59-5:00")
                .build());
```
