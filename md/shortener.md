## Shortener API

> Documentation of the Shortener API. Reading this implies that you have already read the [Getting started][link-getstarted] guide

Shortener allows you to create minified URLs of the form `https://emrio.fr/l/XXXXX`

The current latest version of the API: `v1`

**Table of content:**
- How it works
- Getting information on an ID
- Creating a minified URL
- Deleting a minified URL

### How it works

Each minified URL has a unique ID. Going to `https://emrio.fr/l/abcdefg` redirects you to the URL associated with the ID `abcdefg`.

IDs are made of alphanumerical unaccentuated characters (a to Z and 0 to 9)

Creating a minified URL using the API binds it to your user so that you can later modify/delete it.

### Getting information on an ID

To get information on an ID (e.g.: `abcdefg`), you can use the following endpoint:

```
GET https://apis.emrio.fr/shortener/?id=abcdefg
```

If the ID exists and no error occurs, it outputs the following:
```json
{
  "code": 200,
  "message": "Request succeeded",
  "data": {
    "id": "abcdefg",
    "original_url": "http://example.com/a/very/long/url",
    "url": "http://emrio.fr/l/abcdefg",
    "popularity": 10
  }
}
```

Here:
- `id` (String) is the ID of the minified URL
- `original_url` (String) is the URL the link redirects to
- `url` (String) is the minified URL
- `popularity` (Number) is the number of times this URL has been used

The response does not show the associated user.

### Creating a minified URL

**Note:** This request requires authentication

To create a new minified URL (e.g., for `http://example.com`), you can use the following endpoint:

```
POST https://apis.emrio.fr/shortener
```

The request should also contain `x-www-form-urlencoded` form data that should look like this:

```
url=http://example.com
```

If the request succeeds, a JSON should return a response like the following:
```json
{
  "code": 200,
  "message": "Request succeeded",
  "data": {
    "id": "abcdefg",
    "original_url": "http://example.com",
    "url": "http://emrio.fr/l/abcdefg",
    "popularity": 0
  }
}
```

The minified URL is bound to your Emrio account.

### Deleting a minified URL

**Note:** This request requires authentication

Deleting a minified URL (e.g., the id of `abcdefg`) should be made at:

```
DELETE https://apis.emrio.fr/shortener
```

With the following `x-www-form-urlencoded` form data:

```
id=abcdefg
```

If you did not create the minified URL, the request would return a 403 HTTP error.
However, if the request succeeds, the request should output:

```json
{
  "code": 200,
  "message": "Request succeeded",
  "data": {
    "id": "abcdefg",
    "original_url": "http://example.com",
    "url": "http://emrio.fr/l/abcdefg",
    "popularity": 10
  }
}
```

After this point, the URL will no longer redirect to the site.


[link-myaccount]: //emrio.fr/myaccount
[link-getstarted]: //emrio.fr/apis/getstarted
