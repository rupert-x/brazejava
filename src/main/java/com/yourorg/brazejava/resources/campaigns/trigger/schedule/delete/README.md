
### Delete Scheduled API Triggered Campaigns <a name="create"></a>

> The delete schedule endpoint allows you to cancel a message that you previously scheduled API-triggered Canvases before it has been sent. 
  

To use this endpoint, you’ll need to generate an API key with the `campaigns.trigger.schedule.delete` permission.

Scheduled messages or triggers that are deleted very close to or during the time they were supposed to be sent will be updated with best efforts, so last-second deletions could be applied to all, some, or none of your targeted users.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `campaign_id` | Required | String | See [campaign identifier](https://www.braze.com/docs/api/identifier_types/). |
| `schedule_id` | Required | String | The `schedule_id` to delete (obtained from the response to create schedule). |

**API Endpoint**: `POST /campaigns/trigger/schedule/delete`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `CampaignsTriggerScheduleDeleteCreateBody.builder().campaignId("campaign_identifier").scheduleId("schedule_identifier").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CampaignsTriggerScheduleDeleteCreateBody;
import com.yourorg.brazejava.resources.campaigns.trigger.schedule.delete.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.campaigns().trigger().schedule().delete().create(CreateRequest
                .builder()
                .data(CampaignsTriggerScheduleDeleteCreateBody
                      .builder()
                      .campaignId("campaign_identifier")
                      .scheduleId("schedule_identifier")
                      .build())
                .build());
```
