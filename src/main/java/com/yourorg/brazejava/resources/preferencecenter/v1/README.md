
### View Details for Preference Center <a name="get"></a>

> Use this endpoint to view the details for your preference centers, including when it was created and updated. 
  

To use this endpoint, you’ll need to generate an API key with the `preference_center.get` permission.

## Rate limit

This endpoint has a rate limit of 1,000 requests per minute, per workspace.

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `preferenceCenterExternalID` | Required | String | The ID for your preference center. |

## Request parameters

There are no request parameters for this endpoint.

## Example request

```
curl --location -g --request GET https://rest.iad-01.braze.com/preference_center/v1/preference_center_external_id \
--header 'Authorization: Bearer YOUR-REST-API-KEY'

```

## Response

``` json
{
  "name": "My Preference Center",
  "preference_center_api_id": "preference_center_api_id",
  "created_at": "example_time_created",
  "updated_at": "example_time_updated",
  "preference_center_title": "Example preference center title",
  "preference_center_page_html": "HTML for preference center here",
  "confirmation_page_html": "HTML for confirmation page here",
  "redirect_page_html": null,
  "preference_center_options": {
    "meta-viewport-content": "width=device-width, initial-scale=2"
  },
  "state": "active"
}

```

**API Endpoint**: `GET /preference_center/v1/{PreferenceCenterExternalID}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `PreferenceCenterExternalID` | ✓ |  | `"string"` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.resources.preferencecenter.v1.params.GetRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.preferenceCenter().v1().get(GetRequest
                .builder()
                .preferenceCenterExternalId("string")
                .build());
```

### Create Preference Center <a name="create"></a>

> Use this endpoint to create a preference center to allow users to manage their notification preferences for email campaigns. 
  

To use this endpoint, you’ll need to generate an API key with the `preference_center.update` permission.

