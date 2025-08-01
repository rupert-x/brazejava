
### Update User's Subscription Group Status - SMS <a name="create"></a>

> Use this endpoint to batch update the subscription state of up to 50 users on the Braze dashboard. 
  

To use this endpoint, you’ll need to generate an API key with the `subscription.status.set` permission.

You can access a subscription group’s `subscription_group_id` by navigating to the **Subscription Group** page.

Tip: When creating new users via the [/users/track](https://www.braze.com/docs/api/endpoints/user_data/post_user_track/) endpoint, you can set subscription groups within the user attributes object, which allows you to create a user and set the subscription group state in one API call.

\*Only `external_id` or `phone` is accepted for SMS subscription groups.

### Rate limit

For customers who onboarded with Braze on or after January 6, 2022, we apply a rate limit of 5,000 requests per minute shared across the `/subscription/status/set` and `/v2/subscription/status/set` endpoint as documented in [API rate limits](http://localhost:4000/docs/api/api_limits/).

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `subscription_group_id` | Required | String | The `id` of your subscription group. |
| `subscription_state` | Required | String | Available values are `unsubscribed` (not in subscription group) or `subscribed` (in subscription group). |
| `external_id` | Required\* | Array of strings | The `external_id` of the user or users, may include up to 50 `id`s. |
| `phone` | Required\* | String in [E.164](https://en.wikipedia.org/wiki/E.164) format | The phone number of the user, can be passed as an array of strings. Must include at least one phone number (with a max of 50). |

### Example successful response

The status code `201` could return the following response body.

``` json
{
    "message": "success"
}

```

Important: The endpoint only accepts the `email` or `phone` value, not both. If given both, you will receive this response: `{"message":"Either an email address or a phone number should be provided, but not both."}`

**API Endpoint**: `POST /subscription/status/set`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `SubscriptionStatusSetCreateBody.builder().externalId("external_identifier").phone(List.of("+12223334444","+11112223333")).subscriptionGroupId("subscription_group_identifier").subscriptionState("unsubscribed").build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.SubscriptionStatusSetCreateBody;
import com.yourorg.brazejava.resources.subscription.status.set.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.subscription().status().set().create(CreateRequest
                .builder()
                .data(SubscriptionStatusSetCreateBody
                      .builder()
                      .externalId("external_identifier")
                      .phone(List.of(
                                 "+12223334444",
                                 "+11112223333"
                             ))
                      .subscriptionGroupId("subscription_group_identifier")
                      .subscriptionState("unsubscribed")
                      .build())
                .build());
```
