
### Export News Feed Card Analytics <a name="list"></a>

> Use this endpoint to retrieve a daily series of engagement stats for a card over time. 
  

Note: If you are using our [older navigation](https://www.braze.com/docs/navigation), \`card_id\` can be found at **Developer Console > API Settings**.

To use this endpoint, you’ll need to generate an API key with the `feed.data_series` permission.

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
            "time" : (string) the point in time - as ISO 8601 extended when unit is "hour" and as ISO 8601 date when unit is "day",
            "clicks" : (int) the number of clicks,
            "impressions" : (int) the number of impressions,
            "unique_clicks" : (int) the number of unique clicks,
            "unique_impressions" : (int) the number of unique impressions
        },
        ...
    ]
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /feed/data_series`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `card_id` | ✗ | (Required) String  See [Card API identifier](https://www.braze.com/docs/api/identifier_types/).  The `card_id` for a given card can be found in the **Settings > Setup and Testing > API Keys** page and on the card details page within your dashboard, or you can use the [News Feed List Endpoint](https://www.braze.com/docs/api/endpoints/export/news_feed/get_news_feed_cards/). | `"{{card_identifier}}"` |
| `ending_at` | ✗ | (Optional) Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string)  Date on which the data series should end. Defaults to time of the request.  | `"2018-06-28T23:59:59-5:00"` |
| `length` | ✗ | (Required) Integer  Max number of units (days or hours) before `ending_at` to include in the returned series. Must be between 1 and 100 (inclusive). | `14` |
| `unit` | ✗ | (Optional) String  Unit of time between data points. Can be `day` or `hour`, defaults to `day`. | `"day"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.feed.dataseries.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.feed().dataSeries().list(ListRequest
                .builder()
                .cardId("{{card_identifier}}")
                .endingAt("2018-06-28T23:59:59-5:00")
                .length(14)
                .unit("day")
                .build());
```
