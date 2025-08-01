
### Generate Preference Center URL <a name="get"></a>

> Use this endpoint to generate a URL for a preference center. 
  

To use this endpoint, you’ll need to generate an API key with the `preference_center.user.get` permission.

Each preference center URL is unique to each user.

## Rate limit

This endpoint has a rate limit of 1,000 requests per minute, per workspace.

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `preferenceCenterExternalID` | Required | String | The ID for your preference center. |
| `userID` | Required | String | The user ID. |

## Example request

```
curl --location --request GET 'https://rest.iad-01.braze.com/preference_center/v1/$preference_center_external_id/url/$user_external_id' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE'

```

## Response

``` json
{
  "preference_center_url": "https://www.example.com/preferences"
}

```

**API Endpoint**: `GET /preference_center_v1/{PreferenceCenterExternalID}/url/{UserID}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `PreferenceCenterExternalID` | ✓ |  | `"string"` |
| `UserID` | ✓ |  | `"string"` |
| `external_id` | ✗ | (Required) String | `"{{external_id}}"` |
| `preference_center_api_id` | ✗ |  | `"{{preference_center_api_id}}"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.preferencecenterv1.url.params.GetRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.preferenceCenterV1().url().get(GetRequest
                .builder()
                .preferenceCenterExternalId("string")
                .userId("string")
                .externalId("{{external_id}}")
                .preferenceCenterApiId("{{preference_center_api_id}}")
                .build());
```
