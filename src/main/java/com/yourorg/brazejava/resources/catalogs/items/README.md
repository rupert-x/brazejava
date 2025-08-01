
### Delete Multiple Catalog Items <a name="delete"></a>

> Use this endpoint to delete multiple items in your catalog. 

To use this endpoint, you’ll need to generate an API key with the `catalogs.delete_items` permission.

Each request can support up to 50 items. This endpoint is asynchronous.

## Rate limit

This endpoint has a shared rate limit of 100 requests per minute between all asynchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `items` | Required | Array | An array that contains item objects. The item objects should contain an `id` referencing the items Braze should delete. Up to 50 item objects are allowed per request. |

## Example request

```
curl --location --request DELETE 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {"id": "restaurant1"},
    {"id": "restaurant2"},
    {"id": "restaurant3"}
  ]
}'

```

## Response

There are three status code responses for this endpoint: `202`, `400`, and `404`.

### Example success response

The status code `202` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "items-missing-ids",
      "message": "There are 1 item(s) that do not have ids",
      "parameters": [],
      "parameter_values": []
    }
  ],
  "message": "Invalid Request",
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `catalog-not-found` | Check that the catalog name is valid. |
| `ids-too-large` | Item IDs can't be more than 250 characters. |
| `ids-not-unique` | Check that the item IDs are unique in the request. |
| `ids-not-strings` | Item IDs must be of type string. |
| `items-missing-ids` | There are items that do not have item IDs. Check that each item has an item ID. |
| `invalid-ids` | Item IDs can only include letters, numbers, hyphens, and underscores. |
| `request-includes-too-many-items` | Your request has too many items. The item limit per request is 50. |

**API Endpoint**: `DELETE /catalogs/{catalog_name}/items`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.catalogs.items.params.DeleteRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().delete(DeleteRequest
                .builder()
                .catalogName("string")
                .build());
```

### Delete a Catalog Item <a name="delete_1"></a>

> Use this endpoint to delete an item in your catalog. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.delete_item` permission.

## Rate limit

This endpoint has a shared rate limit of 50 requests per minute between all synchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |
| `item_id` | Required | String | The ID of the catalog item. |

## Request parameters

There is no request body for this endpoint.

## Example request

```
curl --location --request DELETE 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'

```

## Response

There are three status code responses for this endpoint: `202`, `400`, and `404`.

### Example success response

The status code `202` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "item-not-found",
      "message": "Could not find item",
      "parameters": [
        "item_id"
      ],
      "parameter_values": [
        "restaurant34"
      ]
    }
  ],
  "message": "Invalid Request"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `arbitrary-error` | An arbitrary error occurred. Please try again or contact [Support](https://www.braze.com/docs/support_contact/). |
| `catalog-not-found` | Check that the catalog name is valid. |
| `item-not-found` | Check that the item to be deleted exists in your catalog. |

**API Endpoint**: `DELETE /catalogs/{catalog_name}/items/{item_id}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |
| `item_id` | ✓ |  | `"string"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.catalogs.items.params.Delete1Request;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().delete1(Delete1Request
                .builder()
                .catalogName("string")
                .itemId("string")
                .build());
```

### List Multiple Catalog Item Details <a name="list"></a>

> Use this endpoint to return multiple catalog items and their content. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.get_items` permission.

## Rate limit

This endpoint has a shared rate limit of 50 requests per minute between all synchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |

## Query parameters

Note that each call to this endpoint will return 50 items. For a catalog with more than 50 items, use the `Link` header to retrieve the data on the next page as shown in the following example response.

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `cursor` | Optional | String | Determines the pagination of the catalog items. |

## Example requests

### Without cursor

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'

```

### With cursor

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs/restaurants/items?cursor=c2tpcDow' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'

```

## Response

There are three status code responses for this endpoint: `200`, `400`, and `404`.

### Example success response

The status code `200` could return the following response header and body.

{% alert note %}  
The `Link` header won't exist if the catalog has less than or equal to 50 items. For calls without a cursor, `prev` will not show. When looking at the last page of items, `next` will not show.  
{% endalert %}

```
Link: ; rel="prev",; rel="next"

```

``` json
{
  "items": [
    {
      "id": "restaurant1",
      "Name": "Restaurant1",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": true,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    },
    {
      "id": "restaurant2",
      "Name": "Restaurant2",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 10,
      "Loyalty_Program": true,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    },
    {
      "id": "restaurant3",
      "Name": "Restaurant3",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": false,
      "Open_Time": "2022-11-02T09:03:19.967Z"
    }
  ],
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "invalid-cursor",
      "message": "'cursor' is not valid",
      "parameters": [
        "cursor"
      ],
      "parameter_values": [
        "bad-cursor"
      ]
    }
  ],
  "message": "Invalid Request"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `catalog-not-found` | Check that the catalog name is valid. |
| `invalid-cursor` | Check that your `cursor` is valid. |

**API Endpoint**: `GET /catalogs/{catalog_name}/items`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.catalogs.items.params.ListRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().list(ListRequest
                .builder()
                .catalogName("string")
                .build());
```

### List Catalog Item Details <a name="get"></a>

> Use this endpoint to return a catalog item and its content. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.get_item` permission.

## Rate limit

This endpoint has a shared rate limit of 50 requests per minute between all synchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |
| `item_id` | Required | String | The ID of the catalog item. |

## Request parameters

There is no request body for this endpoint.

## Example request

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'

```

## Response

There are two status code responses for this endpoint: `200` and `404`.

### Example success response

The status code `200` could return the following response body.

``` json
{
  "items": [
    {
      "id": "restaurant3",
      "Name": "Restaurant1",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": true,
      "Open_Time": "2022-11-01T09:03:19.967Z"
    }
  ],
  "message": "success"
}

```

### Example error response

The status code `404` could return the following response. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "item-not-found",
      "message": "Could not find item",
      "parameters": [
        "item_id"
      ],
      "parameter_values": [
        "restaurant34"
      ]
    }
  ],
  "message": "Invalid Request"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps, if applicable.

