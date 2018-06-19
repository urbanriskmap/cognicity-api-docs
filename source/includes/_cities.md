# Cities

CogniCity deployments are organised by city. Cities are delineated by a unique code and bounding box geometries. Note that the term "city" is used somewhat arbitrairily for organisational purposes. Cities may refer to an urban conurbation or wider metropolitan area. For example in the United States "Broward" is used to refer to the area of Broward County which includes multiple cities.

## Get All Cities

```shell
curl "/cities?geoformat=geojson"
```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/cities', {
  params: {
    geoformat: 'geojson'
    }
  })
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
          "type": "Polygon",
          "coordinates": [
            [
              [
                -80.56454636,
                26.4393434677
              ],
              [
                -80.011194015,
                26.4376911515
              ],
              [
                -80.0147106747,
                25.8743814793
              ],
              [
                -80.5690752042,
                25.8759818852
              ],
              [
                -80.56454636,
                26.4393434677
              ]
            ]
          ]
        },
        "properties": {
          "code": "brw",
          "name": "broward"
        }
      }
    ]
  }
}
```

This endpoint returns all cities covered by the CogniCity instance, including their three letter code and bounding box geometry.

### HTTP Request

`GET /cities`

### Query Parameters

Parameter | Required | Description | Default |
--------- | ------- | ------------ | ------- |
geoformat | false | Specifies either 'geojson' or 'topojson' | topojson |

### Response
The returned data uses the GeoJSON FeatureCollection or TopoJSON GeometryCollection types. The properties of each sensor feature as described in the following table.

Attribute | Type | Description |
--------- | --------- | ----------- |
code | string | Unique 3 letter code for each city |
name | string | City name |
