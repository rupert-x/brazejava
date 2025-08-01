
### Query List of Unsubscribed Email Addresses <a name="list"></a>

> Use this endpoint to return emails that have unsubscribed during the time period from `start_date` to `end_date`. 
  

You can use this endpoint to set up a bi-directional sync between Braze and other email systems or your own database.

To use this endpoint, you’ll need to generate an API key with the `email.unsubscribe` permission.

**Note:** You must provide an `end_date`, as well as either an `email` or a `start_date`.

If your date range has more than `limit` number of unsubscribes, you will need to make multiple API calls, each time increasing the `offset` until a call returns either fewer than `limit` or zero results.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Example request

```
curl --location --request GET 'https://rest.iad-01.braze.com/email/unsubscribes?start_date=2020-01-01&end_date=2020-02-01&limit=1&offset=1&sort_direction=desc&email=example@braze.com' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE'

```

## Response

Entries are listed in descending order.

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "emails": [
    {
      "email": "example1@braze.com",
      "unsubscribed_at": "2016-08-25 15:24:32 +0000"
    },
    {
      "email": "example2@braze.com",
      "unsubscribed_at": "2016-08-24 17:41:58 +0000"
    },
    {
      "email": "example3@braze.com",
      "unsubscribed_at": "2016-08-24 12:01:13 +0000"
    }
  ],
  "message": "success"
}

```

**API Endpoint**: `GET /email/unsubscribes`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `email` | ✗ | (Optional*) String  If provided, we will return whether or not the user has unsubscribed. | `"example@braze.com"` |
| `end_date` | ✗ | (Optional*)  String in YYYY-MM-DD format  End date of the range to retrieve unsubscribes. This is treated as midnight in UTC time by the API. | `"2020-02-01"` |
| `limit` | ✗ | (Optional) Integer  Optional field to limit the number of results returned. Limit must be greater than 1. Defaults to 100, maximum is 500. | `1` |
| `offset` | ✗ | (Optional) Integer   Optional beginning point in the list to retrieve from. | `1` |
| `sort_direction` | ✗ | (Optional) String  Pass in the value `asc` to sort unsubscribes from oldest to newest. Pass in `desc` to sort from newest to oldest. If sort_direction is not included, the default order is newest to oldest. | `"desc"` |
| `start_date` | ✗ | (Optional*) String in YYYY-MM-DD format  Start date of the range to retrieve unsubscribes, must be earlier than end_date. This is treated as midnight in UTC time by the API. | `"2020-01-01"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.email.unsubscribes.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.email().unsubscribes().list(ListRequest
                .builder()
                .email("example@braze.com")
                .endDate("2020-02-01")
                .limit(1)
                .offset(1)
                .sortDirection("desc")
                .startDate("2020-01-01")
                .build());
```