| Error | Troubleshooting |
| --- | --- |
| `catalog-not-found` | Check that the catalog name is valid. |
| `item-not-found` | Check that the item is in the catalog. |

**API Endpoint**: `GET /catalogs/{catalog_name}/items/{item_id}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |
| `item_id` | ✓ |  | `"string"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.catalogs.items.params.GetRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().get(GetRequest
                .builder()
                .catalogName("string")
                .itemId("string")
                .build());
```

### Edit Multiple Catalog Items <a name="patch"></a>

> Use this endpoint to delete multiple items in your catalog. 

To use this endpoint, you’ll need to generate an API key with the `catalogs.delete_items` permission.

Each request can support up to 50 items. This endpoint is asynchronous.

## Rate limit

This endpoint has a shared rate limit of 100 requests per minute between all asynchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `items` | Required | Array | An array that contains item objects. The item objects should contain an `id` referencing the items Braze should delete. Up to 50 item objects are allowed per request. |

## Example request

```
curl --location --request DELETE 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {"id": "restaurant1"},
    {"id": "restaurant2"},
    {"id": "restaurant3"}
  ]
}'

```

## Response

There are three status code responses for this endpoint: `202`, `400`, and `404`.

### Example success response

The status code `202` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "items-missing-ids",
      "message": "There are 1 item(s) that do not have ids",
      "parameters": [],
      "parameter_values": []
    }
  ],
  "message": "Invalid Request",
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `catalog-not-found` | Check that the catalog name is valid. |
| `ids-too-large` | Item IDs can't be more than 250 characters. |
| `ids-not-unique` | Check that the item IDs are unique in the request. |
| `ids-not-strings` | Item IDs must be of type string. |
| `items-missing-ids` | There are items that do not have item IDs. Check that each item has an item ID. |
| `invalid-ids` | Item IDs can only include letters, numbers, hyphens, and underscores. |
| `request-includes-too-many-items` | Your request has too many items. The item limit per request is 50. |

**API Endpoint**: `PATCH /catalogs/{catalog_name}/items`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |
| `data` | ✗ |  | `CatalogsItemsPatchBody.builder().items(List.of(CatalogsItemsPatchBodyItemsItem.builder().id("restaurant1").build())).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CatalogsItemsPatchBody;
import com.yourorg.brazejava.model.CatalogsItemsPatchBodyItemsItem;
import com.yourorg.brazejava.resources.catalogs.items.params.PatchRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().patch(PatchRequest
                .builder()
                .data(CatalogsItemsPatchBody
                      .builder()
                      .items(List.of(
                                 CatalogsItemsPatchBodyItemsItem
                                 .builder()
                                 .id("restaurant1")
                                 .build()
                             ))
                      .build())
                .catalogName("string")
                .build());
```

### Edit Catalog Items <a name="patch_1"></a>

> Use this endpoint to edit an item in your catalog. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.update_item` permission.

## Rate Limit

