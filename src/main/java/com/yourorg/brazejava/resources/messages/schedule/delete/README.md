
### Delete Scheduled Messages <a name="create"></a>

> Use this endpoint to cancel a message that you previously scheduled before it has been sent. 
  

To use this endpoint, you’ll need to generate an API key with the `messages.schedule.delete` permission.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `schedule_id` | Required | String | The schedule_id to delete (obtained from the response to create schedule). |

**API Endpoint**: `POST /messages/schedule/delete`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `MessagesScheduleDeleteCreateBody.builder().scheduleId("schedule_identifier").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.MessagesScheduleDeleteCreateBody;
import com.yourorg.brazejava.resources.messages.schedule.delete.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.messages().schedule().delete().create(CreateRequest
                .builder()
                .data(MessagesScheduleDeleteCreateBody
                      .builder()
                      .scheduleId("schedule_identifier")
                      .build())
                .build());
```
