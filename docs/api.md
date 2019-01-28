SendingBee can be used either through its the web interface or pragmatically
via its APIs. The APIs allow you to do anything the web interface does. After
all, the web interface is just another client of those APIs.

As of right now, we're not ready to commit to stability of most of the APIs.
Things can change, be removed, or added in a breaking way. Please use only
the APIs described here.

#### Authentication and Authorization

All of the APIs require token authentication. SendingBee supports creating
tokens with different permissions. That way you can create a token for every
environment with only the necessary permissions.

<p class="centered">
  ![remote templates](../_assets/images/api.png ':size=500')
</p>

You can create these tokens by navigating to your Profile. Once you have a
token, provide it with every request in the "Authorization" header as
follows:

```bash
curl -H 'Authorization: Bearer <token>' ...
```

Continue to [Contacts](/api/contacts).
