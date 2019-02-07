## Accounts API

> Documentation of the Accounts API. Reading this implies that you have already read the [Getting started][link-getstarted] guide

Accounts allows you to get pieces of information on accounts of Emrio.fr

The base URL of this API is `https://apis.emrio.fr/accounts/`.

The current latest version of the API is `v1`.

**Table of content:**
- Username and email availability
- User lookup

### Username and email availability

You can test if an email address or a username is available (no account has this email/name) with these URLs:

To test for a username:
```
GET https://apis.emrio.fr/accounts/availability?username=Someone
```

To test for an email address
```
GET https://apis.emrio.fr/accounts/availability?email=some.one@emrio.fr
```

The response looks like this:
```json
{
  "code": 200,
  "message": "Request succeeded",
  "data": {
    "usernameOrEmail": "Someone",
    "taken": true
  }
}
```

- `usernameOrEmail` (String) is set depending on the given input
- `taken` (Boolean) is set to true when an account already have this username/email

The API only considers the `email` property if both `username` and `email` are set.

### User lookup

You can lookup for a user's information using this API.

**Warning:** If a user decided to put his account in restricted mode, querying for this user returns a `204 - No content.`

To lookup a user based on a username
```
GET https://apis.emrio.fr/accounts/lookup?username=Someone
```

To lookup a user based on an email address
```
GET https://apis.emrio.fr/accounts/lookup?username=some.one@emrio.fr
```

If the user exists and allows to show its information, the response looks like this:
```json
{
  "code": 200,
  "message": "Request succeeded",
  "data": {
    "role": "user",
    "username": "Someone",
    "email": "some.one@emrio.fr",
    "active": true,
    "creationDate": 1549105249229,
    "lastEditDate": 1549105517380
  }
}
```

If no user matches, the endpoint returns `204 - No content` and sets the `data` property to `null`.

[link-getstarted]: //emrio.fr/apis/getstarted
