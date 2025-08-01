
### Update User's Subscription Group Status V2 <a name="create"></a>

> Use this endpoint to batch update the subscription state of up to 50 users on the Braze dashboard. 
  

To use this endpoint, you’ll need to generate an API key with the `subscription.status.set` permission.

You can access a subscription group’s `subscription_group_id` by navigating to the **Subscriptions Group** page.

## Rate limit

For customers who onboarded with Braze on or after January 6, 2022, we apply a rate limit of 5,000 requests per minute shared across the `/subscription/status/set` and `/v2/subscription/status/set` endpoint as documented in [API rate limits](http://localhost:4000/docs/api/api_limits/).

## Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `subscription_group_id` | Required | String | The `id` of your subscription group. |
| `subscription_state` | Required | String | Available values are `unsubscribed` (not in subscription group) or `subscribed` (in subscription group). |
| `external_ids` | Required\* | Array of strings | The `external_id` of the user or users, may include up to 50 `id`s. |
| `phones` | Required\* | String in [E.164](https://en.wikipedia.org/wiki/E.164) format | The phone numbers of the user, can be passed as an array of strings. Must include at least one phone number (with a max of 50). |

### Example successful response

Response: (status 201)

``` json
{
    "message": "success"
}

```

**API Endpoint**: `POST /v2/subscription/status/set`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `V2SubscriptionStatusSetCreateBody.builder().subscriptionGroups(List.of(V2SubscriptionStatusSetCreateBodySubscriptionGroupsItem.builder().emails(List.of("example1@email.com","example2@email.com")).subscriptionGroupId("subscription_group_identifier").subscriptionState("subscribed").build())).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.V2SubscriptionStatusSetCreateBody;
import com.yourorg.brazejava.model.V2SubscriptionStatusSetCreateBodySubscriptionGroupsItem;
import com.yourorg.brazejava.resources.v2.subscription.status.set.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.v2().subscription().status().set().create(CreateRequest
                .builder()
                .data(V2SubscriptionStatusSetCreateBody
                      .builder()
                      .subscriptionGroups(List.of(
                                  V2SubscriptionStatusSetCreateBodySubscriptionGroupsItem
                                  .builder()
                                  .emails(List.of(
                                          "example1@email.com",
                                          "example2@email.com"
                                          ))
                                  .subscriptionGroupId("subscription_group_identifier")
                                  .subscriptionState("subscribed")
                                  .build()
                              ))
                      .build())
                .build());
```
