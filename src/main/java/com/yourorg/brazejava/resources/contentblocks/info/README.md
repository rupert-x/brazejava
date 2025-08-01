
### See Content Block Information <a name="list"></a>

> Use this endpoint to call information for your existing [Content Blocks](https://www.braze.com/docs/user_guide/engagement_tools/templates_and_media/content_blocks/). 
  

To use this endpoint, you’ll need to generate an API key with the `content_blocks.info` permission.

**Note:** If you are using our [older navigation](https://www.braze.com/docs/navigation), `content_block_id`can be found at ****Developer Console** > **API Settings****.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR_REST_API_KEY
{
  "content_block_id": "string",
  "name": "string",
  "content": "string",
  "description": "string",
  "content_type": "html or text",
  "tags":  "array of strings",
  "created_at": "time-in-iso",
  "last_edited": "time-in-iso",
  "inclusion_count" : "integer",
  "message": "success"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `Content Block ID cannot be blank` | Make sure that a Content Block is listed in your request and is encapsulated in quotes (`""`). |
| `Content Block ID is invalid for this App Group` | This Content Block doesn't exist or is in a different company account or app group. |
| `Content Block has been deleted—content not available` | This Content Block, though it may have existed earlier, has been deleted. |
| `Include Inclusion Data—error` | This parameter only accepts boolean values (true or false). Make sure the value for `include_inclusion_data` is not encapsulated in quotes (`""`), which causes the value to be sent as a string instead. See [request parameters](#request-parameters) for details. |

**API Endpoint**: `GET /content_blocks/info`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `content_block_id` | ✗ | (Required) String  The content block identifier.   You can find this by either listing content block information through an API call or going to **Settings > Setup and Testing > API Keys**, then scrolling to the bottom and searching for your content block API identifier. | `"{{content_block_id}}"` |
| `include_inclusion_data` | ✗ | (Optional) Boolean  When set to `true`, the API returns back the Message Variation API identifier of campaigns and Canvases where this content block is included, to be used in subsequent calls. The results exclude archived or deleted Campaigns or Canvases. | `true` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.contentblocks.info.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.contentBlocks().info().list(ListRequest
                .builder()
                .contentBlockId("{{content_block_id}}")
                .build());
```
