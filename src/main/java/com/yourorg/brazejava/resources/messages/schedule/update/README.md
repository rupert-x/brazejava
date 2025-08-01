
### Update Scheduled Messages <a name="create"></a>

> Use this endpoint to update scheduled messages. 
  

To use this endpoint, you’ll need to generate an API key with the `messages.schedule.update` permission.

This endpoint accepts updates to either the `schedule` or `messages` parameter or both. Your request must contain at least one of those two keys.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `schedule_id` | Required | String | The `schedule_id` to update (obtained from the response to create schedule). |
| `schedule` | Optional | Object | See [schedule object](https://www.braze.com/docs/api/objects_filters/schedule_object/). |
| `messages` | Optional | Object | See available [message objects](https://www.braze.com/docs/api/objects_filters/#messaging-objects). |

**API Endpoint**: `POST /messages/schedule/update`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `MessagesScheduleUpdateCreateBody.builder().messages(MessagesScheduleUpdateCreateBodyMessages.builder().androidPush(MessagesScheduleUpdateCreateBodyMessagesAndroidPush.builder().alert("Updated message!").title("Updated title!").build()).applePush(MessagesScheduleUpdateCreateBodyMessagesApplePush.builder().alert("Updated Message!").badge(1).build()).sms(MessagesScheduleUpdateCreateBodyMessagesSms.builder().appId("app_identifier").body("This is my SMS body.").messageVariationId("message_variation_identifier").subscriptionGroupId("subscription_group_identifier").build()).build()).schedule(MessagesScheduleUpdateCreateBodySchedule.builder().time("2017-05-24T20:30:36Z").build()).scheduleId("schedule_identifier").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.MessagesScheduleUpdateCreateBody;
import com.yourorg.brazejava.model.MessagesScheduleUpdateCreateBodyMessages;
import com.yourorg.brazejava.model.MessagesScheduleUpdateCreateBodyMessagesAndroidPush;
import com.yourorg.brazejava.model.MessagesScheduleUpdateCreateBodyMessagesApplePush;
import com.yourorg.brazejava.model.MessagesScheduleUpdateCreateBodyMessagesSms;
import com.yourorg.brazejava.model.MessagesScheduleUpdateCreateBodySchedule;
import com.yourorg.brazejava.resources.messages.schedule.update.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.messages().schedule().update().create(CreateRequest
                .builder()
                .data(MessagesScheduleUpdateCreateBody
                      .builder()
                      .messages(MessagesScheduleUpdateCreateBodyMessages
                                .builder()
                                .androidPush(MessagesScheduleUpdateCreateBodyMessagesAndroidPush
                                        .builder()
                                        .alert("Updated message!")
                                        .title("Updated title!")
                                        .build())
                                .applePush(MessagesScheduleUpdateCreateBodyMessagesApplePush
                                        .builder()
                                        .alert("Updated Message!")
                                        .badge(1)
                                        .build())
                                .sms(MessagesScheduleUpdateCreateBodyMessagesSms
                                     .builder()
                                     .appId("app_identifier")
                                     .body("This is my SMS body.")
                                     .messageVariationId("message_variation_identifier")
                                     .subscriptionGroupId("subscription_group_identifier")
                                     .build())
                                .build())
                      .schedule(MessagesScheduleUpdateCreateBodySchedule
                                .builder()
                                .time("2017-05-24T20:30:36Z")
                                .build())
                      .scheduleId("schedule_identifier")
                      .build())
                .build());
```
