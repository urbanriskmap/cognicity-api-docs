# Authentication

```shell
curl "endpoint" -H "Authorization: token or key"

```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/endpoint', {'headers': {'Authorization': 'token'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))

```

```python
import requests # module to make http requests

headers = {'Authorization': 'token'}
response = requests.get('/endpoint', headers=headers)

print (response.status_code)
print (response.json())        
```

Some CogniCity endpoints require authentication in the form of either an API key or a JSON Web Token. Authentication keys or tokens are passed via the `x-api-key` or `Authorization` headers. Endpoints requiring authentication are detailed below. 

`x-api-key: key`

`Authorization: token`

<aside class="success">
All requests should be made via https.
</aside>
