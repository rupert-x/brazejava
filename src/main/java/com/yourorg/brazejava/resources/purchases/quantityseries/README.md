
### Export Number of Purchases <a name="list"></a>

> Use this endpoint to return the total number of purchases in your app over a time range. 
  

To use this endpoint, you’ll need to generate an API key with the `purchases.quantity_series` permission.

## Rate limit

For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 1,000 requests per hour to this endpoint. This rate limit is shared with the `/events/list` endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Example request

```
curl --location --request GET 'https://rest.iad-01.braze.com/purchases/quantity_series?length=100' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'

```

## Response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "message": (required, string) the status of the export, returns 'success' when completed without errors,
  "data" : [
    {
      "time" : (string) the date as ISO 8601 date,
      "purchase_quantity" : (int) the number of items purchased in the time period
      },
    ...
  ]
}

```

> **Tip:** For help with CSV and API exports, visit [Export troubleshooting](https://www.braze.com/docs/user_guide/data_and_analytics/export_braze_data/export_troubleshooting/).

**API Endpoint**: `GET /purchases/quantity_series`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `app_id` | ✗ | (Optional) String App API identifier retrieved from the Settings > Setup and Testing > API Keys to limit analytics to a specific app. | `"{{app_identifier}}"` |
| `ending_at` | ✗ | (Optional) Datetime (ISO 8601 string) Date on which the data series should end. Defaults to time of the request. | `"2018-06-28T23:59:59-5:00"` |
| `length` | ✗ | (Required) Integer Maximum number of days before ending_at to include in the returned series. Must be between 1 and 100 (inclusive). | `100` |
| `product` | ✗ | (Optional) String Name of product to filter response by. If excluded, results for all apps will be returned. | `"name"` |
| `unit` | ✗ | (Optional) String Unit of time between data points. Can be `day` or `hour`, defaults to `day`.  | `14` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.purchases.quantityseries.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.purchases().quantitySeries().list(ListRequest
                .builder()
                .appId("{{app_identifier}}")
                .endingAt("2018-06-28T23:59:59-5:00")
                .length(100)
                .product("name")
                .unit(14)
                .build());
```
