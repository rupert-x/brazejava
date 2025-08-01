
### Export Daily Active Users by Date <a name="list"></a>

> Use this endpoint to retrieve a daily series of the total number of unique active users on each date. 
  

Note: If you are using our [older navigation](https://www.braze.com/docs/navigation), API Keys can be found at **Developer Console > API Settings**.

To use this endpoint, you’ll need to generate an API key with the `kpi.dau.data_series` permission.

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
            "time" : (string) the date as ISO 8601 date,
            "dau" : (int) the number of daily active users
        },
        ...
    ]
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /kpi/dau/data_series`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `app_id` | ✗ | (Optional) String  App API identifier retrieved from **Settings > Setup and Testing > API Keys**. If excluded, results for all apps in workspace will be returned. | `"{{app_identifier}}"` |
| `ending_at` | ✗ | (Optional)  Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string) Date on which the data series should end. Defaults to time of the request. | `"2018-06-28T23:59:59-5:00"` |
| `length` | ✗ | (Required) Integer  Maximum number of days before `ending_at` to include in the returned series. Must be between 1 and 100 (inclusive). | `10` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.kpi.dau.dataseries.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.kpi().dau().dataSeries().list(ListRequest
                .builder()
                .appId("{{app_identifier}}")
                .endingAt("2018-06-28T23:59:59-5:00")
                .length(10)
                .build());
```
