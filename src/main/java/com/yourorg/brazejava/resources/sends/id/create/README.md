
### Create Send IDs For Message Send Tracking <a name="create"></a>

> Use this endpoint to create send IDs that can be used to send messages and track message performance programatically, without campaign creation for each send. 
  

To use this endpoint, you’ll need to generate an API key with the `sends.id.create` permission.

Using the send identifier to track and send messages is useful if you are planning to programmatically generate and send content.

## Rate limit

The daily maximum number of custom send identifiers that can be created via this endpoint is 100 for a given app group. Each `send_id` and `campaign_id` combination that you create will count towards your daily limit. The response headers for any valid request include the current rate limit status, see [API rate limits](https://www.braze.com/docs/api/api_limits/) for details.

### Request parameters

| Parameter | Required | Data Type | Description |
| --- | --- | --- | --- |
| `campaign_id` | Required | String | See [campaign identifier]({{site.baseurl}}/api/identifier_types/). |
| `send_id` | Optional | String | See [send identifier]({{site.baseurl}}/api/identifier_types/). |

## Response

### Example success response

``` json
Content-Type: application/json
Authorization: Bearer YOUR-REST-API-KEY
{
  "message": "success",
  "send_id" : (string) the send identifier
}

```

**API Endpoint**: `POST /sends/id/create`

#### Parameters

| Parameter | Required | Description | Example |
|-----------|:--------:|-------------|--------|
| `data` | ✗ |  | `SendsIdCreateCreateBody.builder().campaignId("campaign_identifier").sendId("send_identifier").build()` |

#### Example Snippet

```java
import java.util.Map;

import com.yourorg.brazejava.Client;
import com.yourorg.brazejava.model.SendsIdCreateCreateBody;
import com.yourorg.brazejava.resources.sends.id.create.params.CreateRequest;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
Map<?, ?> res = client.sends().id().create().create(CreateRequest
                .builder()
                .data(SendsIdCreateCreateBody
                      .builder()
                      .campaignId("campaign_identifier")
                      .sendId("send_identifier")
                      .build())
                .build());
```
