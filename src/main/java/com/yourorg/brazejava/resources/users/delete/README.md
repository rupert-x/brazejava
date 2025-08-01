
### Delete Users <a name="create"></a>

> Use this endpoint to delete any user profile by specifying a known user identifier. 
  

To use this endpoint, you’ll need to generate an API key with the `users.delete` permission.

Up to 50 `external_ids`, `user_aliases`, or `braze_ids` can be included in a single request. Only one of `external_ids`, `user_aliases`, or `braze_ids` can be included in a single request.

> **Important:** Deleting user profiles cannot be undone. It will permanently remove users which may cause discrepancies in your data. Learn more about what happens when you [delete a user profile via API](https://braze.com/docs/help/help_articles/api/delete_user/) in our Help documentation. 
  

### Rate limit

For customers who onboarded with Braze on or after September 16, 2021, we apply a shared rate limit of 20,000 requests per minute to this endpoint. This rate limit is shared with the `/users/alias/new` and `/users/identify` endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameter

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `external_ids` | Optional | Array of strings | External identifiers for the users to delete. |
| `user_aliases` | Optional | Array of user alias object | [User aliases](https://www.braze.com/docs/api/objects_filters/user_alias_object/) for the users to delete. |
| `braze_ids` | Optional | Array of strings | Braze user identifiers for the users to delete. |

**API Endpoint**: `POST /users/delete`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `UsersDeleteCreateBody.builder().brazeIds(List.of("braze_identifier1","braze_identifier2")).externalIds(List.of("external_identifier1","external_identifier2")).userAliases(List.of(UsersDeleteCreateBodyUserAliasesItem.builder().aliasLabel("alias_label1").aliasName("user_alias1").build(),UsersDeleteCreateBodyUserAliasesItem.builder().aliasLabel("alias_label2").aliasName("user_alias2").build())).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.UsersDeleteCreateBody;
import com.yourorg.brazejava.model.UsersDeleteCreateBodyUserAliasesItem;
import com.yourorg.brazejava.resources.users.delete.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.users().delete().create(CreateRequest
                .builder()
                .data(UsersDeleteCreateBody
                      .builder()
                      .brazeIds(List.of(
                                    "braze_identifier1",
                                    "braze_identifier2"
                                ))
                      .externalIds(List.of(
                                       "external_identifier1",
                                       "external_identifier2"
                                   ))
                      .userAliases(List.of(
                                       UsersDeleteCreateBodyUserAliasesItem
                                       .builder()
                                       .aliasLabel("alias_label1")
                                       .aliasName("user_alias1")
                                       .build(),
                                       UsersDeleteCreateBodyUserAliasesItem
                                       .builder()
                                       .aliasLabel("alias_label2")
                                       .aliasName("user_alias2")
                                       .build()
                                   ))
                      .build())
                .build());
```
