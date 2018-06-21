## Facebook

Send and receive Facebook messenger events.

### Thank you message


```shell
curl -X POST '/facebook/send' -H 'Content-Type: application/json' -H 'x-api-key: key' -d '{
    "reportId": 1,
    "instanceRegionCode": "brw",
    "language": "en",
    "username": "userid",
    "network": "facebook"
}'
```

```javascript
import axios from 'axios'; // package to make http requests

axios.post('/', {
    reportId: 1,
    instanceRegionCode: "brw",
    language: "en",
    username: "userid",
    network: "facebook"
  }, {headers: {'x-api-key': 'key'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))```
```

> The above command returns JSON structured like this:

```json
{}
```

Send a reply to user after they submit a report.

#### HTTP Request

`POST /facebook/send`

#### Properties
Attribute | Required | Description | Example
--------- | -------- | ----------- | -------
reportId  | true | The unique ID of the report submitted | none | 1
instanceRegionCode | true | The instance region containing the report (from the /cities endpoint). May be null. | "brw"
language | true | The user's 2 letter language if known. May be null | "en"
username | true | The username or user id number from the social network | "123"
network | true | The name of the social network of the user | "facebook"

<aside class="success">
This request requires an API key for authorization using the `x-api-key` header.
</aside>

### Webhook Challenge

```shell
curl "/facebook/webhook?hub.verify_token=<token>"
```

```javascript
// Webhook configured at developers.facebook.com
```

> The above command returns JSON structured like this:

```json
{
    // hub challenge value
}
```

This endpoint responds to a Facebook Webhook authentication challenge. See https://developers.facebook.com/docs/messenger-platform/getting-started/webhook-setup/

#### HTTP Request

`GET /facebook/webhook`

### Webhook Message Event
```sh
curl -X POST '/facebook/webhook' -H 'Content-Type: application/json' -H 'x-api-key: key' -d '{
    <message event>
}'
```

```javascript
// Webhook configured at developers.facebook.com
```

> The above command returns JSON structured like this:

```json
{}
```

This endpoint responds to a Facebook Webhook message event. See Facebook [documentation](https://developers.facebook.com/docs/messenger-platform/getting-started/webhook-setup/) for more details.

#### HTTP Request

`POST /facebook/webhook`