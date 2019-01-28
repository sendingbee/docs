The contact API allows you to search, update, and remove individual contacts
by [query](/api/contacts/query-language.md). The following endpoints are
available:

* [Get details by query](#get-details-by-query)
* [Update by query](#update-by-query)
* [Delete by query](#delete-by-query)

### Get details by query

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

Returns details about a specific contact based on the provided
[query](/api/contacts/query-language). The query needs to match exactly
**one** contact.

```
GET https://api.sendingbee.com/v1/contact?project=<project_id>&query=<query>
```

```json
[
  {
    field: "external_id",
    operator: "=",
    value: "42"
  }
]
```

**Request**

To send the query, it needs to be stringified and encodeURIComponent encoded.
A request with the query above might look like this:

```
curl http://api.sendingbee.com/v1/contact?project=<project_id>&query=%5B%7B%22field%22%3A%22external_id%22%2C%22operator%22%3A%22%3D%22%2C%22value%22%3A42%7D%5D
```

**Response**

The response by will the same as in the [Get details by
ID](/api/contacts#get-details-by-id) case. See [Query
language](/api/contacts/query-language) for the full list of supported
queries. We will expand the list of supported queries as we go. If you have a
need for a specific query, please contact us at
[support@sendingbee.com](mailto:suppport@sendingbee.com).


### Update by query

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The update endpoint will update a contact based on a
[query](/api/contacts/query-language.md). The query needs to match exactly
**one** contact.

Existing custom fields are merged with those already set. If you want to
unset a custom field, set its value to
*null*. If you provide **lists**, they will *replace* those already set.

**Request**

```
PATCH https://api.sendingbee.com/v1/contact?project=<project_id>&query=<query>
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

Take a look at the previous example how to format the query in the URL. The
body of the request is the same as accepted in the [Update by
ID](/api/contacts#update-by-id.md) endpoint.

**Response**

The HTTP status will be 200 on success, 4xx otherwise.

### Delete by query

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

The endpoint will delete a contact based on a
[query](/api/contacts/query-language.md). The query needs to match exactly
**one** contact.

**Request**

```
DELETE https://api.sendingbee.com/v1/contact?project=<project_id>&query=<query>
```

**Response**

The HTTP status will be 200 on success, 4xx otherwise.
