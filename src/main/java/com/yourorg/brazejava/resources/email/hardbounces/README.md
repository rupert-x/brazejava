
### Query Hard Bounced Emails <a name="list"></a>

> Use this endpoint to pull a list of email addresses that have “hard bounced” your email messages within a certain time frame. 
  

To use this endpoint, you’ll need to generate an API key with the `email.hard_bounces` permission.

**Note:** You must provide an `end_date`, as well as either an `email` or a `start_date`. If you provide all three, `start_date`, `end_date`, and an `email`, we prioritize the emails given and disregard the date range.

If your date range has more than `limit` number of hard bounces, you will need to make multiple API calls, each time increasing the `offset` until a call returns either fewer than `limit` or zero results.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Example request

```
curl --location --request GET 'https://rest.iad-01.braze.com/email/hard_bounces?start_date=2019-01-01&end_date=2019-02-01&limit=100&offset=1&email=example@braze.com' \
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
      "hard_bounced_at": "2016-08-25 15:24:32 +0000"
    },
    {
      "email": "example2@braze.com",
      "hard_bounced_at": "2016-08-24 17:41:58 +0000"
    },
    {
      "email": "example3@braze.com",
      "hard_bounced_at": "2016-08-24 12:01:13 +0000"
    }
  ],
  "message": "success"
}

```

**API Endpoint**: `GET /email/hard_bounces`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `email` | ✗ | (Optional*) String  If provided, we will return whether or not the user has hard bounced.  *You must provide either an `email` or a `start_date`, and an `end_date`. | `"example@braze.com"` |
| `end_date` | ✗ | (Optional*) String in YYYY-MM-DD format  String in YYYY-MM-DD format. End date of the range to retrieve hard bounces. This is treated as midnight in UTC time by the API.  *You must provide either an `email` or a `start_date`, and an `end_date`. | `"2019-02-01"` |
| `limit` | ✗ | (Optional) Integer  Optional field to limit the number of results returned. Defaults to 100, maximum is 500. | `100` |
| `offset` | ✗ | (Optional) Integer  Optional beginning point in the list to retrieve from. | `1` |
| `start_date` | ✗ | (Optional*) String in YYYY-MM-DD format   Start date of the range to retrieve hard bounces, must be earlier than `end_date`. This is treated as midnight in UTC time by the API.  *You must provide either an `email` or a `start_date`, and an `end_date`.  | `"2019-01-01"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.email.hardbounces.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.email().hardBounces().list(ListRequest
                .builder()
                .email("example@braze.com")
                .endDate("2019-02-01")
                .limit(100)
                .offset(1)
                .startDate("2019-01-01")
                .build());
```
