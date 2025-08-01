
### Create Email Template <a name="create"></a>

> Use this endpoint to create email templates on the Braze dashboard. 
  

To use this endpoint, you’ll need to generate an API key with the `templates.email.create` permission.

These templates will be available on the **Templates & Media** page. The response from this endpoint will include a field for `email_template_id`, which can be used to update the template in subsequent API calls.

Users’ email subscription status can be updated and retrieved via Braze using a RESTful API. You can use the API to set up bi-directional sync between Braze and other email systems or your own database. All API requests are made over HTTPS.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `template_name` | Required | String | Name of your email template. |
| `subject` | Required | String | Email template subject line. |
| `body` | Required | String | Email template body that may include HTML. |
| `plaintext_body` | Optional | String | A plaintext version of the email template body. |
| `preheader` | Optional | String | Email preheader used to generate previews in some clients. |
| `tags` | Optional | String | [Tags](https://www.braze.com/docs/user_guide/administrative/app_settings/manage_app_group/tags/) must already exist. |
| `should_inline_css` | Optional | Boolean | Enables or disables the `inline_css` feature per template. If not provided, Braze will use the default setting for the app group. One of `true` or `false` is expected. |

### Possible errors

The following table lists possible returned errors and their associated troubleshooting steps, if applicable.

| Error | Troubleshooting |
| --- | --- |
| Template name is required | Enter a template name. |
| Tags must be an array | Tags must be formatted as an array of strings, for example `["marketing", "promotional", "transactional"]`. |
| All tags must be strings | Make sure your tags are encapsulated in quotes (`""`). |
| Some tags could not be found | To add a tag when creating an email template, the tag must already exist in Braze. |
| Email must have valid Content Block names | The email contains Content Blocks that don't exist in this environment. |
| Invalid value for `should_inline_css`. One of `true` or `false` was expected | This parameter only accepts boolean values (true or false). Make sure the value for `should_inline_css` is not encapsulated in quotes (`""`), which causes the value to be sent as a string instead. |

**API Endpoint**: `POST /templates/email/create`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `TemplatesEmailCreateCreateBody.builder().body("This is the text within my email body and https://www.braze.com/ here is a link to Braze.com.").plaintextBody("This is the text within my email body and here is a link to https://www.braze.com/.").preheader("My preheader is pretty cool.").subject("Welcome to my email template!").tags(List.of("Tag1","Tag2")).templateName("email_template_name").build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.TemplatesEmailCreateCreateBody;
import com.yourorg.brazejava.resources.templates.email.create.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.templates().email().create().create(CreateRequest
                .builder()
                .data(TemplatesEmailCreateCreateBody
                      .builder()
                      .body("This is the text within my email body and https://www.braze.com/ here is a link to Braze.com.")
                      .plaintextBody("This is the text within my email body and here is a link to https://www.braze.com/.")
                      .preheader("My preheader is pretty cool.")
                      .subject("Welcome to my email template!")
                      .tags(List.of(
                                "Tag1",
                                "Tag2"
                            ))
                      .templateName("email_template_name")
                      .build())
                .build());
```
