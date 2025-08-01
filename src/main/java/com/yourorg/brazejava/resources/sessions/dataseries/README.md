
### Export App Sessions by Time <a name="list"></a>

> Use this endpoint to retrieve a series of the number of sessions for your app over a designated time period. 
  

Note: If you are using our [older navigation](https://www.braze.com/docs/navigation), `segment_id` can be found at **Developer Console > API Settings**.

To use this endpoint, you’ll need to generate an API key with the `sessions.data_series` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "data" : [
        {
            "time" : (string) point in time - as ISO 8601 extended when unit is "hour" and as ISO 8601 date when unit is "day",
            "sessions" : (int)
        },
        ...
    ]
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /sessions/data_series`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `app_id` | ✗ | (Optional) String  App API identifier retrieved from the **Settings > Setup and Testing > API Keys** to limit analytics to a specific app. | `"{{app_identifier}}"` |
| `ending_at` | ✗ | (Optional) Datetime (ISO 8601 string)  Date on which the data series should end. Defaults to time of the request. | `"2018-06-28T23:59:59-5:00"` |
| `length` | ✗ | (Required) Integer  Max number of days before `ending_at` to include in the returned series - must be between 1 and 100 (inclusive). | `14` |
| `segment_id` | ✗ | (Required) String  See [Segment API identifier](https://www.braze.com/docs/api/identifier_types/). Segment ID indicating the analytics-enabled segment for which sessions should be returned. | `"{{segment_identifier}}"` |
| `unit` | ✗ | (Optional) String  Unit of time between data points. Can be `day` or `hour`, defaults to `day`.  | `"day"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.sessions.dataseries.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.sessions().dataSeries().list(ListRequest
                .builder()
                .appId("{{app_identifier}}")
                .endingAt("2018-06-28T23:59:59-5:00")
                .length(14)
                .segmentId("{{segment_identifier}}")
                .unit("day")
                .build());
```
