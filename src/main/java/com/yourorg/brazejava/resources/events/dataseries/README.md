
### Export Custom Events Analytics <a name="list"></a>

> Use this endpoint to retrieve a series of the number of occurrences of a custom event in your app over a designated time period. 
  

Note: If you are using our [older navigation](https://www.braze.com/docs/navigation), `app_id` can be found at**Developer Console** > **API Settings**

To use this endpoint, you’ll need to generate an API key with the `events.data_series` permission.

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
            "count" : (int)
        },
        ...
    ]
}

```

### Fatal error response codes

For status codes and associated error messages that will be returned if your request encounters a fatal error, reference [Fatal errors & responses](https://www.braze.com/docs/api/errors/#fatal-errors).

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /events/data_series`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `app_id` | ✗ | (Optional) String  App API identifier retrieved from **Settings > Setup and Testing > API Keys** to limit analytics to a specific app. | `"{{app_identifier}}"` |
| `ending_at` | ✗ | (Optional) Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string)  Date on which the data series should end. Defaults to time of the request. | `"2014-12-10T23:59:59-05:00"` |
| `event` | ✗ | (Required) String  The name of the custom event for which to return analytics.  | `"event_name"` |
| `length` | ✗ | (Required) Integer  Maximum number of units (days or hours) before `ending_at` to include in the returned series. Must be between 1 and 100 (inclusive). | `24` |
| `segment_id` | ✗ | (Optional) String  See [Segment API identifier](https://www.braze.com/docs/api/identifier_types/). Segment ID indicating the analytics-enabled segment for which event analytics should be returned. | `"{{segment_identifier}}"` |
| `unit` | ✗ | (Optional) String  Unit of time between data points - can be `day` or `hour`, defaults to `day`. | `"hour"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.events.dataseries.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.events().dataSeries().list(ListRequest
                .builder()
                .appId("{{app_identifier}}")
                .endingAt("2014-12-10T23:59:59-05:00")
                .event("event_name")
                .length(24)
                .segmentId("{{segment_identifier}}")
                .unit("hour")
                .build());
```
