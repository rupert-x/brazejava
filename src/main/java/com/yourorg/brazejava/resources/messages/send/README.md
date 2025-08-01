
### Send Messages Immediately via API Only <a name="create"></a>

> Use this endpoint to send immediate, ad-hoc messages to designated users via the Braze API. 
  

To use this endpoint, you’ll need to generate an API key with the `messages.send` permission.

Be sure to include Messaging Objects in your body to complete your requests.

If you are targeting a segment, a record of your request will be stored in the [Developer Console](https://dashboard.braze.com/app_settings/developer_console/activitylog/).

## Rate limit

When specifying a segment or Connected Audience in your request, we apply a rate limit of 250 requests per minute to this endpoint. Otherwise, if specifying an `external_id`, this endpoint has a default rate limit of 250,000 requests per hour, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

Braze endpoints support [batching API requests](https://www.braze.com/docs/api/api_limits/#batching-api-requests). A single request to the messaging endpoints can reach any of the following:

- Up to 50 specific `external_ids`, each with individual message parameters
- A segment of any size created in the Braze dashboard, specified by its `segment_id`
- An ad-hoc audience segment of any size, defined in the request as a [Connected Audience](https://www.braze.com/docs/api/objects_filters/connected_audience/) object
    

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `broadcast` | Optional | Boolean | See [broadcast](https://www.braze.com/docs/api/parameters/#broadcast). This parameter defaults to false (as of August 31, 2017).  <br>  <br>If `recipients` is omitted, `broadcast` must be set to true. However, use caution when setting `broadcast: true`, as unintentionally setting this flag may cause you to send your messages to a larger than expected audience. |
| `external_user_ids` | Optional | Array of strings | See [external user ID](https://www.braze.com/docs/api/parameters/#external-user-id). |
| `user_aliases` | Optional | Array of user alias objects | See [user alias object](https://www.braze.com/docs/api/objects_filters/user_alias_object/). |
| `segment_id` | Optional | String | See [segment identifier](https://www.braze.com/docs/api/identifier_types/). |
| `audience` | Optional | Connected audience object | See [connected audience](https://www.braze.com/docs/api/objects_filters/connected_audience/). |
| `campaign_id` | Optional\* | String | See [campaign identifier](https://www.braze.com/docs/api/identifier_types/) for more information.  <br>  <br>\*Required if you wish to track campaign stats (e.g. sends, clicks, bounces, etc) on the Braze dashboard. |
| `send_id` | Optional | String | See [send identifier](https://www.braze.com/docs/api/identifier_types/) |
| `override_frequency_capping` | Optional | Boolean | Ignore \`frequency_capping\` for campaigns, defaults to false. |
| `recipient_subscription_state` | Optional | String | Use this to send messages to only users who have opted in (`opted_in`), only users who have subscribed or are opted in (`subscribed`) or to all users, including unsubscribed users (`all`).  <br>  <br>Using `all` users is useful for transactional email messaging. Defaults to `subscribed`. |
| `messages` | Optional | Messaging objects | See available [messaging objects](https://www.braze.com/docs/api/endpoints/messaging/send_messages/post_send_messages/#available-messaging-objects). |

## Response details

Message sending endpoint responses will include the message’s `dispatch_id` for reference back to the dispatch of the message. The `dispatch_id` is the id of the message dispatch (unique id for each ‘transmission’ sent from the Braze platform). For more, information refer to [Dispatch ID behavior](https://www.braze.com/docs/help/help_articles/data/dispatch_id/).

**API Endpoint**: `POST /messages/send`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `MessagesSendCreateBody.builder().audience(MessagesSendCreateBodyAudience.builder().and(List.of(Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "equals"),Map.entry("custom_attribute_name", "eye_color"),Map.entry("value", "blue")))),Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "includes_value"),Map.entry("custom_attribute_name", "favorite_foods"),Map.entry("value", "pizza")))),Map.ofEntries(Map.entry("OR", List.of(Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "less_than_x_days_ago"),Map.entry("custom_attribute_name", "last_purchase_time"),Map.entry("value", 2)))),Map.ofEntries(Map.entry("push_subscription_status", Map.ofEntries(Map.entry("comparison", "is"),Map.entry("value", "opted_in"))))))),Map.ofEntries(Map.entry("email_subscription_status", Map.ofEntries(Map.entry("comparison", "is_not"),Map.entry("value", "subscribed")))),Map.ofEntries(Map.entry("last_used_app", Map.ofEntries(Map.entry("comparison", "after"),Map.entry("value", "2019-07-22T13:17:55+0000")))))).build()).broadcast("false").campaignId("campaign_identifier").externalUserIds("external_user_identifiers").messages(MessagesSendCreateBodyMessages.builder().androidPush("(optional, Android Push Object)").applePush("(optional, Apple Push Object)").contentCard("(optional, Content Card Object)").email("(optional, Email Object)").kindlePush("(optional, Kindle/FireOS Push Object)").webPush("(optional, Web Push Object)").windowsPhone8Push("(optional, Windows Phone 8 Push Object)").windowsUniversalPush("(optional, Windows Universal Push Object)").build()).overrideFrequencyCapping("false").recipientSubscriptionState("all").segmentId("segment_identifier").sendId("send_identifier").userAliases(MessagesSendCreateBodyUserAliases.builder().aliasLabel("example_label").aliasName("example_name").build()).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.MessagesSendCreateBody;
import com.yourorg.brazejava.model.MessagesSendCreateBodyAudience;
import com.yourorg.brazejava.model.MessagesSendCreateBodyMessages;
import com.yourorg.brazejava.model.MessagesSendCreateBodyUserAliases;
import com.yourorg.brazejava.resources.messages.send.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.messages().send().create(CreateRequest
                .builder()
                .data(MessagesSendCreateBody
                      .builder()
                      .audience(MessagesSendCreateBodyAudience
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
                      .broadcast("false")
                      .campaignId("campaign_identifier")
                      .externalUserIds("external_user_identifiers")
                      .messages(MessagesSendCreateBodyMessages
                                .builder()
                                .androidPush("(optional, Android Push Object)")
                                .applePush("(optional, Apple Push Object)")
                                .contentCard("(optional, Content Card Object)")
                                .email("(optional, Email Object)")
                                .kindlePush("(optional, Kindle/FireOS Push Object)")
                                .webPush("(optional, Web Push Object)")
                                .windowsPhone8Push("(optional, Windows Phone 8 Push Object)")
                                .windowsUniversalPush("(optional, Windows Universal Push Object)")
                                .build())
                      .overrideFrequencyCapping("false")
                      .recipientSubscriptionState("all")
                      .segmentId("segment_identifier")
                      .sendId("send_identifier")
                      .userAliases(MessagesSendCreateBodyUserAliases
                                   .builder()
                                   .aliasLabel("example_label")
                                   .aliasName("example_name")
                                   .build())
                      .build())
                .build());
```
