# Authentication

```shell
curl "endpoint" -H "Authorization: token or key"

```

```javascript
import axios from 'axios'; // package to make http requests

/* Request with API key authentication */
axios.get('/endpoint', {headers: {'x-api-key': 'key'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))

/* Request with token authentication */
axios.get('/endpoint', {headers: {'Authorization': 'token'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

Some CogniCity endpoints require authentication in the form of either an API key or a JSON Web Token. Authentication keys or tokens are passed via the `x-api-key` or `Authorization` headers. Endpoints requiring authentication are detailed below.

`x-api-key: key`

`Authorization: token`

<aside class="success">
All requests should be made via https.
</aside>
