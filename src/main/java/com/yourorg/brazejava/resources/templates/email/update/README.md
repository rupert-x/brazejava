
### Update Email Template <a name="create"></a>

> Use this endpoint to update email templates on the Braze dashboard. 
  

To use this endpoint, you’ll need to generate an API key with the `templates.email.update` permission.

You can access an email template’s `email_template_id` by navigating to it on the **Templates & Media** page. The [Create email template endpoint](https://www.braze.com/docs/api/endpoints/templates/email_templates/post_create_email_template/) will also return an `email_template_id` reference.

All fields other than the `email_template_id` are optional, but you must specify at least one field to update.

### Rate limit

We apply the default Braze rate limit of 250,000 requests per hour to this endpoint, as documented in [API rate limits](https://www.braze.com/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `email_template_id` | Required | String | Your [email template's API identifier](https://www.braze.com/docs/api/identifier_types/). |
| `template_name` | Optional | String | Name of your email template. |
| `subject` | Optional | String | Email template subject line. |
| `body` | Optional | String | Email template body that may include HTML. |
| `plaintext_body` | Optional | String | A plaintext version of the email template body. |
| `preheader` | Optional | String | Email preheader used to generate previews in some clients. |
| `tags` | Optional | String | [Tags](https://www.braze.com/docs/user_guide/administrative/app_settings/manage_app_group/tags/) must already exist. |
| `should_inline_css` | Optional | Boolean | Enables or disables the `inline_css` feature per template. If not provided, Braze will use the default setting for the AppGroup. One of `true` or `false` is expected. |

### Possible errors

The following table lists possible returned errors and their associated troubleshooting steps, if applicable.

| Error | Troubleshooting |
| --- | --- |
| Template name is required |  |
| Tags must be an array | Tags must be formatted as an array of strings, for example `["marketing", "promotional", "transactional"]`. |
| All tags must be strings | Make sure your tags are encapsulated in quotes (`""`). |
| Some tags could not be found | To add a tag when creating an email template, the tag must already exist in Braze. |
| Invalid value for `should_inline_css`. One of `true` or `false` was expected | This parameter only accepts boolean values (true or false). Make sure the value for `should_inline_css` is not encapsulated in quotes (`""`), which causes the value to be sent as a string instead. |

**API Endpoint**: `POST /templates/email/update`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `TemplatesEmailUpdateCreateBody.builder().body("Check out this week's digital lookbook to inspire your outfits. Take a look at https://www.braze.com/").emailTemplateId("email_template_id").plaintextBody("This is the updated text within my email body and here is a link to https://www.braze.com/.").preheader("We want you to have the best looks this Summer").subject("This Week's Styles").tags(List.of("Tag1","Tag2")).templateName("Weekly Newsletter").build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.TemplatesEmailUpdateCreateBody;
import com.yourorg.brazejava.resources.templates.email.update.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.templates().email().update().create(CreateRequest
                .builder()
                .data(TemplatesEmailUpdateCreateBody
                      .builder()
                      .body("Check out this week's digital lookbook to inspire your outfits. Take a look at https://www.braze.com/")
                      .emailTemplateId("email_template_id")
                      .plaintextBody("This is the updated text within my email body and here is a link to https://www.braze.com/.")
                      .preheader("We want you to have the best looks this Summer")
                      .subject("This Week's Styles")
                      .tags(List.of(
                                "Tag1",
                                "Tag2"
                            ))
                      .templateName("Weekly Newsletter")
                      .build())
                .build());
```
