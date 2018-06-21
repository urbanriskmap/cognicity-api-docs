## Twitter

Send and receive Twitter direct message events.

### POST /twitter/send


```shell
curl -X POST '/twitter/send' -H 'Content-Type: application/json' -H 'x-api-key: key' -d '{
    "reportId": 1,
    "instanceRegionCode": "brw",
    "language": "en",
    "username": "userid",
    "network": "twitter"
}'
```

```javascript
import axios from 'axios'; // package to make http requests

axios.post('/', {
    reportId: 1,
    instanceRegionCode: "brw",
    language: "en",
    username: "userid",
    network: "twitter"
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

`POST /twitter/send`

#### Properties
Attribute | Required | Description | Example
--------- | -------- | ----------- | -------
reportId  | true | The unique ID of the report submitted | none | 1
instanceRegionCode | true | The instance region containing the report (from the /cities endpoint). May be null. | "brw"
language | true | The user's 2 letter language if known. May be null | "en"
username | true | The username or user id number from the social network | "123"
network | true | The name of the social network of the user | "twitter"

<aside class="success">
This request requires an API key for authorization using the `x-api-key` header.
</aside>

### GET /twitter/webhook

```shell
curl "/twitter/webhook?crc_token=<token>"
```

```javascript
// Webhook configured at developer.twitter.com
```

> The above command returns JSON structured like this:

```json
{
    "response_token": "<token>"
}
```

This endpoint responds to a twitter Webhook challenge response check. See https://developer.twitter.com/en/docs/accounts-and-users/subscribe-account-activity/overview

#### HTTP Request

`GET /twitter/webhook`

### POST /twitter/webhook
```sh
curl -X POST '/twitter/webhook' -H 'Content-Type: application/json' -H 'x-api-key: key' -d '{
    <message event>
}'
```

```javascript
// Webhook configured at developer.twitter.com
```

> The above command returns JSON structured like this:

```json
{}
```

This endpoint responds to a twitter Webhook message event. See twitter [documentation](https://developers.twitter.com/docs/messenger-platform/getting-started/webhook-setup/) for more details.

#### HTTP Request

`POST /twitter/webhook`