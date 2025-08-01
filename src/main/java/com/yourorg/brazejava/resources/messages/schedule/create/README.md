
### Create Scheduled Messages <a name="create"></a>

> Use this endpoint to schedule a campaign, Canvas, or other message to be sent at a designated time (up to 90 days in the future) and provides you with an identifier to reference that message for updates. 
  

To use this endpoint, you’ll need to generate an API key with the `messages.schedule.create` permission.

If you are targeting a segment, a record of your request will be stored in the [Developer Console](https://dashboard.braze.com/app_settings/developer_console/activitylog/) after all scheduled messages have been sent.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

Braze endpoints support [batching API requests](https://www.braze.com/docs/api/api_limits/#batching-api-requests). A single request to the messaging endpoints can reach any of the following:

- Up to 50 specific external_ids, each with individual message parameters
- A segment of any size created in the Braze dashboard, specified by its `segment_id`
- An ad-hoc audience segment of any size, defined in the request as a [Connected Audience](https://www.braze.com/docs/api/objects_filters/connected_audience/) object
    

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `broadcast` | Optional | Boolean | See [broadcast](https://www.braze.com/docs/api/parameters/#broadcast). This parameter defaults to false (as of August 31, 2017).  <br>  <br>If `recipients` is omitted, `broadcast` must be set to true. However, use caution when setting `broadcast: true`, as unintentionally setting this flag may cause you to send your message to a larger than expected audience. |
| `external_user_ids` | Optional | Array of strings | See [external user identifier](https://www.braze.com/docs/api/parameters/#external-user-id). |
| `user_aliases` | Optional | Array of user alias objects | See [user alias object](https://www.braze.com/docs/api/objects_filters/user_alias_object/). |
| `audience` | Optional | Connected audience object | See [connected audience](https://www.braze.com/docs/api/objects_filters/connected_audience/). |
| `segment_id` | Optional | String | See [segment identifier](https://www.braze.com/docs/api/identifier_types/). |
| `campaign_id` | Required | String | See [campaign identifier](https://www.braze.com/docs/api/identifier_types/). |
| `recipients` | Optional | Array of recipients objects | See [recipients object](https://www.braze.com/docs/api/objects_filters/recipient_object/). |
| `send_id` | Optional | String | See [send identifier](https://www.braze.com/docs/api/identifier_types/). |
| `override_messaging_limits` | Optional | Boolean | Ignore global rate limits for campaigns, defaults to false |
| `recipient_subscription_state` | Optional | String | Use this to send messages to only users who have opted in (`opted_in`), only users who have subscribed or are opted in (`subscribed`) or to all users, including unsubscribed users (`all`).  <br>  <br>Using `all` users is useful for transactional email messaging. Defaults to `subscribed`. |
| `schedule` | Required | Schedule object | See [schedule object](https://www.braze.com/docs/api/objects_filters/schedule_object/) |
| `messages` | Optional | Messaging object | See available [messaging objects](https://www.braze.com/docs/api/objects_filters/#messaging-objects). |

## Response

### Example success response

``` json
{
    "dispatch_id": (string) the dispatch identifier,
    "schedule_id": (string) the schedule identifier,
    "message": "success"
}

```

**API Endpoint**: `POST /messages/schedule/create`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `MessagesScheduleCreateCreateBody.builder().audience(MessagesScheduleCreateCreateBodyAudience.builder().and(List.of(Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "equals"),Map.entry("custom_attribute_name", "eye_color"),Map.entry("value", "blue")))),Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "includes_value"),Map.entry("custom_attribute_name", "favorite_foods"),Map.entry("value", "pizza")))),Map.ofEntries(Map.entry("OR", List.of(Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "less_than_x_days_ago"),Map.entry("custom_attribute_name", "last_purchase_time"),Map.entry("value", 2)))),Map.ofEntries(Map.entry("push_subscription_status", Map.ofEntries(Map.entry("comparison", "is"),Map.entry("value", "opted_in"))))))),Map.ofEntries(Map.entry("email_subscription_status", Map.ofEntries(Map.entry("comparison", "is_not"),Map.entry("value", "subscribed")))),Map.ofEntries(Map.entry("last_used_app", Map.ofEntries(Map.entry("comparison", "after"),Map.entry("value", "2019-07-22T13:17:55+0000")))))).build()).broadcast(false).campaignId("campaign_identifier").externalUserIds("external_user_identifiers").messages(MessagesScheduleCreateCreateBodyMessages.builder().androidPush(Map.ofEntries()).applePush(Map.ofEntries()).contentCard(Map.ofEntries()).email(Map.ofEntries()).kindlePush(Map.ofEntries()).webPush(Map.ofEntries()).webhook(Map.ofEntries()).windows8Push(Map.ofEntries()).windowsPush(Map.ofEntries()).build()).overrideMessagingLimits(false).recipientSubscriptionState("subscribed").schedule(MessagesScheduleCreateCreateBodySchedule.builder().atOptimalTime(true).inLocalTime(true).time("").build()).segmentId("segment_identifiers").sendId("send_identifier").userAliases(MessagesScheduleCreateCreateBodyUserAliases.builder().aliasLabel("example_label").aliasName("example_name").build()).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.MessagesScheduleCreateCreateBody;
import com.yourorg.brazejava.model.MessagesScheduleCreateCreateBodyAudience;
import com.yourorg.brazejava.model.MessagesScheduleCreateCreateBodyMessages;
import com.yourorg.brazejava.model.MessagesScheduleCreateCreateBodySchedule;
import com.yourorg.brazejava.model.MessagesScheduleCreateCreateBodyUserAliases;
import com.yourorg.brazejava.resources.messages.schedule.create.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.messages().schedule().create().create(CreateRequest
                .builder()
                .data(MessagesScheduleCreateCreateBody
                      .builder()
                      .audience(MessagesScheduleCreateCreateBodyAudience
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
                      .externalUserIds("external_user_identifiers")
                      .messages(MessagesScheduleCreateCreateBodyMessages
                                .builder()
                                .androidPush(Map.ofEntries(

                                        ))
                                .applePush(Map.ofEntries(

                                        ))
                                .contentCard(Map.ofEntries(

                                        ))
                                .email(Map.ofEntries(

                                       ))
                                .kindlePush(Map.ofEntries(

                                        ))
                                .webPush(Map.ofEntries(

                                        ))
                                .webhook(Map.ofEntries(

                                        ))
                                .windows8Push(Map.ofEntries(

                                        ))
                                .windowsPush(Map.ofEntries(

                                        ))
                                .build())
                      .overrideMessagingLimits(false)
                      .recipientSubscriptionState("subscribed")
                      .schedule(MessagesScheduleCreateCreateBodySchedule
                                .builder()
                                .atOptimalTime(true)
                                .inLocalTime(true)
                                .time("")
                                .build())
                      .segmentId("segment_identifiers")
                      .sendId("send_identifier")
                      .userAliases(MessagesScheduleCreateCreateBodyUserAliases
                                   .builder()
                                   .aliasLabel("example_label")
                                   .aliasName("example_name")
                                   .build())
                      .build())
                .build());
```
