
### Export Canvas List <a name="list"></a>

> Use this endpoint to export a list of Canvases, including the name, Canvas API identifier and associated tags. 
  

Canvases are returned in groups of 100 sorted by time of creation (oldest to newest by default).

Archived Canvases will not be included in the API response unless the `include_archived` field is specified. Canvases that are stopped but not archived, however, will be returned by default.

To use this endpoint, you’ll need to generate an API key with the `canvas.list` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "canvases" : [
      {
          "id" : (string) Canvas API Identifier,
          "last_edited": (ISO 8601 string) the last edited time for the message,
          "name" : (string) Canvas name,
          "tags" : (array) tag names associated with the Canvas,
      },
    ... (more Canvases)
  ],
  "message": (required, string) the status of the export, returns 'success' when completed without errors
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://desktop.postman.com/?desktopVersion=9.19.0&userId=16580579&teamId=409325).

**API Endpoint**: `GET /canvas/list`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `include_archived` | ✗ | (Optional) Boolean  Whether or not to include archived Canvases, defaults to `false`. | `true` |
| `last_edit.time[gt]` | ✗ | (Optional) Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string)  Filters the results and only returns Canvases that were edited greater than the time provided till now. Format is `yyyy-MM-DDTHH:mm:ss`. | `"2020-06-28T23:59:59-5:00"` |
| `page` | ✗ | (Optional) Integer  The page of Canvases to return, defaults to `0` (returns the first set of up to 100). | `1` |
| `sort_direction` | ✗ | (Optional) String  - Sort creation time from newest to oldest: pass in the value `desc`. - Sort creation time from oldest to newest: pass in the value `asc`.  If `sort_direction` is not included, the default order is oldest to newest. | `"desc"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.canvas.list.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.canvas().list().list(ListRequest
                .builder()
                .lastEditTimeGt("2020-06-28T23:59:59-5:00")
                .page(1)
                .sortDirection("desc")
                .build());
```
