
### List Upcoming Scheduled Campaigns and Canvases <a name="list"></a>

> Use this endpoint to return a JSON list of information about scheduled campaigns and entry Canvases between now and a designated `end_time` specified in the request. 
  

To use this endpoint, you’ll need to generate an API key with the `messages.schedule_broadcasts` permission.

Daily, recurring messages will only appear once with their next occurrence. Results returned in this endpoint are only for campaigns and Canvases created and scheduled in Braze.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "scheduled_broadcasts": [
    {
      "name" (string) the name of the scheduled boradcast,
      "id" (stings) the Canvas or campaign identifier,
      "type" (string) the broadcast type either Canvas or Campaign,
      "tags" (array) an array of tag names formatted as strings,
      "next_send_time" (string) The next send time formatted in ISO 8601, may also include time zone if not local/intelligent delivery,
      "schedule_type" (string) The schedule type, either local_time_zones, intelligent_delivery or the name of your company's time zone,
    },
  ]
}

```

**API Endpoint**: `GET /messages/scheduled_broadcasts`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `end_time` | ✗ | (Required) String in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) format  End date of the range to retrieve upcoming scheduled Campaigns and Canvases. This is treated as midnight in UTC time by the API. | `"2018-09-01T00:00:00-04:00"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.messages.scheduledbroadcasts.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.messages().scheduledBroadcasts().list(ListRequest
                .builder()
                .endTime("2018-09-01T00:00:00-04:00")
                .build());
```
