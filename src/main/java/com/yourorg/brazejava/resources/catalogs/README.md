
### Delete Catalog <a name="delete"></a>

> Use this endpoint to delete a catalog. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.delete` permission.

## Rate limit

This endpoint has a shared rate limit of 5 requests per minute between all synchronous catalog endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalog_name` | Required | String | Name of the catalog. |

## Response

There are two status code responses for this endpoint: `200` and `404`.

### Example success response

The status code `200` could return the following response body.

``` json
{
  "message": "success"
}

```

### Example error response

The status code `404` could return the following response body. Refer to [Troubleshooting](https://www.braze.com/docs/api/endpoints/catalogs/catalog_management/synchronous/delete_catalog/#troubleshooting) for more information about errors you may encounter.

``` json
{
  "errors": [
    {
      "id": "catalog-not-found",
      "message": "Could not find catalog",
      "parameters": [
        "catalog_name"
      ],
      "parameter_values": [
        "restaurants"
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

**API Endpoint**: `DELETE /catalogs/{catalog_name}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `catalog_name` | ✓ |  | `"string"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.catalogs.params.DeleteRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().delete(DeleteRequest
                .builder()
                .catalogName("string")
                .build());
```

### List Catalogs <a name="list"></a>

> Use this endpoint to return a list of catalogs in a workspace. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.get` permission.

## Rate limit

This endpoint has a shared rate limit of 5 requests per minute between all synchronous catalog endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Path and request parameters

There are no path or request parameters for this endpoint.

## Example request

```
curl --location --request GET 'https://rest.iad-03.braze.com/catalogs' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY'

```

## Response

### Example success response

The status code `200` could return the following response body.

``` json
{
  "catalogs": [
    {
      "description": "My Restaurants",
      "fields": [
        {
          "name": "id",
          "type": "string"
        },
        {
          "name": "Name",
          "type": "string"
        },
        {
          "name": "City",
          "type": "string"
        },
        {
          "name": "Cuisine",
          "type": "string"
        },
        {
          "name": "Rating",
          "type": "number"
        },
        {
          "name": "Loyalty_Program",
          "type": "boolean"
        },
        {
          "name": "Created_At",
          "type": "time"
        }
      ],
      "name": "restaurants",
      "num_items": 10,
      "updated_at": "2022-11-02T20:04:06.879+00:00"
    },
    {
      "description": "My Catalog",
      "fields": [
        {
          "name": "id",
          "type": "string"
        },
        {
          "name": "string_field",
          "type": "string"
        },
        {
          "name": "number_field",
          "type": "number"
        },
        {
          "name": "boolean_field",
          "type": "boolean"
        },
        {
          "name": "time_field",
          "type": "time"
        },
      ],
      "name": "my_catalog",
      "num_items": 3,
      "updated_at": "2022-11-02T09:03:19.967+00:00"
    },
  ],
  "message": "success"
}

```

**API Endpoint**: `GET /catalogs`

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().list();
```

### Create Catalog <a name="create"></a>

> Use this endpoint to create a catalog. 
  

To use this endpoint, you’ll need to generate an API key with the `catalogs.create` permission.

## Rate limit

This endpoint has a shared rate limit of 5 requests per minute between all synchronous catalog endpoints, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `catalogs` | Required | Array | An array that contains catalog objects. Only one catalog object is allowed for this request. |

### Catalog object parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `name` | Required | String | The name of the catalog that you want to create. |
| `description` | Required | String | The description of the catalog that you want to create. |
| `fields` | Required | Array | An array of objects where the object contains keys `name` and `type`. |

## Example request

```
curl --location --request POST 'https://rest.iad-03.braze.com/catalogs' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-REST-API-KEY' \
--data-raw '{
  "catalogs": [
    {
      "name": "restaurants",
      "description": "My Restaurants",
      "fields": [
        {
          "name": "id",
          "type": "string"
        },
        {
          "name": "Name",
          "type": "string"
        },
        {
          "name": "City",
          "type": "string"
        },
        {
          "name": "Cuisine",
          "type": "string"
        },
        {
          "name": "Rating",
          "type": "number"
        },
        {
          "name": "Loyalty_Program",
          "type": "boolean"
        },
        {
          "name": "Created_At",
          "type": "time"
        }
      ]
    }
  ]
}'

```

## Response

There are two status code responses for this endpoint: `201` and `400`.

### Example success response

The status code `201` could return the following response body.

``` json
{
  "catalogs": [
    {
      "description": "My Restaurants",
      "fields": [
        {
          "name": "id",
          "type": "string"
        },
        {
          "name": "Name",
          "type": "string"
        },
        {
          "name": "City",
          "type": "string"
        },
        {
          "name": "Cuisine",
          "type": "string"
        },
        {
          "name": "Rating",
          "type": "number"
        },
        {
          "name": "Loyalty_Program",
          "type": "boolean"
        },
        {
          "name": "Created_At",
          "type": "time"
        }
      ],
      "name": "restaurants",
      "num_items": 0,
      "updated_at": "2022-11-02T20:04:06.879+00:00"
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
      "id": "catalog-name-already-exists",
      "message": "A catalog with that name already exists",
      "parameters": [
        "name"
      ],
      "parameter_values": [
        "restaurants"
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
| `catalog-array-invalid` | `catalogs` must be an array of objects. |
| `catalog-name-already-exists` | Catalog with that name already exists. |
| `catalog-name-too-large` | Character limit for a catalog name is 250. |
| `description-too-long` | Character limit for description is 250. |
| `field-names-not-unique` | The same field name is referenced twice. |
| `field-names-too-large` | Character limit for a field name is 250. |
| `id-not-first-column` | The `id` must be the first field in the array. Check that the type is a string. |
| `invalid_catalog_name` | Catalog name can only include letters, numbers, hyphens, and underscores. |
| `invalid-field-names` | Fields can only include letters, numbers, hyphens, and underscores. |
| `invalid-field-types` | Make sure the field types are valid. |
| `invalid-fields` | `fields` is not formatted correctly. |
| `reached-company-catalogs-limit` | Maximum number of catalogs reached. Contact your Braze account manager for more information. |
| `too-many-catalog-atoms` | You can only create one catalog per request. |
| `too-many-fields` | Number of fields limit is 30. |

**API Endpoint**: `POST /catalogs`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `CatalogsCreateBody.builder().catalogs(List.of(CatalogsCreateBodyCatalogsItem.builder().description("My Restaurants").fields(List.of(CatalogsCreateBodyCatalogsItemFieldsItem.builder().name("id").type("string").build())).name("restaurants").build())).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.CatalogsCreateBody;
import com.yourorg.brazejava.model.CatalogsCreateBodyCatalogsItem;
import com.yourorg.brazejava.model.CatalogsCreateBodyCatalogsItemFieldsItem;
import com.yourorg.brazejava.resources.catalogs.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.catalogs().create(CreateRequest
                .builder()
                .data(CatalogsCreateBody
                      .builder()
                      .catalogs(List.of(
                                    CatalogsCreateBodyCatalogsItem
                                    .builder()
                                    .description("My Restaurants")
                                    .fields(List.of(
                                            CatalogsCreateBodyCatalogsItemFieldsItem
                                            .builder()
                                            .name("id")
                                            .type("string")
                                            .build()
                                            ))
                                    .name("restaurants")
                                    .build()
                                ))
                      .build())
                .build());
```
