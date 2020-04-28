The campaigns API allows you to get details, send, cancel, and delete
campaigns. The following endpoints are available:

* [Get details](#get-details)
* [Get all](#get-all)
* [Send](#send)
* [Cancel](#cancel)
* [Delete](#delete)

### Get details

?> The token needs to have the **MANAGE_CAMPAIGNS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

Returns details about a specific campaigns based on the provided ID.

```
GET https://api.sendingbee.com/v1/campaigns/<id>
```

```json
{
  "campaigns": {
    "id": "5b97b3c85d81888ba509d999",
    "project": "5b965da2379be47dfe4e7e2b",
    "name": "Newsletter #1",
    "send_at": "2018-09-11T12:23:36.224Z",
    "query": [
      {
        "field": "$meta.active",
        "operator": "=",
        "value": true
      },
      {
        "or": [
          {
            "field": "$any(lists).id",
            "operator": "=",
            "value": "5b965da3379be47dfe4e7e3b"
          }
        ]
      }
    ],
    "updatable": false,
    "canceled": false,
    "waiting": false,
    "planning": false,
    "continuous": false,
    "continuous_interval": 120,
    "template": {
      "subject": "",
      "html": ""
    },
    "template_links": [
      {
        "link": "https://example.com",
        "hash": "100680ad546ce6a577f42f52df33b4cfdca756859e664b8d7de329b150d09ce9"
      }
    ],
    "referenced_lists": [
      {
        "id": "5b965da3379be47dfe4e7e3b"
      }
    ],
    "referenced_segments": [],
    "links": {
      "self": "/v1/campaigns/5b97b3c85d81888ba509d999",
      "project": "/v1/projects/5b965da2379be47dfe4e7e2b"
    }
  }
}
```

- The **id** property is a unique ID assigned to the campaign within the project
- The **send_at** property is the time the campaign is scheduled to be sent / was sent. The time will be pushed forward automatically for continuous campaigns.
- The **query** property contains the final query which will/was used to match contacts.
- The **updatable** property says whether the campaign can be updated
(edited). A campaign can be edited only if it's continuous, or if it's in the
**waiting** state and there's more than 60 seconds to **send_at**.
- The **canceled** property says whether the campaign has been manually canceled.
- The **waiting** property says whether the campaign is currently waiting for
**send_at**.
- The **planning** property says whether the campaign is currently being
planned (contacts are being matched using the **query** and emails will begin
being send shortly).
- The **continuous** property says whether the campaign is continuous, that
is, whether the campaign will be send repeatedly to newly matching contacts
in **continuous_interval** intervals.
- The **template_links** property contains all links found in the template.
The hashes are used as identifiers for other APIs.

### Get all

?> The token needs to have the **MANAGE_CAMPAIGNS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

Returns details about all campaigns within the project.

```
GET https://api.sendingbee.com/v1/campaigns?project=<project_id>
```

The response will be an array of the same structure as in the [Get details byID](#get-details-by-id) case.

### Send

?> The token needs to have the **MANAGE_CAMPAIGNS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The endpoint allows to create new campaigns. In this case, we're creating a
[continuous campaign](/campaigns#continuous-campaigns) (sent every hour)
to all members of list with ID "5b97e9beae72949465b1f339". The first emails
will be sent on 2018-09-30 at 09:50:00 UTC.

See [Query language](/api/contacts/query-language) for more information about
the way matching works.

**Request**

```
POST https://api.sendingbee.com/v1/campaigns
```

```json
{
  "campaign": {
    "name": "Continuous Welcome Campaign",
    "project": "5b965da2379be47dfe4e7e2b",
    "template": {
      "subject": "Welcome",
      "html": "...",
    },
    "query": [
      {
        "field": "$any(lists).id",
        "operator": "=",
        "value": "5b97e9beae72949465b1f339"
      }
    ],
    "send_at": "2018-09-30T09:50:00Z",
    "continuous": true
  }
}
```

- The **template** property contains the actual email content. The **text**
  version will be automatically created from the **html** one.
- The **query** property contains a query in the [Query
language](/api/contacts/query-language) format.
- The **send_at** property contains a time on which the campaign should be
sent. You can omit this property to send immediatelly.
- The **continuous** property specified whether this is a [continuous
campaign](/campaigns#continuous-campaign). You can omit this property
(defaults to false).

**Response**

The HTTP status will be 201 on success, 4xx otherwise.

```json
{
  "campaigns": {
    "id": "5bc5af8f5458bdff93df91fe",

    "links": {
      "self": "/v1/campaigns/5bc5af8f5458bdff93df91fe",
      "project": "/v1/projects/5b965da2379be47dfe4e7e2b"
    }
  }
}
```

### Cancel

?> The token needs to have the **MANAGE_CAMPAIGNS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The cancel endpoint will [cancel](/campaigns#cancel-and-delete) a campaign
based on its **ID**.

**Request**

```
POST https://api.sendingbee.com/v1/campaigns/<id>/cancel
```

**Response**

The HTTP status will be 204 on success, 4xx otherwise. There will be no body
returned.

### Delete

?> The token needs to have the **MANAGE_CAMPAIGNS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The delete endpoint will [delete](/campaigns#cancel-and-delete) a campaign
based on its **ID**.

**Request**

```
DELETE https://api.sendingbee.com/v1/campaigns/<id>
```

**Response**

The HTTP status will be 204 on success, 4xx otherwise. There will be no body
returned.
