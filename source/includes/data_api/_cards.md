## Cards

Report cards for diaster events issued via social media chatbots. Report cards are the mechanism by which users can submit hazard reports. Cards are issued using a one-time-link based on a globally unique identifier (GUID) and can only be used to submit one hazard report. Subsequent hazard reports may be submitted by the user requesting a new card.

The card flow is as follows:

1. Request a new card (POST /cards)
2. Submit hazard report (PUT /cards/:id)
3. Upload image (GET /cards/:id/images)


### GET /cards/:id

This endpoint lists the status of a card. It is useful for checking whether a card has already been used to submit a hazard report.

```shell
curl /cards/:id
```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/cards')
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured as shown below. Note that in this example the card has not yet been submitted by the user. When querying a report that has been submitted additional report details including reportId are provided by this endpoint.

```json
{
    "statusCode": 200,
    "result": {
        "card_id": "guid",
        "network": "twitter",
        "language": "en",
        "received": false,
        "report": null
    }
}
```

#### HTTP Request

`GET /cards/:id`

### POST /cards

This endpoint creates a new card with a GUI, in preparation for submission of hazard information by user.

```shell
curl -X POST /cards
  -H 'Content-Type: application/json' \
  -H 'x-api-key: api-key' \
  -d '{
    "username": "123",
    "network":"twitter",
    "language":"en"
}' 
```

```javascript
import axios from 'axios'; // package to make http requests

axios.post('/cards', {
    username: "123",
    network: "twitter",
    language: "en"
  }, {headers: {'x-api-key': 'key'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured like this:

```json
{
    "cardId": "guid",
    "created": true
}
```

#### HTTP Request
`POST /cards`

#### New Card Attributes
Attribute | Type | Description | Required |
--------- | ---- | ----------- | -------- |
username | string | User social network username or id | Yes 
network | string | Name of social network (e.g. 'twitter') | Yes 
language | string | Two-letter language code for user (e.g. 'en') | Yes 

<aside class="success">
This request requires an API key for authorization using the `x-api-key` header.
</aside>

### PUT /cards/:id

This endpoint receives card information to create a hazard report. Once data is received a report will be generated and become available in the reports endpoint.

```shell
curl -X PUT /cards/:id
  -H 'Content-Type: application/json'
  -H 'x-api-key: api_key' 
  -d '{
    "card_data":{
    	"report_type":"flood",
    	"flood_depth": 20
    	},
    "disaster_type": "flood",
    "text": "Very big flood",
    "created_at":"2016-12-13T19:25:29",
    "location": {
        "lat":-6.4,
        "lng":106.6
    }
}' 
```

```javascript
import axios from 'axios'; // package to make http requests

axios.post('/', {
    card_data:{
    	report_type:"flood",
    	flood_depth: 20
    	},
    disaster_type: "flood",
    text: "Very big flood",
    created_at:"2016-12-13T19:25:29",
    location: {
        lat:-6.4,
        lng:106.6
    }
  }, {headers: {'x-api-key': 'key'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured like this:

```json
{
    "statusCode": 200,
    "cardId": "guid",
    "created": true
}
```

#### HTTP Request
`PUT /cards/:id`

#### Card Report Attributes
Attribute | Type | Description | Required |
--------- | ---- | ----------- | -------- |
card_data | object | Object containing hazard specific data | Yes 
disaster_type | string | Hazard type | Yes 
text | string | Hazard description | Yes 
created_at | string | Timestamp in ISO8601 format YYYY-MM-DDTHH:MM:SS | Yes 
disaster_type | string | Hazard type | Yes 
location | object | Point location, latitude and longitude | Yes


### GET /cards/:id/images

Get a signed AWS S3 URL to upload an image associated with a card. This must be done after card report has been created. Only one image can exist for a given card. See more in the AWS [documentation](https://docs.aws.amazon.com/AWSJavaScriptSDK/latest/AWS/S3.html#getSignedUrl-property).

```shell
curl GET /cards/:id/images
```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/cards/:id/images')
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured like this:

```json
{
    "signedRequest": "https://s3.us-west-2.amazonaws.com/domain/originals/guid.jpeg?aws-signature",
    "url": "https://s3.us-west-2.amazonaws.com/domain/originals/guid.jpeg"
}
```

#### HTTP Request
`GET /cards/:id/images`

<aside class="notice">
After an image is submitted a server-side process shrinks the image to a standard size and there may be a small time lag of a few seconds before the image goes "live" with the report.
</aside>