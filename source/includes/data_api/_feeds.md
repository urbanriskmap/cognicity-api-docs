## Feeds

The feeds endpoint supports input of hazard reports from third-party data-streams such as local civic applications. Reports collected from external data feeds are available from the /reports endpoint.

### POST /qlue

This endpoint accepts hazard reports from the [Qlue Smart City Application](http://www.qlue.co.id/).

```shell
curl -X post /feeds/qlue
  -H 'Content-Type: application/json' \
  -H 'x-api-key: api-key' \
  -d '{
    "post_id": "123",
    "created_at": "twitter",
    "title": "en",
    "text": "flooding!",
    "image_url": "url",
    "qlue_city": "jabodetabek",
    "disaster_type": "flood",
    "location": {
        "lat":-6.2,
        "lon":106.8
    }
}' 
```

```javascript
import axios from 'axios'; // package to make http requests

axios.post('/feeds/qlue', {
    post_id: 123,
    created_at: "2018-06-18T00:00+0700",
    title: "en",
    text: "flooding!",
    image_url: "url",
    qlue_city: "jabodetabek",
    disaster_type: "flood",
    location: {
        lat:-6.2,
        lon:106.8
    }
  }, {headers: {'x-api-key': 'key'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured like this:

```json
{
    "post_id": 1, 
    "created": true
}
```

#### HTTP Request
`POST /feeds/qlue`

#### Qlue Report Attributes
Attribute | Type | Description | Required |
--------- | ---- | ----------- | -------- |
post_id | number | Qlue identifier | Yes 
created_at | string | Timestamp in ISO8601 format YYYY-MM-DDTHH:MM:SS | Yes 
title | string | Title of report | No
text | string | Hazard description | Yes 
image_url | string | URL of image | No
qlue_city | string | City of report origin | No
disaster_type | string | Hazard type | Yes 
location | object | Point location, latitude and longitude | Yes