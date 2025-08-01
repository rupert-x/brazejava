
### Create New User Aliases <a name="create"></a>

> Use this endpoint to add new user aliases for existing identified users, or to create new unidentified users. 
  

To use this endpoint, you’ll need to generate an API key with the `users.alias.new` permission.

Up to 50 user aliases may be specified per request.

**Adding a user alias for an existing user** requires an `external_id` to be included in the new user alias object. If the `external_id` is present in the object but there is no user with that `external_id`, the alias will not be added to any users. If an `external_id` is not present, a user will still be created but will need to be identified later. You can do this using the "Identifying Users" and the `users/identify` endpoint.

**Creating a new alias-only user** requires the `external_id` to be omitted from the new user alias object. Once the user is created, use the `/users/track` endpoint to associate the alias-only user with attributes, events, and purchases, and the `/users/identify` endpoint to identify the user with an `external_id`.

### Rate limit

For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/delete` and `/users/identify` endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `user_aliases` | Required | Array of new user alias objects | See [user alias object](https://www.braze.com/docs/api/objects_filters/user_alias_object/).  <br>  <br>For more information on `alias_name` and `alias_label`, check out our [User Aliases](https://www.braze.com/docs/user_guide/data_and_analytics/user_data_collection/user_profile_lifecycle/#user-aliases) documentation. |

**API Endpoint**: `POST /users/alias/new`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `UsersAliasNewCreateBody.builder().userAliases(List.of(UsersAliasNewCreateBodyUserAliasesItem.builder().aliasLabel("example_label").aliasName("example_name").externalId("external_identifier").build())).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.UsersAliasNewCreateBody;
import com.yourorg.brazejava.model.UsersAliasNewCreateBodyUserAliasesItem;
import com.yourorg.brazejava.resources.users.alias.new__.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.users().alias().new_().create(CreateRequest
                .builder()
                .data(UsersAliasNewCreateBody
                      .builder()
                      .userAliases(List.of(
                                       UsersAliasNewCreateBodyUserAliasesItem
                                       .builder()
                                       .aliasLabel("example_label")
                                       .aliasName("example_name")
                                       .externalId("external_identifier")
                                       .build()
                                   ))
                      .build())
                .build());
```
