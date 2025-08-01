
### List Preference Centers <a name="list"></a>

> Use this endpoint to list your available preference centers. 
  

To use this endpoint, you’ll need to generate an API key with the `preference_center.list` permission.

## Rate limit

This endpoint has a rate limit of 1,000 requests per minute, per workspace.

## Path and request parameters

There are no path or request parameters for this endpoint.

## Example request

```
curl --location -g --request GET https://rest.iad-01.braze.com/preference_center/v1/list \
--header 'Authorization: Bearer YOUR-REST-API-KEY'

```

## Response

``` json
{
  "preference_centers": [
    {
      "name": "My Preference Center 1",
      "preference_center_api_id": "preference_center_api_id",
      "created_at": "2022-08-17T15:46:10Z",
      "updated_at": "2022-08-17T15:46:10Z"
    },
    {
      "name": "My Preference Center 2",
      "preference_center_api_id": "preference_center_api_id",
      "created_at": "2022-08-19T11:13:06Z",
      "updated_at": "2022-08-19T11:13:06Z"
    },
    {
      "name": "My Preference Center 3",
      "preference_center_api_id": "preference_center_api_id",
      "created_at": "2022-08-19T11:30:50Z",
      "updated_at": "2022-08-19T11:30:50Z"
    },
    {
      "name": "My Preference Center 4",
      "preference_center_api_id": "preference_center_api_id",
      "created_at": "2022-09-13T20:41:34Z",
      "updated_at": "2022-09-13T20:41:34Z"
    }
  ]
}

```

**API Endpoint**: `GET /preference_center/v1/list`

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.preferenceCenter().v1().list().list();
```
