
### Delete Scheduled API-Triggered Canvases <a name="create"></a>

> Use this endpoint to cancel a Canvas message that you previously scheduled via API-triggered before it has been sent. 
  

To use this endpoint, you’ll need to generate an API key with the `canvas.trigger.schedule.delete` permission.

Scheduled messages or triggers that are deleted very close to or during the time they were supposed to be sent will be updated with best efforts, so last-second deletions could be applied to all, some, or none of your targeted users.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `canvas_id` | Required | String | See [Canvas identifier](https://braze.com/docs/api/identifier_types/). |
| `schedule_id` | Required | String | The `schedule_id` to delete (obtained from the response to create schedule). |

**API Endpoint**: `POST /canvas/trigger/schedule/delete`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `CanvasTriggerScheduleDeleteCreateBody.builder().canvasId("canvas_identifier").scheduleId("schedule_identifier").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CanvasTriggerScheduleDeleteCreateBody;
import com.yourorg.brazejava.resources.canvas.trigger.schedule.delete.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.canvas().trigger().schedule().delete().create(CreateRequest
                .builder()
                .data(CanvasTriggerScheduleDeleteCreateBody
                      .builder()
                      .canvasId("canvas_identifier")
                      .scheduleId("schedule_identifier")
                      .build())
                .build());
```
