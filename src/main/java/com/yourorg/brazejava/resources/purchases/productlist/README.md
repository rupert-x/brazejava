
### Export Product IDs <a name="list"></a>

> Use this endpoint to return a paginated lists of product IDs. 
  

To use this endpoint, you’ll need to generate an API key with the `purchases.product_list` permission.

## Rate limit

For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 1,000 requests per hour to this endpoint. This rate limit is shared with the `/events/list` endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "products": [
    "product_name" (string), the name of the product
  ],
  "message": "success"
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /purchases/product_list`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `page` | ✗ | (Optional) Integer  The page of your product list that you would like to view. | `1` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.purchases.productlist.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.purchases().productList().list(ListRequest
                .builder()
                .page(1)
                .build());
```
