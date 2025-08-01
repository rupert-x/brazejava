
### Export News Feed Cards Details <a name="list"></a>

> Use this endpoint to retrieve relevant information on a card, which can be identified by the `card_id`. 
  

Note: If you are using our [older navigation](https://www.braze.com/docs/navigation), `card_id` can be found at **Developer Console > API Settings**.

To use this endpoint, you’ll need to generate an API key with the `feed.details` permission.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
    "message": (required, string) The status of the export, returns 'success' when completed without errors,
    "created_at" : (string) Date created as ISO 8601 date,
    "updated_at" : (string) Date last updated as ISO 8601 date,
    "name" : (string) Card name,
    "publish_at" : (string) Date card was published as ISO 8601 date,
    "end_at" : (string) Date card will stop displaying for users as ISO 8601 date,
    "tags" : (array) Tag names associated with the card,
    "title" : (string) Title of the card,
    "image_url" : (string) Image URL used by this card,
    "extras" : (dictionary) Dictionary containing key-value pair data attached to this card,
    "description" : (string) Description text used by this card,
    "archived": (boolean) whether this Card is archived,
    "draft": (boolean) whether this Card is a draft,
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /feed/details`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `card_id` | ✗ | (Required) String  See [Card API identifier](https://www.braze.com/docs/api/identifier_types/).  The `card_id` for a given card can be found in the **Settings > Setup and Testing > API Keys** page and on the card details page within your dashboard, or you can use the [News Feed List Endpoint](https://www.braze.com/docs/api/endpoints/export/news_feed/get_news_feed_cards/). | `"{{card_identifier}}"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.feed.details.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.feed().details().list(ListRequest
                .builder()
                .cardId("{{card_identifier}}")
                .build());
```
