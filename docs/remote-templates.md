Remote templates allow you to keep email templates in your own system and
have them imported automatically.

All that's required is for your system to make the templates available via an
HTTPS endpoint in the given format. You can of course make the endpoint
password protected and embed the credentials in the URL.

#### Setup on SendingBee

Navigate to "Remote templates" in the sidebar and choose "New Remote
Template". The **name** of the remote template is for your organization
purposes only. The **URL** should point to your system's endpoint. Note that
the URL needs to use the HTTPS protocol.

<p class="centered">
  ![remote templates](../_assets/images/remote_templates.png ':size=300')
</p>

In this example, we're fetching templates from "https://example.com" with
username "user" and password "password".

The templates will be fetches immediately and then **every 5 minutes on
demand**. Note that your system needs to respond within 5 seconds. Be sure to
also include [ETag](https://en.wikipedia.org/wiki/HTTP_ETag) in the response
to make the whole process more efficient for both sides.

#### Setup on your side

The endpoint you've specified needs to return templates in the following
UTF-8 encoded JSON format:

```json
{
  templates: [
    {
      name: "Template #1",
      html: "...",
      text: "..."
    },

    // ...
  ]
}
```

The **name** property must to be a string and cannot exceed 50 characters in
length. The **html** property must to be a string as well and cannot exceed
150 000 characters. Similarly for **text** but the limit is 100 000
characters. Both **html** and **text** are optional. The overall JSON size
cannot exceed 1MB.

####  Usage

Once both sides are set up, head to *Campaigns* or *Templates* and see the
remote templates loaded in the *Remote templates* tab.

<p class="centered">
  ![remote templates](../_assets/images/remote_templates2.png)
</p>
