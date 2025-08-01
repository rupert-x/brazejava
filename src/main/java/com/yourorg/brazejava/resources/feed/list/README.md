
### Export News Feed Cards List <a name="list"></a>

> Use this endpoint to export a list of News Feed cards, each of which will include its name and card API identifier. 
  

The cards are returned in groups of 100 sorted by time of creation (oldest to newest by default).

To use this endpoint, you’ll need to generate an API key with the `feed.list` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "cards" : [
        {
            "id" : (string) Card API Identifier,
            "type" : (string) type of the card - NewsItem (classic cards), CaptionedImage, Banner or DevPick (cross-promotional cards),
            "title" : (string) title of the card,
            "tags" : (array) tag names associated with the card
        },
        ...
    ]
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /feed/list`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `include_archived` | ✗ | (Optional) Boolean  Whether or not to include archived cards, defaults to false. | `true` |
| `page` | ✗ | (Optional) Integer  The page of cards to return, defaults to 0 (returns the first set of up to 100). | `1` |
| `sort_direction` | ✗ | (Optional) String  - Sort creation time from newest to oldest: pass in the value `desc`. - Sort creation time from oldest to newest: pass in the value `asc`.  If `sort_direction` is not included, the default order is oldest to newest. | `"desc"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.feed.list.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.feed().list().list(ListRequest
                .builder()
                .includeArchived(true)
                .page(1)
                .sortDirection("desc")
                .build());
```
