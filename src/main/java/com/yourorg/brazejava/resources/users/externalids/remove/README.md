
### Remove External ID <a name="create"></a>

> Use this endpoint to remove your users' old deprecated external IDs. 
  

To use this endpoint, you’ll need to generate an API key with the `users.external_ids.remove` permission.

You can send up to 50 external IDs per request. You will need to create a new [API key](https://www.braze.com/docs/api/api_key/) with permissions for this endpoint.

> **Warning:** This endpoint completely removes the deprecated ID and cannot be undone. Using this endpoint to remove deprecated \`external_ids\` that are still associated with users in your system can permanently prevent you from finding those users' data. 
  

## Rate limit

We apply a rate limit of 1,000 requests per minute to this endpoint, as documented in [API rate limits](http://braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `external_ids` | Required | Array of strings | External identifiers for the users to remove |

> Important: Only deprecated IDs can be removed; attempting to remove a primary external ID will result in an error. 
  

## Response

The response will confirm all successful removals, as well as unsuccessful removals with the associated errors. Error messages in the `removal_errors` field will reference the index in the array of the original request.

``` json
{
  "message" : (string) status message,
  "removed_ids" : (array of successful Remove Operations),
  "removal_errors": (array of any )
}

```

The `message` field will return `success` for any valid request. More specific errors are captured in the `removal_errors` array. The `message` field returns an error in the case of:

- Invalid API key
- Empty `external_ids` array
- `external_ids` array with more than 50 items
- Rate limit hit (>1,000 requests/minute)

**API Endpoint**: `POST /users/external_ids/remove`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `UsersExternalIdsRemoveCreateBody.builder().externalIds(List.of("existing_deprecated_external_id_string")).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.UsersExternalIdsRemoveCreateBody;
import com.yourorg.brazejava.resources.users.externalids.remove.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.users().externalIds().remove().create(CreateRequest
                .builder()
                .data(UsersExternalIdsRemoveCreateBody
                      .builder()
                      .externalIds(List.of(
                                       "existing_deprecated_external_id_string"
                                   ))
                      .build())
                .build());
```
