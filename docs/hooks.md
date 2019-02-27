Hooks allow external systems to observe events happening on SendingBee. When
an event happens, SendingBee will trigger an appropriate hook which will
eventually call its predefined URL and send the event's details.

Note that events are **batched** (buffered) - they're not sent right away.
This means that a hook call will actually deliver an array of events rather
than just one. The calls are made every 5 minutes or when the number of
buffered events exceeds 100.

As of right now, SendingBee will send events for campaign events only (email
bounced, contact complained, or clicked a link). We plan to expand the list
of supported events in the future. If you have a specific event you would
like us to support, please contact us at
[support@sendingbee.com](mailto:suppport@sendingbee.com).

#### Setup

Navigate to "Hooks" in the left sidebar and click "New". The **name** of the
hook is for you only, the **URL** is the endpoint the hook will call. It can
include credentials. Finally, you can choose the type of events the endpoint
should receive.

<p class="centered">
  ![hooks](../_assets/images/hooks.png ':size=300')
</p>

Once saved, the endpoint will receive a "test" request with the following
JSON:

```json
{
  "version": 1,
  "id": "kXLgYoHmwVJDfMp/2VRsGAqkcXlMn/raiVlwyEV9cD0=",
  "hook_id": "5b965e006ed2557dd2d0c5d6",
  "timestamp": 1539007935,
  "events": []
}
```

- The **version** property specifies the version of the structure of the payload.
- The **id** property is unique to every batch. You can use this to make sure
you only process each batch once. We will not send a batch twice under normal
circumstances but it might happen e.g. if there's a network issue and we do
not receive a successful response.
- The **hook_id** is the ID of the hook as created in the admin interface.
- The **timestamp** is a UNIX timestamp of the moment a batch is ready to be
sent.
- The **events** is an array of events. In the case of the very first "test"
request, the array will be empty. Afterwards it will contain the following
structure:

```json
{
  "type": "link_clicked",
  "timestamp": 1539007935,
  "campaign_id": "5bbc8ba774b00e45b7f51bb1",
  "contact_id": "5bbc8ba774b00e45b7f51bb1",
  "custom_fields": {
    "email": "jiri@sensible.io",
    "first_name": "Jiri",
    "last_name": "Pospisil"
  },
  "link_url": "https://example.com",
  "user_agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) ..."
}
```

- The **type** property is the type of the event. It will be "bounced",
"complained", or "link_clicked".
- The **timestamp** is the UNIX time the event occurred.
- The **campaign_id** is the ID of the campaign the email was part of.
- The **contact_id** is the ID of the contact.
- The **custom_fields** are the custom fields the contact had at the time of
the event.
- The **link_url** is the link the contact clicked. It's present only when
the type is "link_clicked".
- The **user_agent** is the user agent the
contact used to click the link. It's present only when the type is
"link_clicked".

The endpoint must return the following JSON as a response for every request
(be it the first "test" request or any other):

```json
{
  "hello": "sendingbee"
}
```

If the endpoint fails to respond with the proper response, it will not
receive any real events. You can of course request another "test" request
later on by clicking on "Setup" in Actions.

<p class="centered">
  ![hooks2](../_assets/images/hooks2.png ':size=300')
</p>