This endpoint has a shared rate limit of 50 requests per minute between all synchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |
| `item_id` | Required | String | The ID of the catalog item. |

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `items` | Required | Array | An array that contains item objects. The item objects should contain fields that exist in the catalog except for the `id` field. Only one item object is allowed per request. |

## Example request

```
curl --location --request PATCH 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {
      "Name": "Restaurant",
      "Loyalty_Program": false,
      "Open_Time": "2021-09-03T09:03:19.967+00:00"
    }
  ]
}'

```

## Response

There are three status code responses for this endpoint: `200`, `400`, and `404`.

### Example success response

The status code `200` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "invalid-fields",
      "message": "Some of the fields given do not exist in the catalog",
      "parameters": [
        "id"
      ],
      "parameter_values": [
        "restaurant1"
      ]
    }
  ],
  "message": "Invalid Request"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `arbitrary-error` | An arbitrary error occurred. Please try again or contact [Support](https://www.braze.com/docs/support_contact/). |
| `catalog-not-found` | Check that the catalog name is valid. |
| `filtered-set-field-too-long` | The field value is being used in a filtered set that exceeds the character limit for an item. |
| `id-in-body` | An item ID already exists in the catalog. |
| `ids-too-large` | Character limit for each item ID is 250 characters. |
| `invalid-ids` | Supported characters for item ID names are letters, numbers, hyphens, and underscores. |
| `invalid-fields` | Confirm that the fields in the request exist in the catalog. |
| `invalid-keys-in-value-object` | Item object keys can't include `.` or `$`. |
| `item-not-found` | Check that the item is in the catalog. |
| `item-array-invalid` | `items` must be an array of objects. |
| `items-too-large` | Character limit for each item is 5,000 characters. |
| `request-includes-too-many-items` | You can only edit one catalog item per request. |
| `too-deep-nesting-in-value-object` | Item objects can't have more than 50 levels of nesting. |
| `unable-to-coerce-value` | Item types can't be converted. |

**API Endpoint**: `PATCH /catalogs/{catalog_name}/items/{item_id}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |
| `item_id` | ✓ |  | `"string"` |
| `data` | ✗ |  | `CatalogsItemsPatch1Body.builder().items(List.of(Map.ofEntries(Map.entry("Loyalty_Program", false),Map.entry("Name", "Restaurant"),Map.entry("Open_Time", "2021-09-03T09:03:19.967+00:00")))).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CatalogsItemsPatch1Body;
import com.yourorg.brazejava.resources.catalogs.items.params.Patch1Request;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().patch1(Patch1Request
                .builder()
                .data(CatalogsItemsPatch1Body
                      .builder()
                      .items(List.of(
                                 Map.ofEntries(
                                     Map.entry("Loyalty_Program", false),
                                     Map.entry("Name", "Restaurant"),
                                     Map.entry("Open_Time", "2021-09-03T09:03:19.967+00:00")
                                 )
                             ))
                      .build())
                .catalogName("string")
                .itemId("string")
                .build());
```

### Create Multiple Catalog Items <a name="create"></a>

> Use this endpoint to create multiple items in your catalog. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.add_items` permission.

Each request can support up to 50 items. This endpoint is asynchronous.

## Rate limit

This endpoint has a shared rate limit of 100 requests per minute between all asynchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `items` | Required | Array | An array that contains item objects. The item objects should contain all of the fields in the catalog. Up to 50 item objects are allowed per request. |

## Example request

```
curl --location --request POST 'https://rest.iad-03.braze.com/catalogs/restaurants/items' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {
      "id": "restaurant1",
      "Name": "Restaurant1",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": true,
      "Created_At": "2022-11-01T09:03:19.967+00:00"
    },
    {
      "id": "restaurant2",
      "Name": "Restaurant2",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 10,
      "Loyalty_Program": true,
      "Created_At": "2022-11-02T09:03:19.967+00:00"
    },
    {
      "id": "restaurant3",
      "Name": "Restaurant3",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 3,
      "Loyalty_Program": false,
      "Created_At": "2022-11-03T09:03:19.967+00:00"
    }
  ]
}'

```

## Response

There are three status code responses for this endpoint: `202`, `400`, and `404`.

### Example success response

The status code `202` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "fields-do-not-match",
      "message": "Fields do not match with fields on the catalog",
      "parameters": [
        "id"
      ],
      "parameter_values": [
        "restaurant2"
      ]
    }
  ],
  "message": "Invalid Request"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `catalog-not-found` | Check that the catalog name is valid. |
