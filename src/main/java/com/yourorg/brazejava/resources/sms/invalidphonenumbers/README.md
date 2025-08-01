
### Query Invalid Phone Numbers <a name="list"></a>

> Use this endpoint to pull a list of phone numbers that have been deemed “invalid” within a certain time frame. 
  

To use this endpoint, you’ll need to generate an API key with the `sms.invalid_phone_numbers` permission.

- If you provide a `start_date`, an `end_date`, and `phone_numbers`, we prioritize the given phone numbers and disregard the date range.
- If your date range has more than the `limit` number of invalid phone numbers, you will need to make multiple API calls with increasing the `offset` each time until a call returns either fewer than `limit` or zero results.
    

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Response

Entries are listed in descending order.

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "sms": [
    {
      "phone": "12345678900",
      "invalid_detected_at": "2016-08-25 15:24:32 +0000"
    },
    {
      "phone": "12345678901",
      "invalid_detected_at": "2016-08-24 17:41:58 +0000"
    },
    {
      "phone": "12345678902",
      "invalid_detected_at": "2016-08-24 12:01:13 +0000"
    }
  ],
  "message": "success"
}

```

**API Endpoint**: `GET /sms/invalid_phone_numbers`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `end_date` | ✗ | (Optional*) String in YYYY-MM-DD format  End date of the range to retrieve invalid phone numbers. This is treated as midnight in UTC time by the API.  | `"2018-09-01"` |
| `limit` | ✗ | (Optional) Integer Optional field to limit the number of results returned. Defaults to 100, maximum is 500. | `100` |
| `offset` | ✗ | (Optional) Integer Optional beginning point in the list to retrieve from. | `1` |
| `phone_numbers` | ✗ | (Optional*) Array of Strings in e.164 format If provided, we will return the phone number if it has been found to be invalid.  | `12345678901` |
| `start_date` | ✗ | (Optional*) String in YYYY-MM-DD format  Start date of the range to retrieve invalid phone numbers, must be earlier than `end_date`. This is treated as midnight in UTC time by the API.  | `"2018-09-01"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.sms.invalidphonenumbers.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.sms().invalidPhoneNumbers().list(ListRequest
                .builder()
                .endDate("2018-09-01")
                .limit(100)
                .offset(1)
                .phoneNumbers(12345678901)
                .startDate("2018-09-01")
                .build());
```
