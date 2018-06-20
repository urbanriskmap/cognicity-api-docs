## Version

### Get CogniCity Version

Get the CogniCity server and database versions for the chosen instance.

The following attributes are returned:

- `version` refers to CogniCity Server [release version](https://github.com/urbanriskmap/cognicity-server/releases)
- `schema` refers to the CogniCity Database [release version](https://github.com/urbanriskmap/cognicity-schema/releases)

```shell
curl '/'
```

```javascript
const request = require('request');
request(
  {
    method: 'GET',
    uri: '/'
  },
  function (error, response, body) {
    console.log(error);
    console.log(response.statusCode);
    console.log(body)
  }
)
```

> Example JSON output:

```json
{
  "version":"3.0.6",
  "schema":"3.0.6"
}
```

This endpoint gets the CogniCity server and database versions.

#### HTTP Request

`GET /`
