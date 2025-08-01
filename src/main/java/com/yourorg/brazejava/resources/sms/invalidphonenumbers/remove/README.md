
### Remove Invalid Phone Numbers <a name="create"></a>

> Use this endpoint to remove “invalid” phone numbers from Braze’s invalid list. 
  

To use this endpoint, you’ll need to generate an API key with the `sms.invalid_phone_numbers.remove` permission.

This can be used to re-validate phone numbers after they have been marked as invalid.

## Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `phone_number` | Required | Array of strings in e.164 format | An array of up to 50 phone numbers to modify. |

**API Endpoint**: `POST /sms/invalid_phone_numbers/remove`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `SmsInvalidPhoneNumbersRemoveCreateBody.builder().phoneNumbers(List.of("12183095514","14255551212")).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.SmsInvalidPhoneNumbersRemoveCreateBody;
import com.yourorg.brazejava.resources.sms.invalidphonenumbers.remove.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.sms().invalidPhoneNumbers().remove().create(CreateRequest
                .builder()
                .data(SmsInvalidPhoneNumbersRemoveCreateBody
                      .builder()
                      .phoneNumbers(List.of(
                                        "12183095514",
                                        "14255551212"
                                    ))
                      .build())
                .build());
```
