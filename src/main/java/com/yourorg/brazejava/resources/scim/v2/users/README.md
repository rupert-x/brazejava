
### Remove Dashboard User Account <a name="delete"></a>

> This endpoint allows you to permanently delete an existing dashboard user by specifying the resource `id` returned by the SCIM [`POST`](https://www.braze.com/docs/scim/post_create_user_account/) method.  
 
  

This is similar to deleting a user in the **Manage Users** section of the Braze dashboard. For information on how to obtain a SCIM token, visit [Automated user provisioning](https://www.braze.com/docs/scim/automated_user_provisioning/).

## Rate limit

This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, and POST endpoints as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data type | Description |
| --- | --- | --- | --- |
| `id` | Required | String | The user’s resource ID. This parameter is returned by the `POST` `/scim/v2/Users/` or `GET` `/scim/v2/Users?filter=userName eq "[user@test.com](mailto:user@test.com)"` methods. |

## Request parameters

There is no request body for this endpoint.

## Response

### Example error response

``` json
HTTP/1.1 204 Not Found
Content-Type: text/html; charset=UTF-8

```

If a developer with this ID doesn’t exist in Braze, the endpoint will respond with:

``` json
HTTP/1.1 404 Not Found Content-Type: text/html; charset=UTF-8
{ "schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"], "detail": "User not found", "status": 404 }

```

**API Endpoint**: `DELETE /scim/v2/Users/{id}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `id` | ✓ |  | `"string"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.scim.v2.users.params.DeleteRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.scim().v2().users().delete(DeleteRequest
                .builder()
                .id("string")
                .build());
```

### Search Existing Dashboard User by Email <a name="list"></a>

> This endpoint allows you to look up an existing dashboard user account by specifying their email in the filter query parameter.  
 
  

Note that when the query parameter is URL encoded it will read like this:

`/scim/v2/Users?filter=userName eq "user@test.com"`

For information on how to obtain a SCIM token, visit [Automated user provisioning](https://www.braze.com/docs/scim/automated_user_provisioning/).

## Rate limit

This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, DELETE, and POST endpoints as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `userName@example.com` | Required | String | The user's email. |

## Request parameters

There is no request body for this endpoint.

## Response

``` json
Content-Type: application/json
X-Request-Origin: YOUR-REQUEST-ORIGIN-HERE
Authorization: Bearer YOUR-SCIM-TOKEN-HERE
{
    "schemas": ["urn:ietf:params:scim:api:messages:2.0:ListResponse"],
    "totalResults": 1,
    "Resources": [
        {
            "userName": "user@test.com",
            "id": "dfa245b7-24195aec-887bb3ad-602b3340",
            "name": {
                "givenName": "Test",
                "familyName": "User"
            },
            "department": "finance",
            "lastSignInAt": "Thursday, January 1, 1970 12:00:00 AM",
            "permissions": {
                "companyPermissions": ["manage_company_settings"],
                "appGroup": [
                    {
                        "appGroupId": "241adcd25789fabcded",
                        "appGroupName": "Test App Group",
                        "appGroupPermissions": ["basic_access","send_campaigns_canvases"],
                        "team": [
                            {
                                "teamId": "241adcd25789fabcded",
                                "teamName": "Test Team",                  
                                "teamPermissions": ["admin"]
                            }
                        ]
                    } 
                ]
            }
        }
    ]
}

```

**API Endpoint**: `GET /scim/v2/Users`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `filter` | ✗ |  | `"{userName@example.com}"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.scim.v2.users.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.scim().v2().users().list(ListRequest
                .builder()
                .filter("{userName@example.com}")
                .build());
```

### Look Up an Existing Dashboard User Account <a name="get"></a>

> This endpoint allows you to look up an existing dashboard user account by specifying the resource `id` returned by the SCIM [`POST`](https://www.braze.com/docs/scim/post_create_user_account/) method.  
 
  

For information on how to obtain a SCIM token, visit [Automated user provisioning](https://www.braze.com/docs/scim/automated_user_provisioning/).

## Rate limit

This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, DELETE, and POST endpoints as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `id` | Required | String | The user's resource ID. This parameter is returned by the `POST` `/scim/v2/Users/` or `GET` `/scim/v2/Users?filter=userName eq "user@test.com"` methods. |

## Request parameters

There is no request body for this endpoint.

## Response

``` json
{
    "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
    "id": "dfa245b7-24195aec-887bb3ad-602b3340",
    "userName": "user@test.com",
    "name": {
        "givenName": "Test",
        "familyName": "User"
    },
    "department": "finance",
    "lastSignInAt": "Thursday, January 1, 1970 12:00:00 AM",
    "permissions": {
        "companyPermissions": ["manage_company_settings"],
        "appGroup": [
            {
                "appGroupId": "241adcd25789fabcded",
                "appGroupName": "Test App Group",
                "appGroupPermissions": ["basic_access","send_campaigns_canvases"],
                "team": [
                    {
                         "teamId": "241adcd25789fabcded",
                         "teamName": "Test Team",                  
                         "teamPermissions": ["admin"]
                    }
                ]
            } 
        ]
    }
}

```

**API Endpoint**: `GET /scim/v2/Users/{id}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `id` | ✓ |  | `"string"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.scim.v2.users.params.GetRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.scim().v2().users().get(GetRequest
                .builder()
                .id("string")
                .build());
```

### Create New Dashboard User Account <a name="create"></a>

> This endpoint allows you to create a new dashboard user account by specifying email, given and family names, permissions (for setting permissions at the company, app group, and team level).  
 
  

For information on how to obtain a SCIM token, visit [Automated user provisioning](https://www.braze.com/docs/scim/automated_user_provisioning/).

## Rate limit

This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` PUT, GET, and DELETE endpoints as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data type | Description |
| --- | --- | --- | --- |
| `schemas` | Required | Array of strings | Expected SCIM 2.0 schema name for user object. |
| `userName` | Required | String | The user’s email address. |
| `name` | Required | JSON object | This object contains the user's given name and family name. |
| `department` | Required | String | Valid department string from the [department string documentation]({{site.baseurl}}/scim_api_appendix/#department-strings). |
| `permissions` | Required | JSON object | Permissions object as described in the [permissions object documentation]({{site.baseurl}}/scim_api_appendix/#permissions-object). |

## Response

``` json
{
    "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
    "id": "dfa245b7-24195aec-887bb3ad-602b3340",
    "userName": "user@test.com",
    "name": {
        "givenName": "Test",
        "familyName": "User"
    },
    "department": "finance",
    "lastSignInAt": "Thursday, January 1, 1970 12:00:00 AM",
    "permissions": {
        "companyPermissions": ["manage_company_settings"],
        "appGroup": [
            {
                "appGroupId": "241adcd25789fabcded",
                "appGroupName": "Test App Group",
                "appGroupPermissions": ["basic_access","send_campaigns_canvases"],
                "team": [
                    {
                         "teamId": "2519dafcdba238ae7",
                         "teamName": "Test Team",                  
                         "teamPermissions": ["basic_access","export_user_data"]
                    }
                ]
            } 
        ]
    }
}

```

### Error states

If a user with this email address already exists in Braze, the endpoint will respond with:

``` json
HTTP/1.1 409 Conflict
Date: Tue, 10 Sep 2019 02:22:30 GMT
Content-Type: text/json;charset=UTF-8
{
  "schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],
  "detail": "User already exists in the database.",
  "status": 409
}

```

**API Endpoint**: `POST /scim/v2/Users`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `ScimV2UsersCreateBody.builder().department("finance").name(ScimV2UsersCreateBodyName.builder().familyName("User").givenName("Test").build()).permissions(ScimV2UsersCreateBodyPermissions.builder().appGroup(List.of(ScimV2UsersCreateBodyPermissionsAppGroupItem.builder().appGroupName("Test App Group").appGroupPermissions(List.of("basic_access","send_campaigns_canvases")).team(List.of(ScimV2UsersCreateBodyPermissionsAppGroupItemTeamItem.builder().teamName("Test Team").teamPermissions(List.of("basic_access","export_user_data")).build())).build())).companyPermissions(List.of("manage_company_settings")).build()).schemas(List.of("urn:ietf:params:scim:schemas:core:2.0:User")).userName("user@test.com").build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.ScimV2UsersCreateBody;
import com.yourorg.brazejava.model.ScimV2UsersCreateBodyName;
import com.yourorg.brazejava.model.ScimV2UsersCreateBodyPermissions;
import com.yourorg.brazejava.model.ScimV2UsersCreateBodyPermissionsAppGroupItem;
import com.yourorg.brazejava.model.ScimV2UsersCreateBodyPermissionsAppGroupItemTeamItem;
import com.yourorg.brazejava.resources.scim.v2.users.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.scim().v2().users().create(CreateRequest
                .builder()
                .data(ScimV2UsersCreateBody
                      .builder()
                      .department("finance")
                      .name(ScimV2UsersCreateBodyName
                            .builder()
                            .familyName("User")
                            .givenName("Test")
                            .build())
                      .permissions(ScimV2UsersCreateBodyPermissions
                                   .builder()
                                   .appGroup(List.of(
                                           ScimV2UsersCreateBodyPermissionsAppGroupItem
                                           .builder()
                                           .appGroupName("Test App Group")
                                           .appGroupPermissions(List.of(
                                                   "basic_access",
                                                   "send_campaigns_canvases"
                                                   ))
                                           .team(List.of(
                                                   ScimV2UsersCreateBodyPermissionsAppGroupItemTeamItem
                                                   .builder()
                                                   .teamName("Test Team")
                                                   .teamPermissions(List.of(
                                                           "basic_access",
                                                           "export_user_data"
                                                           ))
                                                   .build()
                                                   ))
                                           .build()
                                           ))
                                   .companyPermissions(List.of(
                                           "manage_company_settings"
                                           ))
                                   .build())
                      .schemas(List.of(
                                   "urn:ietf:params:scim:schemas:core:2.0:User"
                               ))
                      .userName("user@test.com")
                      .build())
                .build());
```

### Update Dashboard User Account <a name="update"></a>

> This endpoint allows you to update an existing dashboard user account by specifying the resource `id` returned by the SCIM [`POST`](https://www.braze.com/docs/scim/post_create_user_account/) method.  
 
  

It allows you to update of given and family names, permissions (for setting permissions at the company, app group, and team level) and department. For information on how to obtain a SCIM token, visit [Automated user provisioning](https://www.braze.com/docs/scim/automated_user_provisioning/).

For security reasons, `userName` (email address) cannot be updated through this endpoint. If you would like to change the `userName` (email address) for a user, contact [Support](https://www.braze.com/docs/support_contact/).

## Rate limit

This endpoint has a rate limit of 5000 requests per day, per company. This rate limit is shared with the `/scim/v2/Users/` GET, DELETE, and POST endpoints as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `id` | Required | String | The user's resource ID. This parameter is returned by the `POST` `/scim/v2/Users/` or `GET` `/scim/v2/Users?filter=userName eq "user@test.com"` methods. |

## Request parameters

| Parameter | Required | Data type | Description |
| --- | --- | --- | --- |
| `schemas` | Required | Array of strings | Expected SCIM 2.0 schema name for user object. |
| `name` | Required | JSON object | This object contains the user's given name and family name. |
| `department` | Required | String | Valid department string from the [department string documentation]({{site.baseurl}}/scim_api_appendix/#department-strings). |
| `permissions` | Required | JSON object | Permissions object as described in the [permissions object documentation]({{site.baseurl}}/scim_api_appendix/#permissions-object). |

## Response

``` json
{
    "schemas": ["urn:ietf:params:scim:schemas:core:2.0:User"],
    "id": "dfa245b7-24195aec-887bb3ad-602b3340",
    "userName": "user@test.com",
    "name": {
        "givenName": "Test",
        "familyName": "User"
    },
    "department": "finance",
    "lastSignInAt": "Thursday, January 1, 1970 12:00:00 AM",
    "permissions": {
        "companyPermissions": ["manage_company_settings"],
        "appGroup": [
            {
                "appGroupId": "241adcd25789fabcded",
                "appGroupName": "Test App Group",
                "appGroupPermissions": ["basic_access","send_campaigns_canvases"],
                "team": [
                    {
                         "teamId": "2519dafcdba238ae7",
                         "teamName": "Test Team",                  
                         "teamPermissions": ["admin"]
                    }
                ]
            } 
        ]
    }
}

```

### Error states

If a user with this ID doesn’t exist in Braze, the endpoint will respond with:

``` json
HTTP/1.1 404 Not Found
Content-Type: text/html; charset=UTF-8
{
    "schemas": ["urn:ietf:params:scim:api:messages:2.0:Error"],
    "detail": "User not found",
    "status": 404
}

```

**API Endpoint**: `PUT /scim/v2/Users/{id}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `id` | ✓ |  | `"string"` |
| `data` | ✗ |  | `ScimV2UsersUpdateBody.builder().department("finance").name(ScimV2UsersUpdateBodyName.builder().familyName("User").givenName("Test").build()).permissions(ScimV2UsersUpdateBodyPermissions.builder().appGroup(List.of(ScimV2UsersUpdateBodyPermissionsAppGroupItem.builder().appGroupName("Test App Group").appGroupPermissions(List.of("basic_access","send_campaigns_canvases")).team(List.of(ScimV2UsersUpdateBodyPermissionsAppGroupItemTeamItem.builder().teamName("Test Team").teamPermissions(List.of("admin")).build())).build())).companyPermissions(List.of("manage_company_settings")).build()).schemas(List.of("urn:ietf:params:scim:schemas:core:2.0:User")).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.ScimV2UsersUpdateBody;
import com.yourorg.brazejava.model.ScimV2UsersUpdateBodyName;
import com.yourorg.brazejava.model.ScimV2UsersUpdateBodyPermissions;
import com.yourorg.brazejava.model.ScimV2UsersUpdateBodyPermissionsAppGroupItem;
import com.yourorg.brazejava.model.ScimV2UsersUpdateBodyPermissionsAppGroupItemTeamItem;
import com.yourorg.brazejava.resources.scim.v2.users.params.UpdateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.scim().v2().users().update(UpdateRequest
                .builder()
                .data(ScimV2UsersUpdateBody
                      .builder()
                      .department("finance")
                      .name(ScimV2UsersUpdateBodyName
                            .builder()
                            .familyName("User")
                            .givenName("Test")
                            .build())
                      .permissions(ScimV2UsersUpdateBodyPermissions
                                   .builder()
                                   .appGroup(List.of(
                                           ScimV2UsersUpdateBodyPermissionsAppGroupItem
                                           .builder()
                                           .appGroupName("Test App Group")
                                           .appGroupPermissions(List.of(
                                                   "basic_access",
                                                   "send_campaigns_canvases"
                                                   ))
                                           .team(List.of(
                                                   ScimV2UsersUpdateBodyPermissionsAppGroupItemTeamItem
                                                   .builder()
                                                   .teamName("Test Team")
                                                   .teamPermissions(List.of(
                                                           "admin"
                                                           ))
                                                   .build()
                                                   ))
                                           .build()
                                           ))
                                   .companyPermissions(List.of(
                                           "manage_company_settings"
                                           ))
                                   .build())
                      .schemas(List.of(
                                   "urn:ietf:params:scim:schemas:core:2.0:User"
                               ))
                      .build())
                .id("string")
                .build());
```