Check out [Creating a preference center via API](https://www.braze.com/docs/user_guide/message_building_by_channel/email/preference_center/) for details on how to include this in your email campaigns.

## Rate limit

This endpoint has a rate limit of 10 requests per minute, per workspace.

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `name` | Required | String | The name of the preference center that meets the following requirements:  <br>\- Only contains letters, numbers, hyphens, and underscores  <br>\- Does not have spaces |
| `preference_center_title` | Optional | String | The title for the preference center and confirmation pages. If a title is not specified, the title of the pages will default to "Preference Center". |
| `preference_center_page_html` | Required | String | The HTML for the preference center page. |
| `confirmation_page_html` | Required | String | The HTML for the confirmation page. |
| `state` | Optional | String | Choose `active` or `draft`. Defaults to `active` if not specified. |
| `options` | Optional | Object | Attributes: `meta-viewport-content`. When present, a `viewport` meta tag will be added to the page with `content=` . |

> **Note:** The preference center name can't be edited once created. 
  

### Liquid tags

Refer to the following Liquid tags that can be included in your HTML to generate a user's subscription state on the preference center page.

#### User subscription state

| Liquid | Description |
| --- | --- |
| `{{subscribed_state.${email_global}}}` | Get the global email subscribed state for the user (i.e., "opted_in", "subscribed", or "unsubscribed". |
| `{{subscribed_state.${}}}` | Get the subscribed state of the specified subscription group for the user (i.e., "subscribed" or "unsubscribed"). |

#### Form inputs and action

| Liquid | Description |
| --- | --- |
| `{% form_field_name :email_global_state %}` | Indicates that a specific form input element corresponds to the user's global email subscribed state. The user's selection state should be "opted_in", "subscribed", or "unsubscribed" when the form is submitted with selection data for the global email subscribed state. If it's a checkbox, the user will either be "opted_in" or "unsubscribed". For a hidden input, the "subscribed" state will also be valid. |
| `{% form_field_name :subscription_group %}` | Indicates that a specific form input element corresponds to a given subscription group. The user's selection state should be either "subscribed" or "unsubscribed" when the form is submitted with selection data for a specific subscription group. |
| `{{preference_center_submit_url}}` | Generates URL for form submission. |

## Example response

```
{
  "preference_center_api_id": "preference_center_api_id_example",
  "liquid_tag": "{{preference_center.${MyPreferenceCenter2022-09-22}}}",
  "created_at": "2022-09-22T18:28:07+00:00",
  "message": "success"
}

```

**API Endpoint**: `POST /preference_center/v1`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `PreferenceCenterV1CreateBody.builder().confirmationPageHtml("string").name("string").options(PreferenceCenterV1CreateBodyOptions.builder().metaViewportContent("string").build()).preferenceCenterPageHtml("string").preferenceCenterTitle("string").state("active").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.PreferenceCenterV1CreateBody;
import com.yourorg.brazejava.model.PreferenceCenterV1CreateBodyOptions;
import com.yourorg.brazejava.resources.preferencecenter.v1.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.preferenceCenter().v1().create(CreateRequest
                .builder()
                .data(PreferenceCenterV1CreateBody
                      .builder()
                      .confirmationPageHtml("string")
                      .name("string")
                      .options(PreferenceCenterV1CreateBodyOptions
                               .builder()
                               .metaViewportContent("string")
                               .build())
                      .preferenceCenterPageHtml("string")
                      .preferenceCenterTitle("string")
                      .state("active")
                      .build())
                .build());
```

### Update Preference Center <a name="update"></a>

> Use this endpoint to update a preference center. 
  

To use this endpoint, you’ll need to generate an API key with the `preference_center.update` permission.

## Rate limit

This endpoint has a rate limit of 10 requests per minute, per workspace.

## Path parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `preferenceCenterExternalID` | Required | String | The ID for your preference center. |

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `preference_center_page_html` | Required | String | The HTML for the preference center page. |
| `preference_center_title` | Optional | String | The title for the preference center and confirmation pages. If a title is not specified, the title of the pages will default to "Preference Center". |
| `confirmation_page_html` | Required | String | The HTML for the confirmation page. |
| `state` | Optional | String | Choose `active` or `draft`. |
| `options` | Optional | Object | Attributes: `meta-viewport-content`. When present, a `viewport` meta tag will be added to the page with `content=` . |

## Example request

```
curl --location --request POST 'https://rest.iad-01.braze.com/preference_center/v1/{preferenceCenterExternalId}' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE' \
--data-raw '{
  "name": "Example",
  "preference_center_title": "Example Preference Center Title",
  "preference_center_page_html": "HTML for preference center here",
  "confirmation_page_html": "HTML here with a message to users here",
  "state": "active"
}
'

```

## Example response

```
{
  "preference_center_api_id": "8efc52aa-935e-42b7-bd6b-98f43bb9b0f1",
  "created_at": "2022-09-22T18:28:07Z",
  "updated_at": "2022-09-22T18:32:07Z",
  "message": "success"
}

```

**API Endpoint**: `PUT /preference_center/v1/{PreferenceCenterExternalID}`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `PreferenceCenterExternalID` | ✓ |  | `"string"` |
| `data` | ✗ |  | `PreferenceCenterV1UpdateBody.builder().externalSendId("YOUR_BASE64_COMPATIBLE_ID").recipient(List.of(PreferenceCenterV1UpdateBodyRecipientItem.builder().externalUserId("TARGETED_USER_ID_STRING").build())).triggerProperties(PreferenceCenterV1UpdateBodyTriggerProperties.builder().exampleIntegerProperty("YOUR_EXAMPLE_INTEGER").exampleStringProperty("YOUR_EXAMPLE_STRING").build()).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.PreferenceCenterV1UpdateBody;
import com.yourorg.brazejava.model.PreferenceCenterV1UpdateBodyRecipientItem;
import com.yourorg.brazejava.model.PreferenceCenterV1UpdateBodyTriggerProperties;
import com.yourorg.brazejava.resources.preferencecenter.v1.params.UpdateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.preferenceCenter().v1().update(UpdateRequest
                .builder()
                .data(PreferenceCenterV1UpdateBody
                      .builder()
                      .externalSendId("YOUR_BASE64_COMPATIBLE_ID")
                      .recipient(List.of(
                                     PreferenceCenterV1UpdateBodyRecipientItem
                                     .builder()
                                     .externalUserId("TARGETED_USER_ID_STRING")
                                     .build()
                                 ))
                      .triggerProperties(PreferenceCenterV1UpdateBodyTriggerProperties
                              .builder()
                              .exampleIntegerProperty("YOUR_EXAMPLE_INTEGER")
                              .exampleStringProperty("YOUR_EXAMPLE_STRING")
                              .build())
                      .build())
                .preferenceCenterExternalId("string")
                .build());
```