| `ids-not-strings` | Item IDs must be of type string. |
| `ids-not-unique` | Item IDs must be unique in the request. |
| `ids-too-large` | Item IDs can't be more than 250 characters. |
| `invalid-ids` | Item IDs can only include letters, numbers, hyphens, and underscores. |
| `invalid-fields` | Confirm that the fields in the request exist in the catalog. |
| `invalid-keys-in-value-object` | Item object keys can't include `.` or `$`. |
| `item-array-invalid` | `items` must be an array of objects. |
| `items-missing-ids` | There are items that do not have item IDs. Check that each item has an item ID. |
| `items-too-large` | Item values can't exceed 5,000 characters. |
| `request-includes-too-many-items` | Your request has too many items. The item limit per request is 50. |
| `too-deep-nesting-in-value-object` | Item objects can't have more than 50 levels of nesting. |
| `unable-to-coerce-value` | Item types can't be converted. |

**API Endpoint**: `POST /catalogs/{catalog_name}/items`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |
| `data` | ✗ |  | `CatalogsItemsCreateBody.builder().items(List.of(Map.ofEntries(Map.entry("City", "New York"),Map.entry("Created_At", "2022-11-01T09:03:19.967+00:00"),Map.entry("Cuisine", "American"),Map.entry("Loyalty_Program", true),Map.entry("Name", "Restaurant1"),Map.entry("Rating", 5),Map.entry("id", "restaurant1")))).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CatalogsItemsCreateBody;
import com.yourorg.brazejava.resources.catalogs.items.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().create(CreateRequest
                .builder()
                .data(CatalogsItemsCreateBody
                      .builder()
                      .items(List.of(
                                 Map.ofEntries(
                                     Map.entry("City", "New York"),
                                     Map.entry("Created_At", "2022-11-01T09:03:19.967+00:00"),
                                     Map.entry("Cuisine", "American"),
                                     Map.entry("Loyalty_Program", true),
                                     Map.entry("Name", "Restaurant1"),
                                     Map.entry("Rating", 5),
                                     Map.entry("id", "restaurant1")
                                 )
                             ))
                      .build())
                .catalogName("string")
                .build());
```

### Create Catalog Item <a name="create_1"></a>

> Use this endpoint to create an item in your catalog. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.create_item` permission.

## Rate limit

This endpoint has a shared rate limit of 50 requests per minute between all synchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |
| `item_id` | Required | String | The ID of the catalog item. |

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `items` | Required | Array | An array that contains item objects. The item objects should contain all of the fields in the catalog except for the `id` field. Only one item object is allowed per request. |

## Example Request

```
curl --location --request POST 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {
      "Name": "Restaurant1",
      "City": "New York",
      "Cuisine": "American",
      "Rating": 5,
      "Loyalty_Program": true,
      "Created_At": "2022-11-01T09:03:19.967+00:00"
    }
  ]
}'

```

## Response

There are three status code responses for this endpoint: `201`, `400`, and `404`.

### Example success response

The status code `201` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "fields-do-not-match",
      "message": "Fields do not match with fields on the catalog",
      "parameters": [
        "id"
      ],
      "parameter_values": [
        "restaurant2"
      ]
    }
  ],
  "message": "Invalid Request"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `already-reached-catalog-item-limit` | Maximum number of catalogs reached. Contact your Braze account manager for more information. |
| `already-reached-company-item-limit` | Maximum number of catalog items reached. Contact your Braze account manager for more information. |
| `arbitrary-error` | An arbitrary error occurred. Please try again or contact [Support](https://www.braze.com/docs/support_contact/). |
| `catalog-not-found` | Check that the catalog name is valid. |
| `filtered-set-field-too-long` | The field value is being used in a filtered set that exceeds the character limit for an item. |
| `id-in-body` | Remove any item IDs in the request body. |
| `ids-too-large` | Character limit for each item ID is 250 characters. |
| `invalid-ids` | Supported characters for item ID names are letters, numbers, hyphens, and underscores. |
| `invalid-fields` | Confirm that the fields in the request exist in the catalog. |
| `invalid-keys-in-value-object` | Item object keys can't include `.` or `$`. |
| `item-already-exists` | The item already exists in the catalog. |
| `item-array-invalid` | `items` must be an array of objects. |
| `items-too-large` | Character limit for each item is 5,000 characters. |
| `request-includes-too-many-items` | You can only create one catalog item per request. |
| `too-deep-nesting-in-value-object` | Item objects can't have more than 50 levels of nesting. |
| `unable-to-coerce-value` | Item types can't be converted. |

**API Endpoint**: `POST /catalogs/{catalog_name}/items/{item_id}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |
| `item_id` | ✓ |  | `"string"` |
| `data` | ✗ |  | `CatalogsItemsCreate1Body.builder().items(List.of(Map.ofEntries(Map.entry("City", "New York"),Map.entry("Created_At", "2022-11-01T09:03:19.967+00:00"),Map.entry("Cuisine", "American"),Map.entry("Loyalty_Program", true),Map.entry("Name", "Restaurant1"),Map.entry("Rating", 5)))).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CatalogsItemsCreate1Body;
import com.yourorg.brazejava.resources.catalogs.items.params.Create1Request;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().create1(Create1Request
                .builder()
                .data(CatalogsItemsCreate1Body
                      .builder()
                      .items(List.of(
                                 Map.ofEntries(
                                     Map.entry("City", "New York"),
                                     Map.entry("Created_At", "2022-11-01T09:03:19.967+00:00"),
                                     Map.entry("Cuisine", "American"),
                                     Map.entry("Loyalty_Program", true),
                                     Map.entry("Name", "Restaurant1"),
                                     Map.entry("Rating", 5)
                                 )
                             ))
                      .build())
                .catalogName("string")
                .itemId("string")
                .build());
```

