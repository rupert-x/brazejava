
# Braze Endpoints Java SDK

## Overview
# Braze API overview

Braze provides a high-performance REST API to allow you to track users, send messages, export data, and more. This reference article covers what a REST API is, the terminology, a brief overview of API keys, and API limits.

A REST API is a way to programmatically transfer information over the web using a predefined schema. Braze has created many different endpoints which perform various actions and/or return various data.

Braze manages a number of different instances for our dashboard and REST Endpoints. When your account is provisioned you will log in to one of the following URLs. Use the correct REST endpoint based on which instance you are provisioned to. If you are unsure, open a [support ticket](https://www.braze.com/docs/braze_support/) or use the following table to match the URL of the dashboard you use to the correct REST Endpoint.

> Customers using Braze’s EU database should use the `https://rest.fra-01.braze.eu/` endpoint. This endpoint will be used when configuring the Braze [iOS](https://www.braze.com/docs/developer_guide/platform_integration_guides/ios/initial_sdk_setup/completing_integration/#compile-time-endpoint-configuration-recommended), [Android](https://www.braze.com/docs/developer_guide/platform_integration_guides/android/initial_sdk_setup/android_sdk_integration/#step-2-configure-the-braze-sdk-in-brazexml), and [Web](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/initial_sdk_setup/#step-2-initialize-braze) SDKs.

## Braze Instances

| Instance | Dashboard URL | REST Endpoint |
| --- | --- | --- |
| US-01 | `https://dashboard.braze.com` or  <br>`https://dashboard-01.braze.com` | `https://rest.iad-01.braze.com` |
| US-02 | `https://dashboard-02.braze.com` | `https://rest.iad-02.braze.com` |
| US-03 | `https://dashboard-03.braze.com` | `https://rest.iad-03.braze.com` |
| US-04 | `https://dashboard-04.braze.com` | `https://rest.iad-04.braze.com` |
| US-05 | `https://dashboard-05.braze.com` | `https://rest.iad-05.braze.com` |
| US-06 | `https://dashboard-06.braze.com` | `https://rest.iad-06.braze.com` |
| US-08 | `https://dashboard-08.braze.com` | `https://rest.iad-08.braze.com` |
| EU-01 | `https://dashboard-01.braze.eu` | `https://rest.fra-01.braze.eu` |
| EU-02 | `https://dashboard-02.braze.eu` | `https://rest.fra-02.braze.eu` |

# Using Braze's Postman collection

If you have a Postman account (you can download macOS, Windows, and Linux versions from the [Postman website](https://www.getpostman.com/) ), you can open our Postman documentation in your own Postman app by clicking the orange **Run in Postman** button. You can then [create an environment](https://www.braze.com/docs/api/postman_collection/#setting-up-your-postman-environment), or use our Braze REST API environment as a template, and edit the available `POST` and `GET` requests to suit your own needs.

## Setting up your Postman environment

The Braze Postman Collection uses a templating variable, `https://rest.example.braze.com`, to substitute the REST API URL of your Braze instance into the pre-built requests, and the `{{api_key}}` variable for your API Key. Rather than having to manually edit all requests in the Collection, you can set up this variable in your Postman environment. You can either select our templated environment (Braze REST API Environment Template) from the dropdown and replace the variable values with your own, or you can set up your own environment.

To set up your own environment, perform the following steps:

1.  From the **Workspaces** tab, select **Environments**.
2.  Click the **+** plus button to create a new environment.
3.  Give this environment a name (e.g., “Braze API Requests”) and add keys for `instance_url` and `api_key` with values corresponding to your [Braze instance](https://www.braze.com/docs/developer_guide/rest_api/basics/#endpoints) and [Braze REST API Key](https://www.braze.com/docs/api/api_key/).
4.  Click **Save**.
    

## Using the pre-built requests from the collection

Once you have configured your environment. You can use any of the pre-built requests in the collection as a template for building new API requests. To start using one of the pre-built requests, click on it within the **Collections** menu of Postman. This will open the request as a new tab in the main window of the Postman app.

In general, there are two types of requests that Braze’s API endpoints accept - `GET` and `POST`. Depending on which `HTTP` method the endpoint uses, you’ll need to edit the pre-built request differently.

### Edit a POST request

When editing a `POST` request, open the request and navigate to the **Body** section in the request editor. For readability, select the **raw** radio button to format the `JSON` request body.

### Edit a GET request

When editing a `GET` request, edit the parameters passed in the request URL. To do so, select the **Params** tab and edit the key-value pairs in the fields that appear.

## Send your request

Once your API request is ready, click **Send**. The request sends and the response data populates in a section underneath the request editor. From here, you can view the raw data returned from Braze’s API, see the HTTP response code, see how long the request took to process, and view header information.

The following documentation can be found on the Braze documentation site:

*   [Object & filter specifications](https://www.braze.com/docs/api/objects_filters/)
*   [API key overview](https://www.braze.com/docs/api/api_key/)
*   [API identifier types](https://www.braze.com/docs/api/identifier_types/)
*   [Errors & responses](https://www.braze.com/docs/api/errors/)
*   [Parameters](https://www.braze.com/docs/api/parameters)
*   [Data retention](https://www.braze.com/docs/api/data_retention/)
*   [API network connectivity issues](https://www.braze.com/docs/api/network_connectivity_issues)
*   [Rate limits](https://www.braze.com/docs/api/api_limits/)
*   [API campaigns](https://www.braze.com/docs/api/api_campaigns/)

#### Example Client Initialization

```java
import com.yourorg.brazejava.Client;

Client client = Client
                .builder()
                .withBearerAuth(System.getenv("API_TOKEN"))
                .build();
```

## Module Documentation and Snippets

### [campaigns.dataSeries](src/main/java/com/yourorg/brazejava/resources/campaigns/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/campaigns/dataseries/README.md#list) - Export Campaign Analytics

### [campaigns.details](src/main/java/com/yourorg/brazejava/resources/campaigns/details/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/campaigns/details/README.md#list) - Export Campaign Details

### [campaigns.list](src/main/java/com/yourorg/brazejava/resources/campaigns/list/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/campaigns/list/README.md#list) - Export Campaign List

### [campaigns.trigger.schedule.create](src/main/java/com/yourorg/brazejava/resources/campaigns/trigger/schedule/create/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/campaigns/trigger/schedule/create/README.md#create) - Schedule API Triggered Campaigns

### [campaigns.trigger.schedule.delete](src/main/java/com/yourorg/brazejava/resources/campaigns/trigger/schedule/delete/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/campaigns/trigger/schedule/delete/README.md#create) - Delete Scheduled API Triggered Campaigns

### [campaigns.trigger.schedule.update](src/main/java/com/yourorg/brazejava/resources/campaigns/trigger/schedule/update/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/campaigns/trigger/schedule/update/README.md#create) - Update Scheduled API Triggered Campaigns

### [campaigns.trigger.send](src/main/java/com/yourorg/brazejava/resources/campaigns/trigger/send/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/campaigns/trigger/send/README.md#create) - Send Campaign Messages via API Triggered Delivery

### [canvas.dataSeries](src/main/java/com/yourorg/brazejava/resources/canvas/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/canvas/dataseries/README.md#list) - Export Canvas Data Series Analytics

### [canvas.dataSummary](src/main/java/com/yourorg/brazejava/resources/canvas/datasummary/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/canvas/datasummary/README.md#list) - Export Canvas Data Analytics Summary

### [canvas.details](src/main/java/com/yourorg/brazejava/resources/canvas/details/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/canvas/details/README.md#list) - Export Canvas Details

### [canvas.list](src/main/java/com/yourorg/brazejava/resources/canvas/list/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/canvas/list/README.md#list) - Export Canvas List

### [canvas.trigger.schedule.create](src/main/java/com/yourorg/brazejava/resources/canvas/trigger/schedule/create/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/canvas/trigger/schedule/create/README.md#create) - Schedule API Triggered Canvases

### [canvas.trigger.schedule.delete](src/main/java/com/yourorg/brazejava/resources/canvas/trigger/schedule/delete/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/canvas/trigger/schedule/delete/README.md#create) - Delete Scheduled API-Triggered Canvases

### [canvas.trigger.schedule.update](src/main/java/com/yourorg/brazejava/resources/canvas/trigger/schedule/update/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/canvas/trigger/schedule/update/README.md#create) - Update Scheduled API Triggered Canvases

### [canvas.trigger.send](src/main/java/com/yourorg/brazejava/resources/canvas/trigger/send/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/canvas/trigger/send/README.md#create) - Send Canvas Messages via API Triggered Delivery

### [catalogs](src/main/java/com/yourorg/brazejava/resources/catalogs/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/catalogs/README.md#create) - Create Catalog
* [delete](src/main/java/com/yourorg/brazejava/resources/catalogs/README.md#delete) - Delete Catalog
* [list](src/main/java/com/yourorg/brazejava/resources/catalogs/README.md#list) - List Catalogs

### [catalogs.items](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#create) - Create Multiple Catalog Items
* [create_1](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#create_1) - Create Catalog Item
* [delete](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#delete) - Delete Multiple Catalog Items
* [delete_1](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#delete_1) - Delete a Catalog Item
* [get](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#get) - List Catalog Item Details
* [list](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#list) - List Multiple Catalog Item Details
* [patch](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#patch) - Edit Multiple Catalog Items
* [patch_1](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#patch_1) - Edit Catalog Items
* [update](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#update) - Update Catalog Item
* [update_1](src/main/java/com/yourorg/brazejava/resources/catalogs/items/README.md#update_1) - Update Catalog Item

### [contentBlocks.create](src/main/java/com/yourorg/brazejava/resources/contentblocks/create/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/contentblocks/create/README.md#create) - Create Content Block

### [contentBlocks.info](src/main/java/com/yourorg/brazejava/resources/contentblocks/info/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/contentblocks/info/README.md#list) - See Content Block Information

### [contentBlocks.list](src/main/java/com/yourorg/brazejava/resources/contentblocks/list/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/contentblocks/list/README.md#list) - List Available Content Blocks

### [contentBlocks.update](src/main/java/com/yourorg/brazejava/resources/contentblocks/update/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/contentblocks/update/README.md#create) - Update Content Block

### [email.blacklist](src/main/java/com/yourorg/brazejava/resources/email/blacklist/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/email/blacklist/README.md#create) - Blacklist Email Addresses

### [email.blocklist](src/main/java/com/yourorg/brazejava/resources/email/blocklist/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/email/blocklist/README.md#create) - Blocklist Email Addresses

### [email.bounce.remove](src/main/java/com/yourorg/brazejava/resources/email/bounce/remove/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/email/bounce/remove/README.md#create) - Remove Hard Bounced Emails

### [email.hardBounces](src/main/java/com/yourorg/brazejava/resources/email/hardbounces/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/email/hardbounces/README.md#list) - Query Hard Bounced Emails

### [email.spam.remove](src/main/java/com/yourorg/brazejava/resources/email/spam/remove/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/email/spam/remove/README.md#create) - Remove Email Addresses from Spam List

### [email.status](src/main/java/com/yourorg/brazejava/resources/email/status/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/email/status/README.md#create) - Change Email Subscription Status

### [email.unsubscribes](src/main/java/com/yourorg/brazejava/resources/email/unsubscribes/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/email/unsubscribes/README.md#list) - Query List of Unsubscribed Email Addresses

### [events.dataSeries](src/main/java/com/yourorg/brazejava/resources/events/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/events/dataseries/README.md#list) - Export Custom Events Analytics

### [events.list](src/main/java/com/yourorg/brazejava/resources/events/list/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/events/list/README.md#list) - Export Custom Events List

### [feed.dataSeries](src/main/java/com/yourorg/brazejava/resources/feed/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/feed/dataseries/README.md#list) - Export News Feed Card Analytics

### [feed.details](src/main/java/com/yourorg/brazejava/resources/feed/details/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/feed/details/README.md#list) - Export News Feed Cards Details

### [feed.list](src/main/java/com/yourorg/brazejava/resources/feed/list/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/feed/list/README.md#list) - Export News Feed Cards List

### [kpi.dau.dataSeries](src/main/java/com/yourorg/brazejava/resources/kpi/dau/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/kpi/dau/dataseries/README.md#list) - Export Daily Active Users by Date

### [kpi.mau.dataSeries](src/main/java/com/yourorg/brazejava/resources/kpi/mau/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/kpi/mau/dataseries/README.md#list) - Export Monthly Active Users for Last 30 Days

### [kpi.newUsers.dataSeries](src/main/java/com/yourorg/brazejava/resources/kpi/newusers/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/kpi/newusers/dataseries/README.md#list) - Export Daily New Users by Date

### [kpi.uninstalls.dataSeries](src/main/java/com/yourorg/brazejava/resources/kpi/uninstalls/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/kpi/uninstalls/dataseries/README.md#list) - Export KPIs for Daily App Uninstalls by Date

### [messages.liveActivity.update](src/main/java/com/yourorg/brazejava/resources/messages/liveactivity/update/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/messages/liveactivity/update/README.md#create) - Update Live Activity

### [messages.schedule.create](src/main/java/com/yourorg/brazejava/resources/messages/schedule/create/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/messages/schedule/create/README.md#create) - Create Scheduled Messages

### [messages.schedule.delete](src/main/java/com/yourorg/brazejava/resources/messages/schedule/delete/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/messages/schedule/delete/README.md#create) - Delete Scheduled Messages

### [messages.schedule.update](src/main/java/com/yourorg/brazejava/resources/messages/schedule/update/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/messages/schedule/update/README.md#create) - Update Scheduled Messages

### [messages.scheduledBroadcasts](src/main/java/com/yourorg/brazejava/resources/messages/scheduledbroadcasts/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/messages/scheduledbroadcasts/README.md#list) - List Upcoming Scheduled Campaigns and Canvases

### [messages.send](src/main/java/com/yourorg/brazejava/resources/messages/send/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/messages/send/README.md#create) - Send Messages Immediately via API Only

### [preferenceCenter.v1](src/main/java/com/yourorg/brazejava/resources/preferencecenter/v1/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/preferencecenter/v1/README.md#create) - Create Preference Center
* [get](src/main/java/com/yourorg/brazejava/resources/preferencecenter/v1/README.md#get) - View Details for Preference Center
* [update](src/main/java/com/yourorg/brazejava/resources/preferencecenter/v1/README.md#update) - Update Preference Center

### [preferenceCenter.v1.list](src/main/java/com/yourorg/brazejava/resources/preferencecenter/v1/list/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/preferencecenter/v1/list/README.md#list) - List Preference Centers

### [preferenceCenterV1.url](src/main/java/com/yourorg/brazejava/resources/preferencecenterv1/url/README.md)

* [get](src/main/java/com/yourorg/brazejava/resources/preferencecenterv1/url/README.md#get) - Generate Preference Center URL

### [purchases.productList](src/main/java/com/yourorg/brazejava/resources/purchases/productlist/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/purchases/productlist/README.md#list) - Export Product IDs

### [purchases.quantitySeries](src/main/java/com/yourorg/brazejava/resources/purchases/quantityseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/purchases/quantityseries/README.md#list) - Export Number of Purchases

### [purchases.revenueSeries](src/main/java/com/yourorg/brazejava/resources/purchases/revenueseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/purchases/revenueseries/README.md#list) - Export Revenue Data by Time

### [scim.v2.users](src/main/java/com/yourorg/brazejava/resources/scim/v2/users/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/scim/v2/users/README.md#create) - Create New Dashboard User Account
* [delete](src/main/java/com/yourorg/brazejava/resources/scim/v2/users/README.md#delete) - Remove Dashboard User Account
* [get](src/main/java/com/yourorg/brazejava/resources/scim/v2/users/README.md#get) - Look Up an Existing Dashboard User Account
* [list](src/main/java/com/yourorg/brazejava/resources/scim/v2/users/README.md#list) - Search Existing Dashboard User by Email
* [update](src/main/java/com/yourorg/brazejava/resources/scim/v2/users/README.md#update) - Update Dashboard User Account

### [segments.dataSeries](src/main/java/com/yourorg/brazejava/resources/segments/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/segments/dataseries/README.md#list) - Export Segment Analytics

### [segments.details](src/main/java/com/yourorg/brazejava/resources/segments/details/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/segments/details/README.md#list) - Export Segment Details

### [segments.list](src/main/java/com/yourorg/brazejava/resources/segments/list/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/segments/list/README.md#list) - Export Segment List

### [sends.dataSeries](src/main/java/com/yourorg/brazejava/resources/sends/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/sends/dataseries/README.md#list) - Export Send Analytics

### [sends.id.create](src/main/java/com/yourorg/brazejava/resources/sends/id/create/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/sends/id/create/README.md#create) - Create Send IDs For Message Send Tracking

### [sessions.dataSeries](src/main/java/com/yourorg/brazejava/resources/sessions/dataseries/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/sessions/dataseries/README.md#list) - Export App Sessions by Time

### [sms.invalidPhoneNumbers](src/main/java/com/yourorg/brazejava/resources/sms/invalidphonenumbers/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/sms/invalidphonenumbers/README.md#list) - Query Invalid Phone Numbers

### [sms.invalidPhoneNumbers.remove](src/main/java/com/yourorg/brazejava/resources/sms/invalidphonenumbers/remove/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/sms/invalidphonenumbers/remove/README.md#create) - Remove Invalid Phone Numbers

### [subscription.status.get](src/main/java/com/yourorg/brazejava/resources/subscription/status/get/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/subscription/status/get/README.md#list) - List User's  Subscription Group Status - SMS

### [subscription.status.set](src/main/java/com/yourorg/brazejava/resources/subscription/status/set/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/subscription/status/set/README.md#create) - Update User's Subscription Group Status - SMS

### [subscription.user.status](src/main/java/com/yourorg/brazejava/resources/subscription/user/status/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/subscription/user/status/README.md#list) - List User's Subscription Group - SMS

### [templates.email.create](src/main/java/com/yourorg/brazejava/resources/templates/email/create/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/templates/email/create/README.md#create) - Create Email Template

### [templates.email.info](src/main/java/com/yourorg/brazejava/resources/templates/email/info/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/templates/email/info/README.md#list) - See Email Template Information

### [templates.email.list](src/main/java/com/yourorg/brazejava/resources/templates/email/list/README.md)

* [list](src/main/java/com/yourorg/brazejava/resources/templates/email/list/README.md#list) - List Available Email Templates

### [templates.email.update](src/main/java/com/yourorg/brazejava/resources/templates/email/update/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/templates/email/update/README.md#create) - Update Email Template

### [transactional.v1.campaigns.send](src/main/java/com/yourorg/brazejava/resources/transactional/v1/campaigns/send/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/transactional/v1/campaigns/send/README.md#create) - Send Transactional Email via API Triggered Delivery

### [users.alias.new_](src/main/java/com/yourorg/brazejava/resources/users/alias/new__/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/alias/new__/README.md#create) - Create New User Aliases

### [users.alias.update](src/main/java/com/yourorg/brazejava/resources/users/alias/update/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/alias/update/README.md#create) - Update User Alias

### [users.delete](src/main/java/com/yourorg/brazejava/resources/users/delete/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/delete/README.md#create) - Delete Users

### [users.export.globalControlGroup](src/main/java/com/yourorg/brazejava/resources/users/export/globalcontrolgroup/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/export/globalcontrolgroup/README.md#create) - Export User Profile by Global Control Group

### [users.export.ids](src/main/java/com/yourorg/brazejava/resources/users/export/ids/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/export/ids/README.md#create) - Export User Profile by Identifier

### [users.export.segment](src/main/java/com/yourorg/brazejava/resources/users/export/segment/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/export/segment/README.md#create) - Export User Profile by Segment

### [users.externalIds.remove](src/main/java/com/yourorg/brazejava/resources/users/externalids/remove/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/externalids/remove/README.md#create) - Remove External ID

### [users.externalIds.rename](src/main/java/com/yourorg/brazejava/resources/users/externalids/rename/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/externalids/rename/README.md#create) - Rename External ID

### [users.identify](src/main/java/com/yourorg/brazejava/resources/users/identify/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/identify/README.md#create) - Identify Users

### [users.merge](src/main/java/com/yourorg/brazejava/resources/users/merge/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/merge/README.md#create) - Merge Users

### [users.track](src/main/java/com/yourorg/brazejava/resources/users/track/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/users/track/README.md#create) - Track Users

### [v2.subscription.status.set](src/main/java/com/yourorg/brazejava/resources/v2/subscription/status/set/README.md)

* [create](src/main/java/com/yourorg/brazejava/resources/v2/subscription/status/set/README.md#create) - Update User's Subscription Group Status V2

<!-- MODULE DOCS END -->
