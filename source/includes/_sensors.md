# Sensors

The CogniCity Sensors endpoints support centralising data from automated sensor networks. Sensor data can be inserted into the database, and is served as GeoJSON to support map visualisations.

<aside class="notice">
Note that these endpoints reside on a separate sensors subdomain (e.g. sensors.petabencana.id).
</aside>

## Authentication

Sensor endpoints requiring an API key are documented below.

## Get All Sensors

```python
import requests

response = requests.get('https://sensors.{instance}.{tld}/sensors')
if (response.status_code == 200):
  data = response.json()        # success
  print(data)
else:
  print(response.status_code)      # error            
```

```shell
curl "https://sensors.{instance}.{tld}/sensors"
```

```javascript
const request = require('request');
request(
  {
    method: 'GET',
    uri: 'https://sensors.{instance}.{tld}/sensors'
  },
  function (error, response, body) {
    console.log(error);
    console.log(response.statusCode);
    console.log(body)
  }
)
```

> The response body contains the following JSON object:

```json
{
    "statusCode": 200,
    "body": {
        "type": "FeatureCollection",
        "features": [
            {
                "type": "Feature",
                "geometry": {
                    "type": "Point",
                    "coordinates": [
                        -80.3853056,
                        26.0341111
                    ]
                },
                "properties": {
                    "id": "2",
                    "created": "2017-10-24T22:35:58.875Z",
                    "properties": {
                        "uid": "260653080184901",
                        "type": "GW",
                        "class": "62610",
                        "units": "ft"
                    }
                }
            }
        ]
    }
}
```

This endpoint returns a GeoJSON (or TopoJSON) collection of sensors and their properties within the specific bounding box. If no bounding box is provided all sensors in database will be returned.

Sensor locations are point geometries defined using latitude and longitude coordinates in the WGS 1984 datum (EPSG 4326).

### HTTP Request

`GET https://sensors.{instance}.{tld}/sensors`

### Query Parameters

Parameter | Required | Description | Default | Example |
--------- | ------- | ------------ | ------- | ------- |
bbox | false | A list of longitude and latitude pairs represening the top left and bottom right corners of a bounding box for sensor locations. | none | longitude, latitude, longitude, latitude
geoformat | false | Specifies either 'geojson' or 'topojson'. | geojson | geojson |

### Properties
The returned data uses the GeoJSON FeatureCollection standard (or GeometryCollection for TopoJSON).

Attribute | Data Type | Description |
--------- | --------- | ----------- |
id | integer | Unique sensor identifier |
created | string | timestamp sensor created in database (ISO 8601 format) |
properties | json | metadata attributes for each sensor |

## Get Data for a Specific Sensor

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific sensor.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete
