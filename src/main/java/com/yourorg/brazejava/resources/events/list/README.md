
### Export Custom Events List <a name="list"></a>

> Use this endpoint to export a list of custom events that have been recorded for your app. The event names are returned in groups of 250, sorted alphabetically. 
  

To use this endpoint, you’ll need to generate an API key with the `events.list` permission.

## Rate limit

For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 1,000 requests per hour to this endpoint. This rate limit is shared with the `/purchases/product_list` endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "events" : [
        "Event A", (string) the event name,
        "Event B", (string) the event name,
        "Event C", (string) the event name,
        ...
    ]
}

```

### Fatal error response codes

For status codes and associated error messages that will be returned if your request encounters a fatal error, reference [Fatal errors & responses](https://www.braze.com/docs/api/errors/#fatal-errors).

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /events/list`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `page` | ✗ | (Optional) Integer  The page of event names to return, defaults to 0 (returns the first set of up to 250). | `3` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.events.list.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.events().list().list(ListRequest
                .builder()
                .page(3)
                .build());
```
