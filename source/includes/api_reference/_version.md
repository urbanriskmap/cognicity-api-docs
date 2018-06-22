## Version

### GET /

Gets the CogniCity server and database versions.

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

#### HTTP Request

`GET /`
