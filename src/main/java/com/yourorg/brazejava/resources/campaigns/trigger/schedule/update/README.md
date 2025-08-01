
### Update Scheduled API Triggered Campaigns <a name="create"></a>

> Use this endpoint to update scheduled API-triggered campaigns created in the dashboard, allowing you to decide what action should trigger the message to be sent. 
  

To use this endpoint, you’ll need to generate an API key with the `campaigns.trigger.schedule.update` permission.

You can pass in `trigger_properties` that will be templated into the message itself.

Note that to send messages with this endpoint, you must have a campaign ID, created when you build an [API-triggered campaign](https://www.braze.com/docs/api/api_campaigns/).

Any schedule will completely overwrite the one that you provided in the create schedule request or in previous update schedule requests. For example, if you originally provide `"schedule" : {"time" : "2015-02-20T13:14:47", "in_local_time" : true}` and then in your update you provide `"schedule" : {"time" : "2015-02-20T14:14:47"}`, your message will now be sent at the provided time in UTC, not in the user's local time. Scheduled triggers that are updated very close to or during the time they were supposed to be sent will be updated with best efforts, so last-second changes could be applied to all, some, or none of your targeted users.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `campaign_id` | Required | String | See [campaign identifier](https://www.braze.com/docs/api/identifier_types/) |
| `schedule_id` | Optional | String | The `schedule_id` to update (obtained from the response to create schedule). |
| `schedule` | Required | Object | See [schedule object](https://www.braze.com/docs/api/objects_filters/schedule_object/). |

**API Endpoint**: `POST /campaigns/trigger/schedule/update`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `CampaignsTriggerScheduleUpdateCreateBody.builder().campaignId("campaign_identifier").schedule(CampaignsTriggerScheduleUpdateCreateBodySchedule.builder().inLocalTime(true).time("2017-05-24T21:30:00Z").build()).scheduleId("schedule_identifier").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CampaignsTriggerScheduleUpdateCreateBody;
import com.yourorg.brazejava.model.CampaignsTriggerScheduleUpdateCreateBodySchedule;
import com.yourorg.brazejava.resources.campaigns.trigger.schedule.update.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.campaigns().trigger().schedule().update().create(CreateRequest
                .builder()
                .data(CampaignsTriggerScheduleUpdateCreateBody
                      .builder()
                      .campaignId("campaign_identifier")
                      .schedule(CampaignsTriggerScheduleUpdateCreateBodySchedule
                                .builder()
                                .inLocalTime(true)
                                .time("2017-05-24T21:30:00Z")
                                .build())
                      .scheduleId("schedule_identifier")
                      .build())
                .build());
```
