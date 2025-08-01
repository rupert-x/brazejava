
### Update Content Block <a name="create"></a>

> Use this endpoint to update a [Content Block](https://www.braze.com/docs/user_guide/engagement_tools/templates_and_media/content_blocks/). 
  

To use this endpoint, you’ll need to generate an API key with the `content_blocks.update` permission.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/)

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `content_block_id` | Required | String | Your content block's API identifier. |
| `name` | Required | String | Name of the content block. Must be less than 100 characters. |
| `description` | Optional | String | Description of the content block. Must be less than 250 characters. |
| `content` | Required | String | HTML or text content within content blocks. |
| `state` | Optional | String | Choose `active` or `draft`. Defaults to `active` if not specified. |
| `tags` | Optional | Array of strings | [Tags](https://www.braze.com/docs/user_guide/administrative/app_settings/manage_app_group/tags/) must already exist. |

### Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "content_block_id": (string) Your newly generated block id,
  "liquid_tag": (string) The generated block tag from the Content Block name,
  "created_at": (string) The time the Content Block was created in ISO 8601,
  "message": "success"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `Content cannot be blank` |  |
| `Content must be a string` | Make sure your content is encapsulated in quotes (`""`). |
| `Content must be smaller than 50kb` | The content in your Content Block must be less than 50kb total. |
| `Content contains malformed liquid` | The Liquid provided is not valid or parsable. Try again with valid Liquid or reach out to support. |
| `Content Block cannot be referenced within itself` |  |
| `Content Block description cannot be blank` |  |
| `Content Block description must be a string` | Make sure your Content Block description is encapsulated in quotes (`""`). |
| `Content Block description must be shorter than 250 characters` |  |
| `Content Block name cannot be blank` |  |
| `Content Block name must be shorter than 100 characters` |  |
| `Content Block name can only contain alphanumeric characters` | Content Block names can include any of the following characters: the letters (capitalized or lowercase) `A` through `Z`, the numbers `0` through `9`, dashes `-`, and underscores `_`. It cannot contain non-alphanumeric characters like emojis, `!`, `@`, `~`, `&`, and other "special" characters. |
| `Content Block with this name already exists` | Try a different name. |
| `Content Block name cannot be updated for active Content Blocks` |  |
| `Content Block state must be either active or draft` |  |
| `Active Content Block can not be updated to Draft. Create a new Content Block.` |  |
| `Tags must be an array` | Tags must be formatted as an array of strings, for example `["marketing", "promotional", "transactional"]`. |
| `All tags must be strings` | Make sure your tags are encapsulated in quotes (`""`). |
| `Some tags could not be found` | To add a tag when creating a Content Block, the tag must already exist in Braze. |

**API Endpoint**: `POST /content_blocks/update`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `ContentBlocksUpdateCreateBody.builder().content("HTML or text content within block").contentBlockId("content_block_id").description("This is my content block").name("content_block").state("draft").tags(List.of("marketing")).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.ContentBlocksUpdateCreateBody;
import com.yourorg.brazejava.resources.contentblocks.update.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.contentBlocks().update().create(CreateRequest
                .builder()
                .data(ContentBlocksUpdateCreateBody
                      .builder()
                      .content("HTML or text content within block")
                      .contentBlockId("content_block_id")
                      .description("This is my content block")
                      .name("content_block")
                      .state("draft")
                      .tags(List.of(
                                "marketing"
                            ))
                      .build())
                .build());
```
