
### Track Users <a name="create"></a>

> Use this endpoint to record custom events, purchases, and update user profile attributes. 
  

To use this endpoint, you’ll need to generate an API key with the `users.track` permission.

**Note:** Braze processes the data passed via API at face value and customers should only pass deltas (changing data) to minimize unnecessary data point consumption. To read more, refer to [Data points](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points#data-points).

Customers using the API for server-to-server calls may need to allowlist `rest.iad-01.braze.com` if they’re behind a firewall.

### Rate limit

We apply a base speed limit of 50,000 requests per minute to this endpoint for all customers. Each request to the `/users/track` endpoint can contain up to 75 events, 75 attribute updates, and 75 purchases. Each component (event, attribute, and purchase arrays), can update up to 75 users each for a max of 225 individual data points. Each update can also belong to the same user for a max of 225 updates to a single user in a request.

See our page on [API rate limits](https://www.braze.com/docs/api/api_limits/) for details, and reach out to your customer success manager if you need your limit increased.

### Request parameters

For each of the request components listed in the following table, one of `external_id`, `user_alias`, or `braze_id` is required.

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `attributes` | Optional | Array of attributes objects | See [user attributes object](https://www.braze.com/docs/api/objects_filters/user_attributes_object/) |
| `events` | Optional | Array of event objects | See [events object](https://www.braze.com/docs/api/objects_filters/event_object/) |
| `purchases` | Optional | Array of purchase objects | See [purchases object](https://www.braze.com/docs/api/objects_filters/purchase_object/) |

## User track responses

Upon using any of the aforementioned API requests you should receive one of the following three general responses:

#### Successful message

Successful messages will be met with the following response:

``` json
{
  "message" : "success",
  "attributes_processed" : (optional, integer), if attributes are included in the request, this will return an integer of the number of external_ids with attributes that were queued to be processed,
  "events_processed" : (optional, integer), if events are included in the request, this will return an integer of the number of events that were queued to be processed,
  "purchases_processed" : (optional, integer), if purchases are included in the request, this will return an integer of the number of purchases that were queued to be processed,
}

```

#### Successful message with non-fatal errors

If your message is successful but has non-fatal errors such as one invalid event object out of a long list of events, then you will receive the following response:

``` json
{
  "message" : "success",
  "errors" : [
    {
    }
  ]
}

```

#### Message with fatal errors

In the case of a success, any data that was not affected by an error in the `errors` array will still be processed. If your message has a fatal error you will receive the following response:

``` json
{
  "message" : ,
  "errors" : [
    {
    }
  ]
}

```

### Fatal error response codes

For status codes and associated error messages that will be returned if your request encounters a fatal error, reference [Fatal errors & responses](https://www.braze.com/api/errors/#fatal-errors).

If you receive the error “provided external_id is blacklisted and disallowed”, your request may have included a “dummy user”. For more information, refer to [Spam blocking](https://www.braze.com/docs/user_guide/data_and_analytics/user_data_collection/user_archival/#spam-blocking).

### Creating an alias-only user profile

Keep the following nuances in mind when using the `/users/track` endpoint:

You can use the `/users/track` endpoint to create a new alias-only user by setting the `_update_existing_only` key with a value of `false` in the body of the request. If this value is omitted, the alias-only user profile will not be created. Using an alias-only user guarantees that one profile with that alias will exist. This is especially helpful when building a new integration as it prevents the creation of duplicate user profiles.

### Importing legacy user data

You may submit data through the Braze API for a user who has not yet used your mobile app in order to generate a user profile. If the user subsequently uses the application all information following their identification via the SDK will be merged with the existing user profile you created via the API call. Any user behavior that is recorded anonymously by the SDK prior to identification will be lost upon merging with the existing API-generated user profile.

The segmentation tool will include these users regardless of whether they have engaged with the app. If you want to exclude users uploaded via the User API who have not yet engaged with the app, simply add the filter: `Session Count > 0`.

### Making bulk updates

If you have a use case where you need to make batch updates to the `users/track` endpoint, we recommend adding the bulk update header so that Braze can properly identify, observe, and route your request.

Refer to the following sample request with the `X-Braze-Bulk` header:

``` json
curl --location --request POST 'https://rest.iad-01.braze.com/users/track' \
--header 'Content-Type: application/json' \
--header 'X-Braze-Bulk: true' \
--header 'Authorization: Bearer YOUR-API-KEY-HERE' \
--data-raw '{ "attributes": [ ], "events": [ ], "purchases": [ ] }'

```

Warning: When the `X-Braze-Bulk` header is present with any value, Braze will consider the request a bulk request. Set the value to `true`. Currently, setting the value to `false` does not disable the header—it will still be treated as if it were true.

#### Use cases

Consider the following use cases where you may use the bulk update header:

- A daily job where multiple users’ custom attributes are updated via the `/users/track` endpoint.
- An ad-hoc user data backfill script which updates user information via the `/users/track` endpoint.

**API Endpoint**: `POST /users/track`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `UsersTrackCreateBody.builder().attributes(List.of(Map.ofEntries(Map.entry("array_attribute", List.of("banana","apple")),Map.entry("boolean_attribute_1", true),Map.entry("external_id", "rachel_feinberg"),Map.entry("integer_attribute", 25),Map.entry("string_attribute", "fruit")))).events(List.of(Map.ofEntries(Map.entry("app_id", "your_app_identifier"),Map.entry("external_id", "user_identifier"),Map.entry("name", "rented_movie"),Map.entry("properties", Map.ofEntries(Map.entry("cast", List.of(Map.ofEntries(Map.entry("name", "Actor1")),Map.ofEntries(Map.entry("name", "Actor2")))),Map.entry("release", Map.ofEntries(Map.entry("studio", "FilmStudio"),Map.entry("year", "2022"))))),Map.entry("time", "2022-12-06T19:20:45+01:00")),Map.ofEntries(Map.entry("app_id", "your_app_identifier"),Map.entry("name", "rented_movie"),Map.entry("time", "2013-07-16T19:20:50+01:00"),Map.entry("user_alias", Map.ofEntries(Map.entry("alias_label", "my_device_identifier"),Map.entry("alias_name", "device123")))))).purchases(List.of(Map.ofEntries(Map.entry("app_id", "your_app_identifier"),Map.entry("currency", "USD"),Map.entry("external_id", "user_identifier"),Map.entry("price", 12.12),Map.entry("product_id", "product_name"),Map.entry("properties", Map.ofEntries(Map.entry("brand", "Backpack Locker"),Map.entry("checkout_duration", 180),Map.entry("color", "red"),Map.entry("monogram", "ABC"),Map.entry("size", "Large"))),Map.entry("quantity", 6),Map.entry("time", "2017-05-12T18:47:12Z")))).build()` |

#### Example Snippet

```java
import java.util.List;
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.UsersTrackCreateBody;
import com.yourorg.brazejava.resources.users.track.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.users().track().create(CreateRequest
                .builder()
                .data(UsersTrackCreateBody
                      .builder()
                      .attributes(List.of(
                                      Map.ofEntries(
                                              Map.entry("array_attribute", List.of(
                                                      "banana",
                                                      "apple"
                                                      )),
                                              Map.entry("boolean_attribute_1", true),
                                              Map.entry("external_id", "rachel_feinberg"),
                                              Map.entry("integer_attribute", 25),
                                              Map.entry("string_attribute", "fruit")
                                      )
                                  ))
                      .events(List.of(
                                  Map.ofEntries(
                                      Map.entry("app_id", "your_app_identifier"),
                                      Map.entry("external_id", "user_identifier"),
                                      Map.entry("name", "rented_movie"),
                                      Map.entry("properties", Map.ofEntries(
                                              Map.entry("cast", List.of(
                                                      Map.ofEntries(
                                                              Map.entry("name", "Actor1")
                                                      ),
                                                      Map.ofEntries(
                                                              Map.entry("name", "Actor2")
                                                      )
                                                      )),
                                              Map.entry("release", Map.ofEntries(
                                                      Map.entry("studio", "FilmStudio"),
                                                      Map.entry("year", "2022")
                                                      ))
                                              )),
                                      Map.entry("time", "2022-12-06T19:20:45+01:00")
                                  ),
                                  Map.ofEntries(
                                      Map.entry("app_id", "your_app_identifier"),
                                      Map.entry("name", "rented_movie"),
                                      Map.entry("time", "2013-07-16T19:20:50+01:00"),
                                      Map.entry("user_alias", Map.ofEntries(
                                              Map.entry("alias_label", "my_device_identifier"),
                                              Map.entry("alias_name", "device123")
                                              ))
                                  )
                              ))
                      .purchases(List.of(
                                     Map.ofEntries(
                                             Map.entry("app_id", "your_app_identifier"),
                                             Map.entry("currency", "USD"),
                                             Map.entry("external_id", "user_identifier"),
                                             Map.entry("price", 12.12),
                                             Map.entry("product_id", "product_name"),
                                             Map.entry("properties", Map.ofEntries(
                                                     Map.entry("brand", "Backpack Locker"),
                                                     Map.entry("checkout_duration", 180),
                                                     Map.entry("color", "red"),
                                                     Map.entry("monogram", "ABC"),
                                                     Map.entry("size", "Large")
                                                     )),
                                             Map.entry("quantity", 6),
                                             Map.entry("time", "2017-05-12T18:47:12Z")
                                     )
                                 ))
                      .build())
                .build());
```
