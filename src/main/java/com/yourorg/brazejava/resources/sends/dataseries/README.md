
### Export Send Analytics <a name="list"></a>

> Use this endpoint to retrieve a daily series of various stats for a tracked `send_id`. 
  

Braze stores send analytics for 14 days after the send.

Campaign conversions will be attributed towards the most recent send id that a given user has received from the campaign.

To use this endpoint, you’ll need to generate an API key with the `sends.data_series` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

### Send analytics endpoint API response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
            "variation_name": (string) variation name,
            "sent": (int) the number of sends,
            "delivered": (int) the number of messages successfully delivered,
            "undelivered": (int) the number of undelivered,
            "delivery_failed": (int) the number of rejected,
            "direct_opens": (int) the number of direct opens,
            "total_opens": (int) the number of total opens,
            "bounces": (int) the number of bounces,
            "body_clicks": (int) the number of body clicks,
            "revenue": (float) the number of dollars of revenue (USD),
            "unique_recipients": (int) the number of unique recipients,
            "conversions": (int) the number of conversions,
            "conversions_by_send_time": (int) the number of conversions,
            "conversions1": (int, optional) the number of conversions for the second conversion event,
            "conversions1_by_send_time": (int, optional) the number of conversions for the second conversion event by send time,
            "conversions2": (int, optional) the number of conversions for the third conversion event,
            "conversions2_by_send_time": (int, optional) the number of conversions for the third conversion event by send time,
            "conversions3": (int, optional) the number of conversions for the fourth conversion event,
            "conversions3_by_send_time": (int, optional) the number of conversions for the fourth conversion event by send time
          }
        ]
      },
      "conversions_by_send_time": 0,
      "conversions1_by_send_time": 0,
      "conversions2_by_send_time": 0,
      "conversions3_by_send_time": 0,
      "conversions": 0,
      "conversions1": 0,
      "conversions2": 0,
      "conversions3": 0,
      "unique_recipients": 1,
      "revenue": 0
    }
  ],
  "message": "success"
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /sends/data_series`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `campaign_id` | ✗ | (Required) String  See [Campaign API identifier](https://www.braze.com/docs/api/identifier_types/). | `"{{campaign_identifier}}"` |
| `ending_at` | ✗ | (Optional) Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string)  Date on which the data series should end. Defaults to time of the request. | `"2014-12-10T23:59:59-05:00"` |
| `length` | ✗ | (Required) Integer  Max number of days before `ending_at` to include in the returned series. Must be between 1 and 100 (inclusive). | `30` |
| `send_id` | ✗ | (Required) String  See [Send API identifier](https://www.braze.com/docs/api/identifier_types/). | `"{{send_identifier}}"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.sends.dataseries.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.sends().dataSeries().list(ListRequest
                .builder()
                .campaignId("{{campaign_identifier}}")
                .endingAt("2014-12-10T23:59:59-05:00")
                .length(30)
                .sendId("{{send_identifier}}")
                .build());
```
