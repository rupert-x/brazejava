
### Update User Alias <a name="create"></a>

> Use this endpoint to update existing user aliases. 
  

To use this endpoint, you’ll need to generate an API key with the `users.alias.update` permission.

Up to 50 user aliases may be specified per request.

This endpoint does not guarantee the sequence of `alias_updates` objects being updated.

Updating a user alias requires `alias_label`, `old_alias_name`, and `new_alias_name` to be included in the update user alias object. If there is no user alias associated with the `alias_label` and `old_alias_name`, no alias will be updated. If the given `alias_label` and `old_alias_name` is found, then the `old_alias_name` will be updated to the `new_alias_name`.

## Rate limit

For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/delete`, `/users/identify`, `/users/merge`, and `/users/alias/update` endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `alias_updates` | Required | Array of update user alias objects | See [user alias object](https://www.braze.com/docs/api/objects_filters/user_alias_object/).  <br>  <br>For more information on `old_alias_name`, `new_alias_name`, and `alias_label`, refer to [User aliases](https://www.braze.com/docs/user_guide/data_and_analytics/user_data_collection/user_profile_lifecycle/#user-aliases). |

### Endpoint request body with update user alias object specification

``` json
{
  "alias_label" : (required, string),
  "old_alias_name" : (required, string),
  "new_alias_name" : (required, string)
}

```

**API Endpoint**: `POST /users/alias/update`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `UsersAliasUpdateCreateBody.builder().aliasUpdates(List.of(UsersAliasUpdateCreateBodyAliasUpdatesItem.builder().aliasLabel("example_alias_label").newAliasName("example_new_alias_name").oldAliasName("example_old_alias_name").build())).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.UsersAliasUpdateCreateBody;
import com.yourorg.brazejava.model.UsersAliasUpdateCreateBodyAliasUpdatesItem;
import com.yourorg.brazejava.resources.users.alias.update.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.users().alias().update().create(CreateRequest
                .builder()
                .data(UsersAliasUpdateCreateBody
                      .builder()
                      .aliasUpdates(List.of(
                                        UsersAliasUpdateCreateBodyAliasUpdatesItem
                                        .builder()
                                        .aliasLabel("example_alias_label")
                                        .newAliasName("example_new_alias_name")
                                        .oldAliasName("example_old_alias_name")
                                        .build()
                                    ))
                      .build())
                .build());
```
