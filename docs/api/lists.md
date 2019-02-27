The lists API allows you to get details about lists. The following endpoints
are available:

* [Get details](#get-details)
* [Get all](#get-all)

### Get details

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

Returns details about a specific list based on the provided ID.

```
GET https://api.sendingbee.com/v1/lists/<id>
```

```json
{
  "lists": {
    "id": "5bc852352859fb28b7392759",
    "project": "48db0d30166f0ecbf85367f5",
    "name": "Newsletter",
    "public": true,
    "short_description": "A monthly newsletter with the latest news",
    "implicit": false,
    "segments": [
      "5bc9bfd47a9a353823c5d041"
    ],
    "count": 73450
  },
  "segments": [
    {
      "id": "5bc9bfd47a9a353823c5d041",
      "name": "Active",
      "query": [
        {
          "and": [
            {
              "field": "$any(campaigns).$filter('opened').length",
              "operator": ">",
              "value": 10
            }
          ]
        }
      ],
      "count": 18212
    }
  ]
}
```

- The **id** property is a unique ID assigned to the list within the project
- The **public** property specifies whether the list is visible on a
contact's preference page.
- The **implicit** property specifies whether contacts are automatically
added to this list on create/update.
- The **lists.segments** property is an array of segment IDs. You can find
the actual data in **segments.
- The **count** property specifies the current number of matching contacts.

### Get all

?> The token needs to have the **MANAGE_CONTACTS** permission to perform this
action. More details at [Authentication and
Authorization](/api#authentication-and-authorization).

Returns details about all campaigns within the project.

```
GET https://api.sendingbee.com/v1/lists?project=<project_id>
```

The response will be an array of the same structure as in the [Get details
byID](#get-details-by-id) case.
