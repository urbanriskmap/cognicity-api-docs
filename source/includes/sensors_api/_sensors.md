## Sensors

### GET /

This endpoint returns a collection of sensors and their properties within the specified bounding box. If no bounding box is provided all sensors in the database will be returned.

```shell
curl "/?bbox=-81,27,-79,25&geoformat=geojson"

```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/', {
  params: {
    bbox: '-81,27,-79,25',
    geoformat: 'geojson'
    }
  })
  .then(response => console.log(response))
  .catch(err => console.log(err))

```

> The response body contains the following JSON object:

```json
{
    "statusCode": 200,
    "result": {
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
          },
          {
            "type": "Feature",
            "geometry": {
              "type": "Point",
              "coordinates": [
                -80.1153333,
                26.31780556
              ]
            },
            "properties": {
              "id": "3",
              "created": "2017-10-24T22:35:58.883Z",
              "properties": {
                "uid": "261903080065601",
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

#### HTTP Request

`GET /`

#### Query Parameters

Parameter | Required | Description | Default | Example |
--------- | ------- | ------------ | ------- | ------- |
bbox | false | A list of longitude and latitude pairs representing the top left and bottom right corners of a bounding box for sensor locations. | none | longitude, latitude, longitude, latitude
geoformat | false | Specifies either 'geojson' or 'topojson' | geojson | geojson |
agency | false | Optional filter properties.agency of the sensor (e.g. 'USGS') |

#### Response
The returned data uses the GeoJSON FeatureCollection or TopoJSON GeometryCollection types. The properties of each sensor feature as described in the following table.

Attribute | Type | Description |
--------- | --------- | ----------- |
id | integer | Unique sensor identifier |
created | string | timestamp sensor created in database (ISO 8601 format) |
properties | json | metadata attributes for each sensor |

### POST /


This endpoint creates a new sensor. On success a GeoJSON feature representing the new sensor is returned.

```shell
curl -X POST / -H 'Content-Type: application/json' -H 'x-api-key: key' -d '{
	"properties":{
		"name": "test sensor",
    "agency": "usgs"
	},
	"location":{
		"lat": 25.0,
		"lng": -80.0
	}
}'

```

```javascript
import axios from 'axios'; // package to make http requests

axios.post('/', {
    properties: {
      name: "test sensor",
      agency: "usgs"
    },
    location: {
      lat: 25.0,
      lng: -80.0
    }
  }, {headers: {'x-api-key': 'key'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured like this:

```json
{
    "statusCode": 200,
    "result": {
        "type": "FeatureCollection",
        "features": [
            {
                "type": "Feature",
                "geometry": {
                    "type": "Point",
                    "coordinates": [
                        -80.0,
                        25.0
                    ]
                },
                "properties": {
                    "id": "4",
                    "created": "2018-03-16T18:25:07.613Z",
                    "properties": {
                        "name": "test sensor",
                        "agency": "usgs"
                    }
                }
            }
        ]
    }
}
```

#### HTTP Request

`POST / `

<aside class="success">
This request requires an API key for authorization using the `x-api-key` header.
</aside>


#### New Sensor Attributes
Attribute | Type | Description | Required
--------- | ---- | ----------- | --------
properties | object | Sensor metadata properties | Yes
properties.agency | string | Optional agency tag for sensor (e.g. 'usgs')
location | object | An object with `lat` and `lng` numerical values representing the sensor's latitude and longitude | Yes

### Delete Sensor

```sh
curl -X DELETE /4 -H 'Content-Type: application/json' -H 'x-api-key: key'

```

```javascript
import axios from 'axios'; // http requests
// delete record 2345 from sensor 4
axios.delete('/sensors/4', {headers: {'x-api-key': 'key'}, {'content-type': 'application/json'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

```json
{
    "statusCode": 200,
    "body": {}
}
```
This endpoint deletes a sensor and any data from that sensor. On success the statusCode and an empty body object are returned.

<aside class="success">
This request requires an API key for authorization using the `x-api-key` header.
</aside>

#### HTTP Request

`DELETE /:id`