### Update Catalog Item <a name="update"></a>

> Use this endpoint to send Canvas messages via API-triggered delivery. 
  

To use this endpoint, you'll need to generate an API key with the `catalogs.replace_item` permission.

API-triggered Delivery allows you to store message content in the Braze dashboard while dictating when a message is sent, and to whom via your API.

Note that to send messages with this endpoint, you must have a [Canvas ID](https://www.braze.com/docs/api/identifier_types/#canvas-api-identifier), created when you build a Canvas.

## Rate limit

This endpoint has a shared rate limit of 50 requests per minute between all synchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |
| `item_id` | Required | String | The ID of the catalog item. |

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `items` | Required | Array | An array that contains item objects. The item objects should contain fields that exist in the catalog except for the `id` field. Only one item object is allowed per request. |

## Example request

## Response

There are three status code responses for this endpoint: `200`, `400`, and `404`.

### Example success response

The status code `200` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "invalid-fields",
      "message": "Some of the fields given do not exist in the catalog",
      "parameters": [
        "id"
      ],
      "parameter_values": [
        "restaurant1"
      ]
    }
  ],
  "message": "Invalid Request"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `catalog_not_found` | Check that the catalog name is valid. | 
| `ids_not_string` | Confirm that each item ID is a string. |
| `ids_not_unique` | Check that each item ID is unique. |
| `ids_too_large` | Character limit for each item ID is 250 characters. |
| `item_array_invalid` | `items` must be an array of objects. |
| `items_missing_ids` | Confirm that each item has an ID. |
| `items_too_large` | Item values can't exceed 5,000 characters. |
| `invalid_ids` | Supported characters for item ID names are letters, numbers, hyphens, and underscores. |
| `invalid_fields` | Confirm that the fields in the request exist in the catalog. |
| `invalid_keys_in_value_object` | Item object keys can't include `.` or `$`. |
| `too_deep_nesting_in_value_object` | Item objects can't have more than 50 levels of nesting. 
| `request_includes_too_many_items` | Your request has too many items. The item limit per request is 50. |
| `unable_to_coerce_value` | Item types can't be converted. |

**API Endpoint**: `PUT /catalogs/{catalog_name}/items`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |
| `data` | ✗ |  | `CatalogsItemsUpdateBody.builder().items(List.of(Map.ofEntries(Map.entry("Location", Map.ofEntries(Map.entry("Latitude", 33.6112),Map.entry("Longitude", -117.8711))),Map.entry("Loyalty_Program", false),Map.entry("Name", "Restaurant"),Map.entry("Open_Time", "2021-09-03T09:03:19.967+00:00")))).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CatalogsItemsUpdateBody;
import com.yourorg.brazejava.resources.catalogs.items.params.UpdateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().update(UpdateRequest
                .builder()
                .data(CatalogsItemsUpdateBody
                      .builder()
                      .items(List.of(
                                 Map.ofEntries(
                                     Map.entry("Location", Map.ofEntries(
                                             Map.entry("Latitude", 33.6112),
                                             Map.entry("Longitude", -117.8711)
                                             )),
                                     Map.entry("Loyalty_Program", false),
                                     Map.entry("Name", "Restaurant"),
                                     Map.entry("Open_Time", "2021-09-03T09:03:19.967+00:00")
                                 )
                             ))
                      .build())
                .catalogName("string")
                .build());
```

