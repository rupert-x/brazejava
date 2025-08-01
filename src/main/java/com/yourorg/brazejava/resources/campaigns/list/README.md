
### Export Campaign List <a name="list"></a>

> Use this endpoint to export a list of campaigns, each of which will include its name, campaign API identifier, whether it is an API campaign, and tags associated with the campaign. 
  

The campaigns are returned in groups of 100 sorted by time of creation (oldest to newest by default).

To use this endpoint, you’ll need to generate an API key with the `campaigns.list` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Campaign list endpoint API response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) the status of the export, returns 'success' when completed without errors,
    "campaigns" : [
        {
            "id" : (string) Campaign API Identifier,
            "last_edited": (ISO 8601 string) the last edited time for the message 
            "name" : (string) campaign name,
            "is_api_campaign" : (boolean) whether the campaign is an API Campaign,
            "tags" : (array) tag names associated with the campaign
        },
        ...
    ]
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /campaigns/list`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `include_archived` | ✗ | (Optional) Boolean  Whether or not to include archived campaigns, defaults to false. | `true` |
| `last_edit.time[gt]` | ✗ | (Optional) Datetime ([ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) string)  Filters the results and only returns campaigns that were edited greater than the time provided till now. Format is `yyyy-MM-DDTHH:mm:ss`. | `"2020-06-28T23:59:59-5:00"` |
| `page` | ✗ | (Optional) Integer  The page of campaigns to return, defaults to 0 (returns the first set of up to 100). | `123` |
| `sort_direction` | ✗ | (Optional) String  - Sort creation time from newest to oldest: pass in the value `desc`. - Sort creation time from oldest to newest: pass in the value `asc`.  If `sort_direction` is not included, the default order is oldest to newest. | `"desc"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.campaigns.list.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.campaigns().list().list(ListRequest
                .builder()
                .lastEditTimeGt("2020-06-28T23:59:59-5:00")
                .sortDirection("desc")
                .build());
```
