
### Export Campaign Analytics <a name="list"></a>

> Use this endpoint to retrieve a daily series of various stats for a campaign over time. 
  

Data returned includes how many messages were sent, opened, clicked, or converted by messaging channel.

To use this endpoint, you’ll need to generate an API key with the `campaigns.data_series` permission.

Note: If you are using our [older navigation](https://www.braze.com/docs/navigation), `campaign_id` can be found at **Developer Console > API Settings**.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Responses

### Multichannel response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "data" : [
        {
            "time" : (string) date as ISO 8601 date,
            "messages" : {
                "ios_push" : [
                    {
                      "variation_name": "iOS_Push",
                      "sent" : (int),
                      "direct_opens" : (int),
                      "total_opens" : (int),
                      "bounces" : (int),
                      "body_clicks" : (int)
                      "revenue": 0,
                      "unique_recipients": 1,
                      "conversions": 0,
                      "conversions_by_send_time": 0,
                      "conversions1": 0,
                      "conversions1_by_send_time": 0,
                      "conversions2": 0,
                      "conversions2_by_send_time": 0,
                      "conversions3": 0,
                      "conversions3_by_send_time": 0,
                      "carousel_slide_[NUM]_[TITLE]_click": (optional, int),
                      "notif_button_[NUM]_[TITLE]_click": (optional, int)
                    }
                ],
                "android_push" : [
                    {
                      "sent" : (int),
                      "direct_opens" : (int),
                      "total_opens" : (int),
                      "bounces" : (int),
                      "body_clicks" : (int)
                    }
                ],
                "webhook": [
                    {
                      "sent": (int),
                      "errors": (int)
                    }
                ],
                "email" : [
                    {
                      "sent": (int),
                      "opens": (int),
                      "unique_opens": (int),
                      "clicks": (int),
                      "unique_clicks": (int),
                      "unsubscribes": (int),
                      "bounces": (int),
                      "delivered": (int),
                      "reported_spam": (int)
                    }
                ],
                "sms" : [
                  {
                    "sent": (int),
                    "delivered": (int),
                    "undelivered": (int),
                    "delivery_failed": (int)
                  }
                ]
              },
           "conversions_by_send_time": (optional, int),
           "conversions1_by_send_time": (optional, int),
           "conversions2_by_send_time": (optional, int),
           "conversions3_by_send_time": (optional, int),
           "conversions": (int),
           "conversions1": (optional, int),
           "conversions2": (optional, int),
           "conversions3": (optional, int),
           "unique_recipients": (int),
           "revenue": (optional, float)
        },
        ...
    ],
    ...
}

```

### Multivariate response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "data" : [
        {
            "time" : (string) date as ISO 8601 date,
            "conversions" : (int),
            "revenue": (float),
            "conversions_by_send_time": (int),
            "messages" : {
               "trigger_in_app_message": [{
                      "variation_name": (optional, string),
                      "impressions": (int),
                      "clicks": (int),
                      "first_button_clicks": (int),
                      "second_button_clicks": (int),
                      "revenue": (optional, float),,
                      "unique_recipients": (int),
                      "conversions": (optional, int),
                      "conversions_by_send_time": (optional, int),
                      "conversions1": (optional, int),
                      "conversions1_by_send_time": (optional, int),
                      "conversions2": (optional, int),
                      "conversions2_by_send_time": (optional, int),
                      "conversions3": (optional, int),
                      "conversions3_by_send_time": (optional, int)
                  }, {
                      "variation_name": (optional, string),
                      "impressions": (int),
                      "clicks": (int),
                      "first_button_clicks": (int),
                      "second_button_clicks": (int),
                      "revenue": (optional, float),,
                      "unique_recipients": (int),
                      "conversions": (optional, int),
                      "conversions_by_send_time": (optional, int),
                      "conversions1": (optional, int),
                      "conversions1_by_send_time": (optional, int),
                      "conversions2": (optional, int),
                      "conversions2_by_send_time": (optional, int),
                      "conversions3": (optional, int).
                      "conversions3_by_send_time": (optional, int)
                  }, {
                      "variation_name": (optional, string),
                      "revenue": (optional, float),,
                      "unique_recipients": (int),
                      "conversions": (optional, int),
                      "conversions_by_send_time": (optional, int),
                      "conversions1": (optional, int),
                      "conversions1_by_send_time": (optional, int),
                      "conversions2": (optional, int),
                      "conversions2_by_send_time": (optional, int),
                      "conversions3": (optional, int),
                      "conversions3_by_send_time": (optional, int),
                      "enrolled": (optional, int)
                  }]
              },
              "conversions_by_send_time": (optional, int),
              "conversions1_by_send_time": (optional, int),
              "conversions2_by_send_time": (optional, int),
              "conversions3_by_send_time": (optional, int),
              "conversions": (optional, int,
              "conversions1": (optional, int),
              "conversions2": (optional, int),
              "conversions3": (optional, int),
              "unique_recipients": (int),
              "revenue": (optional, float)
         }],
         ...
}

```

Possible message types are `email`, `in_app_message`, `webhook`, `android_push`, ios_push, `kindle_push`, `web_push`. All push message types will have the same statistics shown for `android_push`.

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /campaigns/data_series`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `campaign_id` | ✗ | (Required) String  See [campaign API identifier](https://www.braze.com/docs/api/identifier_types/).  The `campaign_id` for API campaigns can be found at **Settings > Setup and Testing > API Keys** and the **Campaign Details** page within your dashboard, or you can use the [List campaigns endpoint](https://www.braze.com/docs/api/endpoints/export/campaigns/get_campaigns/). | `"{{campaign_identifier}}"` |
| `ending_at` | ✗ | (Optional) Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string)  Date on which the data series should end. Defaults to time of the request. | `"2020-06-28T23:59:59-5:00"` |
| `length` | ✗ | (Required) Integer  Max number of days before `ending_at` to include in the returned series. Must be between 1 and 100 (inclusive). | `7` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.campaigns.dataseries.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.campaigns().dataSeries().list(ListRequest
                .builder()
                .campaignId("{{campaign_identifier}}")
                .endingAt("2020-06-28T23:59:59-5:00")
                .length(7)
                .build());
```
