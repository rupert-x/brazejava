
### Schedule API Triggered Campaigns <a name="create"></a>

> Use this endpoint to send dashboard created campaign messages (up to 90 days in advance) via API-triggered delivery, allowing you to decide what action should trigger the message to be sent. 
  

To use this endpoint, you’ll need to generate an API key with the `campaigns.trigger.schedule.create` permission.

You can pass in `trigger_properties` that will be templated into the message itself.

Note that to send messages with this endpoint, you must have a [Campaign ID](https://www.braze.com/docs/api/identifier_types/), created when you build an [API-Triggered Campaign](https://www.braze.com/docs/api/api_campaigns/).

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

Braze endpoints support [batching API requests](https://www.braze.com/docs/api/api_limits/#batching-api-requests). A single request to the messaging endpoints can reach any of the following:

- Up to 50 specific external_ids, each with individual message parameters
- A segment of any size created in the Braze dashboard, specified by its `segment_id`
- An ad-hoc audience segment of any size, defined in the request as a [Connected Audience](https://www.braze.com/docs/api/objects_filters/connected_audience/) object
    

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `campaign_id` | Required | String | See [campaign identifier](https://www.braze.com/docs/api/identifier_types/) |
| `send_id` | Optional | String | See [send identifier](https://www.braze.com/docs/api/identifier_types/). |
| `recipients` | Optional | Array of recipient objects | See [recipients object](https://www.braze.com/docs/api/objects_filters/recipient_object/). |
| `audience` | Optional | Connected audience object | See [connected audience](https://www.braze.com/docs/api/objects_filters/connected_audience/). |
| `broadcast` | Optional | Boolean | See [broadcast](https://www.braze.com/docs/api/parameters/#broadcast). This parameter defaults to false (as of August 31, 2017).  <br>  <br>If `recipients` is omitted, `broadcast` must be set to true. However, use caution when setting `broadcast: true`, as unintentionally setting this flag may cause you to send your message to a larger than expected audience. |
| `trigger_properties` | Optional | Object | Personalization key-value pairs for all users in this send. See [trigger properties](https://www.braze.com/docs/api/objects_filters/trigger_properties_object/). |
| `schedule` | Required | Schedule object | See [schedule object](https://www.braze.com/docs/api/objects_filters/schedule_object/). |

## Response

### Example success response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-API-KEY-HERE
{
{
    "dispatch_id": "dispatch_identifier",
    "schedule_id": "schedule_identifier",
    "message": "success"
}

```

**API Endpoint**: `POST /campaigns/trigger/schedule/create`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `CampaignsTriggerScheduleCreateCreateBody.builder().audience(CampaignsTriggerScheduleCreateCreateBodyAudience.builder().and(List.of(Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "equals"),Map.entry("custom_attribute_name", "eye_color"),Map.entry("value", "blue")))),Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "includes_value"),Map.entry("custom_attribute_name", "favorite_foods"),Map.entry("value", "pizza")))),Map.ofEntries(Map.entry("OR", List.of(Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "less_than_x_days_ago"),Map.entry("custom_attribute_name", "last_purchase_time"),Map.entry("value", 2)))),Map.ofEntries(Map.entry("push_subscription_status", Map.ofEntries(Map.entry("comparison", "is"),Map.entry("value", "opted_in"))))))),Map.ofEntries(Map.entry("email_subscription_status", Map.ofEntries(Map.entry("comparison", "is_not"),Map.entry("value", "subscribed")))),Map.ofEntries(Map.entry("last_used_app", Map.ofEntries(Map.entry("comparison", "after"),Map.entry("value", "2019-07-22T13:17:55+0000")))))).build()).broadcast(false).campaignId("campaign_identifier").recipients(List.of(CampaignsTriggerScheduleCreateCreateBodyRecipientsItem.builder().externalUserId("external_user_identifier").triggerProperties(Map.ofEntries()).userAlias("example_alias").build())).schedule(CampaignsTriggerScheduleCreateCreateBodySchedule.builder().atOptimalTime(false).inLocalTime(false).time("").build()).sendId("send_identifier").triggerProperties(Map.ofEntries()).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CampaignsTriggerScheduleCreateCreateBody;
import com.yourorg.brazejava.model.CampaignsTriggerScheduleCreateCreateBodyAudience;
import com.yourorg.brazejava.model.CampaignsTriggerScheduleCreateCreateBodyRecipientsItem;
import com.yourorg.brazejava.model.CampaignsTriggerScheduleCreateCreateBodySchedule;
import com.yourorg.brazejava.resources.campaigns.trigger.schedule.create.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.campaigns().trigger().schedule().create().create(CreateRequest
                .builder()
                .data(CampaignsTriggerScheduleCreateCreateBody
                      .builder()
                      .audience(CampaignsTriggerScheduleCreateCreateBodyAudience
                                .builder()
                                .and(List.of(
                                        Map.ofEntries(
                                                Map.entry("custom_attribute", Map.ofEntries(
                                                        Map.entry("comparison", "equals"),
                                                        Map.entry("custom_attribute_name", "eye_color"),
                                                        Map.entry("value", "blue")
                                                        ))
                                        ),
                                        Map.ofEntries(
                                                Map.entry("custom_attribute", Map.ofEntries(
                                                        Map.entry("comparison", "includes_value"),
                                                        Map.entry("custom_attribute_name", "favorite_foods"),
                                                        Map.entry("value", "pizza")
                                                        ))
                                        ),
                                        Map.ofEntries(
                                                Map.entry("OR", List.of(
                                                        Map.ofEntries(
                                                                Map.entry("custom_attribute", Map.ofEntries(
                                                                        Map.entry("comparison", "less_than_x_days_ago"),
                                                                        Map.entry("custom_attribute_name", "last_purchase_time"),
                                                                        Map.entry("value", 2)
                                                                        ))
                                                        ),
                                                        Map.ofEntries(
                                                                Map.entry("push_subscription_status", Map.ofEntries(
                                                                        Map.entry("comparison", "is"),
                                                                        Map.entry("value", "opted_in")
                                                                        ))
                                                        )
                                                        ))
                                        ),
                                        Map.ofEntries(
                                                Map.entry("email_subscription_status", Map.ofEntries(
                                                        Map.entry("comparison", "is_not"),
                                                        Map.entry("value", "subscribed")
                                                        ))
                                        ),
                                        Map.ofEntries(
                                                Map.entry("last_used_app", Map.ofEntries(
                                                        Map.entry("comparison", "after"),
                                                        Map.entry("value", "2019-07-22T13:17:55+0000")
                                                        ))
                                        )
                                     ))
                                .build())
                      .broadcast(false)
                      .campaignId("campaign_identifier")
                      .recipients(List.of(
                                      CampaignsTriggerScheduleCreateCreateBodyRecipientsItem
                                      .builder()
                                      .externalUserId("external_user_identifier")
                                      .triggerProperties(Map.ofEntries(

                                              ))
                                      .userAlias("example_alias")
                                      .build()
                                  ))
                      .schedule(CampaignsTriggerScheduleCreateCreateBodySchedule
                                .builder()
                                .atOptimalTime(false)
                                .inLocalTime(false)
                                .time("")
                                .build())
                      .sendId("send_identifier")
                      .triggerProperties(Map.ofEntries(

                              ))
                      .build())
                .build());
```
