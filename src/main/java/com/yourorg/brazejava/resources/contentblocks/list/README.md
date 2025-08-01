
### List Available Content Blocks <a name="list"></a>

> Use this endpoint to list your existing [Content Blocks](https://www.braze.com/docs/user_guide/engagement_tools/templates_and_media/content_blocks/) information. 
  

To use this endpoint, you’ll need to generate an API key with the `content_blocks.list` permission.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
{
  "count": "integer",
  "content_blocks": [
    {
      "content_block_id": "string",
      "name": "string",
      "content_type": "html or text",
      "liquid_tag": "string",
      "inclusion_count" : "integer",
      "created_at": "time-in-iso",
      "last_edited": "time-in-iso",
      "tags" : "array of strings"
    }
  ]
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `Modified after time is invalid` | The provided date is not a valid or parsable date. Reformat this value as a string in ISO 8601 format (`yyyy-mm-ddThh:mm:ss.ffffff`). |
| `Modified before time is invalid` | The provided date is not a valid or parsable date. Reformat this value as a string in ISO 8601 format (`yyyy-mm-ddThh:mm:ss.ffffff`). |
| `Modified after time must be earlier than or the same as modified before time.` | Change the `modified_after` value to a time that is earlier than the `modified_before` time. |
| `Content Block number limit is invalid` | The `limit` parameter must be an integer (positive number) greater than 0. |
| `Content Block number limit must be greater than 0` | Change the `limit` parameter to an integer greater than 0. |
| `Content Block number limit exceeds maximum of 1000` | Change the `limit` parameter to an integer less than 1000. |
| `Offset is invalid` | The `offset` parameter must be an integer greater than 0. |
| Offset must be greater than 0 | Change the `offset` parameter to an integer greater than 0. |

**API Endpoint**: `GET /content_blocks/list`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `limit` | ✗ | (Optional) Positive Number  Maximum number of content blocks to retrieve. Default to 100 if not provided, with a maximum acceptable value of 1000. | `100` |
| `modified_after` | ✗ | (Optional) String in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)  Retrieve only content blocks updated at or after the given time. | `"2020-01-01T01:01:01.000000"` |
| `modified_before` | ✗ | (Optional) String in [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)  Retrieve only content blocks updated at or before the given time. | `"2020-02-01T01:01:01.000000"` |
| `offset` | ✗ | (Optional) Positive Number  Number of content blocks to skip before returning rest of the templates that fit the search criteria. | `1` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.contentblocks.list.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.contentBlocks().list().list(ListRequest
                .builder()
                .limit(100)
                .modifiedAfter("2020-01-01T01:01:01.000000")
                .modifiedBefore("2020-02-01T01:01:01.000000")
                .offset(1)
                .build());
```
