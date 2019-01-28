SendingBee uses its own simple JSON based query language. The language is
used for searching for contacts both internally and externally (via API). The
language offers a number of queries to match against contacts including
matching on custom fields, lists, segments, or campaign history.

We will expand the list of supported queries as we go. If you have a need for
a specific query, please contact us at
[support@sendingbee.com](mailto:suppport@sendingbee.com).

* [Custom fields](#custom-fields)
* [Lists and segments](#lists-and-segments)
* [Campaigns](#campaigns)
* [Links](#links)
* [Meta](#meta)

### Custom fields

You can query based on custom fields. Every query is an array, and by
default, there's an implicit *AND* operator between the elements.

```json
[
  {
    "field": "first_name",
    "operator": "=",
    "value": "Jiri"
  },

  {
    "field": "last_name",
    "operator": "=",
    "value": "Pospisil"
  }
]
```

You can make the query more explicit by mentioning the operator. The
following query is equivalent.

```json
[
  {
    "and": [
      {
        "field": "first_name",
        "operator": "=",
        "value": "Jiri"
      },

      {
        "field": "last_name",
        "operator": "=",
        "value": "Pospisil"
      }
    ]
  }
]
```

As you can imagine, there's a also an *OR* operator. You need to use the more
explicit form to use it. Each query supports a different set of operators. In
the case of custom fields, the operators might also be different based on the
data type of a specific custom field.

The supported operators are:

<table>
  <thead>
    <th>
      Operator
    </th>
    <th>
      Description
    </th>
  </thead>

  <tbody>
    <tr>
      <td>
        =
      </td>
      <td>
        The value must match match exactly. Available to all data types.
      </td>
    </tr>
    <tr>
      <td>
        !=
      </td>
      <td>
        The value must NOT match exactly. Available to all data types.
      </td>
    </tr>
    <tr>
      <td>
        &
      </td>
      <td>
        The value must contain the given string. Available to string and email data types.
      </td>
    </tr>
    <tr>
      <td>
        !&
      </td>
      <td>
        The value must NOT contain the given string. Available to string and email data types.
      </td>
    </tr>
    <tr>
      <td>
        ^
      </td>
      <td>
        The value must start the given string. Available to string and email data types.
      </td>
    </tr>
    <tr>
      <td>
        !^
      </td>
      <td>
        The value must NOT start the given string. Available to string and email data types.
      </td>
    </tr>
    <tr>
      <td>
        >
      </td>
      <td>
        The value must be greater than the given value. Available to number and date data types.
      </td>
    </tr>
    <tr>
      <td>
        >=
      </td>
      <td>
        The value must be greater or equal than the given value. Available to number and date data types.
      </td>
    </tr>
    <tr>
      <td>
        <
      </td>
      <td>
        The value must be less than the given value. Available to number and date data types.
      </td>
    </tr>
    <tr>
      <td>
        <=
      </td>
      <td>
        The value must be less or equal than the given value. Available to number and date data types.
      </td>
    </tr>
  </tbody>
</table>

The values the query is matching against also need to have a proper data
type:

- Strings and emails must match against strings.
- Numbers against integers.
- Booleans against booleans.
- Dates against strings in the ISO format *YYYY-MM-DD* or *now* (the current
time). It's also possible to use a *now-Nd* where N is an integer 1-9 (now
minus N days). A plus operator is available as well.

### Lists and segments

You can query based on list or segment membership. You can get the IDs of
lists/segments using the [Lists and segment](/api/lists) APIs.

```json
[
  {
    "field": "$any(lists).id",
    "operator": "=",
    "value": "<list_id>",
  }

  {
    "field": "$any(segments).id",
    "operator": "=",
    "value": "<segment_id>",
  }
]
```

### Campaigns

You can query whether a particular contact has been **sent** or has
**opened** a specific campaign. You can also query the time of
the opening (**opened_at**).

Contacts who have opened the campaign:

```json
[
  {
    "field": "$find(campaigns, '<campaign_id>').opened",
    "operator": "=",
    "value": true
  }
]
```

Contacts who have opened the campaign in the past 7 days:

```json
[
  {
    "field": "$find(campaigns, '<campaign_id>').opened_at",
    "operator": ">",
    "value": "now-7d"
  }
]
```

You can also query whether a contact has ever **opened** or been **sent** a
campaign. Only range operators allowed.

```json
[
  {
    "field": "$any(campaigns).$filter('opened').length",
    "operator": ">",
    "value": 1
  }
]
```

You can get the list of campaigns and their IDs from the
[Campaigns](/api/campaigns.md) endpoint.

### Links

You can query whether a particular contact has **clicked** a link within a
given campaign and when the event happened (**clicked_at**).

Contacts who have clicked the link in the past 7 days:

```json
[
  {
    "field": "$find(campaigns, '<campaign_id>').$find(links, '<link_hash>').clicked_at",
    "operator": ">=",
    "value": "now-7d"
  }
]
```

Contacts who have clicked ANY link in the past 7 days:

```json
[
  {
    "field": "$find(campaigns, '<campaign_id>').$any(links).clicked_at",
    "operator": ">",
    "value": "now-7d",
  }
]
```

You can also ask whether a particular contact has clicked ANY link within a
campaign. Note that the only supported operator/value pairs are =/0 and >=/1.

```json
[
  {
    "field": "$find(campaigns, '<campaign_id>').$filter('clicked').length",
    "operator": ">=",
    "value": 1
  }
]
```

Similarly, you can ask whether a contact has clicked ANY links regardless of
campaigns. Only range operators allowed.

```json
[
  {
    "field": "$any(links).$filter('clicked').length",
    "operator": ">",
    "value": 1
  }
]
```

You can get the list of campaigns, their IDs, and link hashes from the
[Campaigns](/api/campaigns.md) endpoint.

### Meta

You can query "meta" information about a contact. Those are properties
managed by the system itself and include:

- **id** - Match against a specific contact ID.
- **bounced** - Match only contacts who have bounced.
- **complained** - Match only contacts who have complained.
- **active** - Match only active contacts

You can find more information about the states in the
[Contacts](/contacts.md) documentation.

```json
[
  {
    "field": "$meta.id",
    "operator": "=",
    "value": "<contact_id>",
  },

  {
    "field": "$meta.id",
    "operator": "!=",
    "value": "<contact_id2>",
  },

  {
    "field": "$meta.active",
    "operator": "=",
    "value": true,
  }
]
```