### Update Catalog Item <a name="update_1"></a>

> Use this endpoint to update an item in your catalog. 
  

To use this endpoint, you'll need to generate an API key with the `catalogs.replace_item` permission.

If the `item_id` isn't found, this endpoint will create the item. This endpoint is synchronous.

## Rate limit

This endpoint has a shared rate limit of 50 requests per minute between all synchronous catalog item endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |
| `item_id` | Required | String | The ID of the catalog item. |

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `items` | Required | Array | An array that contains item objects. The item objects should contain fields that exist in the catalog except for the `id` field. Only one item object is allowed per request. |

## Example request

```
curl --location --request PUT 'https://rest.iad-03.braze.com/catalogs/restaurants/items/restaurant1' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "items": [
    {
      "Name": "Restaurant",
      "Loyalty_Program": false,
      "Location": {
        "Latitude": 33.6112,
        "Longitude": -117.8711
      },
      "Open_Time": "2021-09-03T09:03:19.967+00:00"
    }
  ]
}'

```

## Response

There are three status code responses for this endpoint: `200`, `400`, and `404`.

### Example success response

The status code `200` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `400` could return the following response body. Refer to [Troubleshooting](#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "invalid-fields",
      "message": "Some of the fields given do not exist in the catalog",
      "parameters": [
        "id"
      ],
      "parameter_values": [
        "restaurant1"
      ]
    }
  ],
  "message": "Invalid Request"
}

```

## Troubleshooting

The following table lists possible returned errors and their associated troubleshooting steps.

| Error | Troubleshooting |
| --- | --- |
| `already_reached_catalog_item_limit` | Maximum number of catalogs reached. Contact your Braze account manager for more information. |
| `already_reached_company_item_limit` | Maximum number of items reached. Contact your Braze account manager for more information. |
| `arbitrary_error` | An arbitrary error occurred. Please try again or contact [Support](https://www.braze.com/docs/support_contact/). |
| `catalog_not_found` | Check that the catalog name is valid. |
| `filtered-set-field-too-long` | The field value is being used in a filtered set that exceeds the character limit for an item. |
| `id_in_body` | Remove any item IDs in the request body. |
| `ids_too_large` | Character limit for each item ID is 250 characters. |
| `invalid_ids` | Supported characters for item ID names are letters, numbers, hyphens, and underscores. |
| `invalid_fields` | Confirm that the fields in the request exist in the catalog. |
| `invalid_keys_in_value_object` | Item object keys can't include `.` or `$`. |
| `item_already_exists` | The item already exists in the catalog. |
| `item_array_invalid` | `items` must be an array of objects. |
| `items_too_large` | Item values can't exceed 5,000 characters. |
| `request_includes_too_many_items` | Your request has too many items. The item limit per request is 50. |
| `too_deep_nesting_in_value_object` | Item objects can't have more than 50 levels of nesting. |
| `unable_to_coerce_value` | Item types can't be converted. |

**API Endpoint**: `PUT /catalogs/{catalog_name}/items/{item_id}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |
| `item_id` | ✓ |  | `"string"` |
| `data` | ✗ |  | `CatalogsItemsUpdate1Body.builder().items(List.of(Map.ofEntries(Map.entry("Location", Map.ofEntries(Map.entry("Latitude", 33.6112),Map.entry("Longitude", -117.8711))),Map.entry("Loyalty_Program", false),Map.entry("Name", "Restaurant"),Map.entry("Open_Time", "2021-09-03T09:03:19.967+00:00")))).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CatalogsItemsUpdate1Body;
import com.yourorg.brazejava.resources.catalogs.items.params.Update1Request;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().items().update1(Update1Request
                .builder()
                .data(CatalogsItemsUpdate1Body
                      .builder()
                      .items(List.of(
                                 Map.ofEntries(
                                     Map.entry("Location", Map.ofEntries(
                                             Map.entry("Latitude", 33.6112),
                                             Map.entry("Longitude", -117.8711)
                                             )),
                                     Map.entry("Loyalty_Program", false),
                                     Map.entry("Name", "Restaurant"),
                                     Map.entry("Open_Time", "2021-09-03T09:03:19.967+00:00")
                                 )
                             ))
                      .build())
                .catalogName("string")
                .itemId("string")
                .build());
```
