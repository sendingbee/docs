The contacts API allows you to search, add, update, and remove contacts. The
following endpoints are available:

* [Get details by ID](#get-details-by-id)
* [Search by query](#search-by-query)
* [Upsert by email](#upsert-by-email)
* [Update by ID](#update-by-id)
* [Add to lists](#add-to-lists)
* [Delete by ID](#delete-by-id)
* [Delete by email](#delete-by-email)
* [Delete by query](#delete-by-query)

### Get details by ID

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

Returns details about a specific contact based on the provided ID.

```
GET https://api.sendingbee.com/v1/contacts/<id>
```

```json
{
  "contacts": {
    "id": "5bbdc22133a6d55c84c8392b",
    "project": "5bbcc26dad44334d12e4c297",
    "created_at": "2018-10-10T09:48:37.015Z",
    "active": true,
    "bounced": false,
    "complained": false,
    "unsubscribed_from_all": false,
    "custom_fields": {
      "email": "jiri@sensible.io",
      "first_name": "Jiri"
    },
    "lists": ["5bbcc26dad44334d12e4c297", "5bbcc26dad44334d12e4c298", "5bbcc26dad44334d12e4c299"],
    "gravatar_url": "https://...",

    "links": {
      "self": "/v1/contacts/5bbdc22133a6d55c84c8392b"
    }
  }
}
```

- The **id** is a unique ID assigned to the contact within a specific
project.
- The **bounced** property says whether the contact has ever
[bounced](/contacts), similarly for **complained** and
**unsubscribed_from_all**. If all of them are false, then **active** is true.
- The **lists** property will contain all of the lists the contact is a
member of including system and implicit lists.
- The **gravatar_url** property will be present only if the project has
gravatars enabled in settings.

### Search by query

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The search endpoint allows you to query the list of contacts using a query.
The [query language](/api/contacts/query-language) allows to search for
contacts based on custom fields, lists, segments, or their campaign history.

```
GET https://api.sendingbee.com/v1/contacts?project=<project_id>&query=<query>
```

```json
[
  {
    field: "first_name",
    operator: "=",
    value: "Jiri"
  }
]
```

**Request**

To send the query, it needs to be stringified and encodeURIComponent encoded.
A request with the query above might look like this:

```
curl http://api.sendingbee.com/v1/contacts?project=<project_id>&query=%5B%7B%22field%22%3A%22first_name%22%2C%22operator%22%3A%22%3D%22%2C%22value%22%3A%22Jiri%22%7D%5D'
```

**Response**

```json
{
  "contacts": [
    {
      // The same as in the "Get details by ID" case
    },
  ],
  "meta": {
    "total": 1,
    "sa": "..."
  }
}
```

The **meta** property contains the *total* number of matches and the *sa*
property. The *sa* property is used to paginate the results. The endpoint
will return 15 contacts. If the total is more than that, you need to make an
additional query with a *sa* query parameter. Note that the value of *sa*
will be different with each result, you need to use the latest value.

```
curl http://api.sendingbee.com/v1/contacts?project=<project_id>&query=<query>&sa=<sa>
```

See [Query language](/api/contacts/query-language) for the full list of supported
queries. We will expand the list of supported queries as we go. If you have a
need for a specific query, please contact us at
[support@sendingbee.com](mailto:suppport@sendingbee.com).

### Upsert by email

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The upsert endpoint will create or update a contact based on the provided
**email address**. In case a contact with the provided email address already
exists, it will merge the existing custom fields with the provided ones. If
you want to unset a custom field, set its value to *null*. Note that the
provided custom fields need to exist in order to be set. Unknown custom
fields are ignored. If you provide **lists**, they will be merged with those
already present.

**Request**

```
POST https://api.sendingbee.com/v1/contacts
```

```json
{
  "contact": {
    "project": "5bbcc26dad44334d12e4c297",
    "lists": ["5bbcc26dad44334d12e4c298", "5bbcc26dad44334d12e4c299"],
    "custom_fields": {
      "email": "jiri@sensible.io",
      "first_name": "Jiri"
    }
  }
}
```

**Response**

The HTTP status will be different based on whether the contact has been
created (201) or updated (200). The actual response body will be the same as
in the [Get details](#get-details) case.

### Update by ID

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The update endpoint will update a contact based on its **ID**. Existing
custom fields are merged with those already set. If you want to unset a
custom field, set its value to *null*. If you provide **lists**, they will
*replace* those already set (this is different from upsert!).

**Request**

```
PATCH https://api.sendingbee.com/v1/contacts/<id>
```

```json
{
  "contact": {
    "custom_fields": {
      "last_name": "Pospisil"
    }
  }
}
```

**Response**

The HTTP status will be 200 on success, 4xx otherwise. The response body will
be the same as in the [Get details](#get-details) case.

### Add to lists

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The endpoint allows to add matching contacts into a set of lists. See [Query
language](/api/contacts/query-language) for more details.

**Request**

```
POST https://api.sendingbee.com/v1/contacts/add_to_lists
```

```json
{
  "list_ids": ["5bc9957f2ca28c3651db824a", "5bc9957f2ca28c3651db824b"],
  "query": [
    {
      "field": "score",
      "operator": ">",
      "value": 1000
    }
  ]
}
```

**Response**

The HTTP status will be 204 on success, 4xx otherwise. There will be no body returned.

### Delete by ID

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The delete endpoint will delete a contact based on its **ID**.

**Request**

```
DELETE https://api.sendingbee.com/v1/contacts/<id>
```

**Response**

The HTTP status will be 204 on success, 4xx otherwise. There will be no body
returned.

### Delete by email

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The endpoint will delete a contact based on its **email address** within the
given project.

**Request**

```
DELETE https://api.sendingbee.com/v1/contacts/email
```

```json
{
  "contact": {
    "project": "5bbcc26dad44334d12e4c297",
    "custom_fields": {
      "email": "jiri@sensible.io"
    }
  }
}
```

**Response**

The HTTP status will be 204 on success, 4xx otherwise. There will be no body returned.

### Delete by query

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The endpoint will delete a contact based on a
[query](/api/contacts/query-language.md). The query needs to be stringified and
encodeURIComponent encoded.

**Request**

```
DELETE https://api.sendingbee.com/v1/contact?project=<project_id>&query=<query>
```

**Response**

The HTTP status will be 200 on success, 4xx otherwise.
