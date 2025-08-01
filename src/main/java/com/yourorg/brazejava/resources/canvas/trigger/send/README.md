
### Send Canvas Messages via API Triggered Delivery <a name="create"></a>

> Use this endpoint to send Canvas messages via API-triggered delivery. 
  

To use this endpoint, you’ll need to generate an API key with the `canvas.trigger.send` permission.

API-triggered delivery allows you to house message content inside of the Braze dashboard while dictating when a message is sent, and to whom via your API.

Note that to send messages with this endpoint, you must have a [Canvas ID](https://www.braze.com/docs/api/identifier_types/#canvas-api-identifier) created when you build a Canvas.

## Rate limit

When specifying a segment or Connected Audience in your request, we apply a rate limit of 250 requests per minute to this endpoint. Otherwise, if specifying an `external_id`, this endpoint has a default rate limit of 250,000 requests per hour, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

Braze endpoints support [batching API requests](https://www.braze.com/docs/api/api_limits/#batching-api-requests). A single request to the messaging endpoints can reach any of the following:

- Up to 50 specific `external_ids`, each with individual message parameters
- A segment of any size created in the Braze dashboard, specified by its `segment_id`
- An ad-hoc audience segment of any size, defined in the request as a [Connected Audience](https://www.braze.com/docs/api/objects_filters/connected_audience/) object
    

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `canvas_id` | Required | String | See [Canvas identifier](https://www.braze.com/docs/api/identifier_types/). |
| `canvas_entry_properties` | Optional | Object | See [Canvas entry properties](https://www.braze.com/docs/api/objects_filters/canvas_entry_properties_object/). Personalization key-value pairs that will apply to all users in this request. The Canvas entry properties object has a maximum size limit of 50 KB. |
| `broadcast` | Optional | Boolean | You must set `broadcast` to true when sending a message to an entire segment that a campaign or Canvas targets. This parameter defaults to false (as of August 31, 2017).  <br>  <br>If `broadcast` is set to true, a recipients list cannot be included. However, use caution when setting `broadcast: true`, as unintentionally setting this flag may cause you to send your message to a larger than expected audience. |
| `audience` | Optional | Connected audience object | See [Connected audience](https://braze.com/docs/api/objects_filters/connected_audience/). |
| `recipients` | Optional | Array | See [Recipients object](https://www.braze.com/docs/api/objects_filters/recipient_object/). If not provided and `broadcast` is set to true, the message will send to the entire segment targeted by the Canvas.  <br>  <br>The `recipients` array may contain up to 50 objects, with each object containing a single `external_user_id` string and `canvas_entry_properties` object. Either `external_user_id` or user_alias is required for this call. Requests must specify only one.  <br>  <br>When `send_to_existing_only` is true, Braze will only send the message to existing users—however this flag can’t be used with user aliases. When `send_to_existing_only` is `false` and a user with the given `id` does not exist, Braze will create a user with that ID and attributes before sending the message. |

Customers using the API for server-to-server calls may need to whitelist the appropriate API URL if they’re behind a firewall.

> **Note:** If you include both specific users in your API call and a target segment in the dashboard, the message will send to specifically the user profiles that are in the API call and qualify for the segment filters. 
  

## Response details

Message sending endpoint responses will include the message’s `dispatch_id` for reference back to the dispatch of the message. The `dispatch_id` is the ID of the message dispatch (unique ID for each “transmission” sent from the Braze platform). Check out [Dispatch ID behavior](https://www.braze.com/docs/help/help_articles/data/dispatch_id/) for more information.

## Create send endpoint

**Using the Attributes Object in Canvas**

Braze has a Messaging Object called `Attributes` that allows you to add, create, or update attributes and values for a user before sending them an API-Triggered Canvas using the `canvas/trigger/send` endpoint as this API call will process the User Attributes object before it processes and sends the Canvas. This helps minimize the risk of there being issues caused by [race conditions](https://www.braze.com/docs/help/best_practices/race_conditions/).

> **Important:** Looking for the camaigns version of this endpoint? Check out [Sending campaign messages via API-triggered delivery](https://www.braze.com/docs/api/endpoints/messaging/send_messages/post_send_triggered_campaigns/).

**API Endpoint**: `POST /canvas/trigger/send`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `CanvasTriggerSendCreateBody.builder().audience(CanvasTriggerSendCreateBodyAudience.builder().and(List.of(Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "equals"),Map.entry("custom_attribute_name", "eye_color"),Map.entry("value", "blue")))),Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "includes_value"),Map.entry("custom_attribute_name", "favorite_foods"),Map.entry("value", "pizza")))),Map.ofEntries(Map.entry("OR", List.of(Map.ofEntries(Map.entry("custom_attribute", Map.ofEntries(Map.entry("comparison", "less_than_x_days_ago"),Map.entry("custom_attribute_name", "last_purchase_time"),Map.entry("value", 2)))),Map.ofEntries(Map.entry("push_subscription_status", Map.ofEntries(Map.entry("comparison", "is"),Map.entry("value", "opted_in"))))))),Map.ofEntries(Map.entry("email_subscription_status", Map.ofEntries(Map.entry("comparison", "is_not"),Map.entry("value", "subscribed")))),Map.ofEntries(Map.entry("last_used_app", Map.ofEntries(Map.entry("comparison", "after"),Map.entry("value", "2019-07-22T13:17:55+0000")))))).build()).broadcast(false).canvasEntryProperties(CanvasTriggerSendCreateBodyCanvasEntryProperties.builder().productName("shoes").productPrice(79.99).build()).canvasId("canvas_identifier").recipients(List.of(CanvasTriggerSendCreateBodyRecipientsItem.builder().attributes(CanvasTriggerSendCreateBodyRecipientsItemAttributes.builder().firstName("Alex").build()).canvasEntryProperties("").externalUserId("user_identifier").sendToExistingOnly(true).triggerProperties(Map.ofEntries()).userAlias(CanvasTriggerSendCreateBodyRecipientsItemUserAlias.builder().aliasLabel("example_label").aliasName("example_name").build()).build())).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CanvasTriggerSendCreateBody;
import com.yourorg.brazejava.model.CanvasTriggerSendCreateBodyAudience;
import com.yourorg.brazejava.model.CanvasTriggerSendCreateBodyCanvasEntryProperties;
import com.yourorg.brazejava.model.CanvasTriggerSendCreateBodyRecipientsItem;
import com.yourorg.brazejava.model.CanvasTriggerSendCreateBodyRecipientsItemAttributes;
import com.yourorg.brazejava.model.CanvasTriggerSendCreateBodyRecipientsItemUserAlias;
import com.yourorg.brazejava.resources.canvas.trigger.send.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.canvas().trigger().send().create(CreateRequest
                .builder()
                .data(CanvasTriggerSendCreateBody
                      .builder()
                      .audience(CanvasTriggerSendCreateBodyAudience
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
                      .canvasEntryProperties(CanvasTriggerSendCreateBodyCanvasEntryProperties
                              .builder()
                              .productName("shoes")
                              .productPrice(79.99)
                              .build())
                      .canvasId("canvas_identifier")
                      .recipients(List.of(
                                      CanvasTriggerSendCreateBodyRecipientsItem
                                      .builder()
                                      .attributes(CanvasTriggerSendCreateBodyRecipientsItemAttributes
                                              .builder()
                                              .firstName("Alex")
                                              .build())
                                      .canvasEntryProperties("")
                                      .externalUserId("user_identifier")
                                      .sendToExistingOnly(true)
                                      .triggerProperties(Map.ofEntries(

                                              ))
                                      .userAlias(CanvasTriggerSendCreateBodyRecipientsItemUserAlias
                                              .builder()
                                              .aliasLabel("example_label")
                                              .aliasName("example_name")
                                              .build())
                                      .build()
                                  ))
                      .build())
                .build());
```
