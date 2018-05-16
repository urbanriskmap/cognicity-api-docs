# Cities

CogniCity deployments are organised by city. Cities are delineated by a unique code and bounding box geometries.

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
                106.48,
                -6.733
              ],
              [
                107.175,
                -6.733
              ],
              [
                107.175,
                -5.88
              ],
              [
                106.48,
                -5.88
              ],
              [
                106.48,
                -6.733
              ]
            ]
          ]
        },
        "properties": {
          "code": "jbd",
          "name": "Jabodetabek"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Polygon",
          "coordinates": [
            [
              [
                107.369,
                -7.165
              ],
              [
                107.931,
                -7.165
              ],
              [
                107.931,
                -6.668
              ],
              [
                107.369,
                -6.668
              ],
              [
                107.369,
                -7.165
              ]
            ]
          ]
        },
        "properties": {
          "code": "bdg",
          "name": "Bandung"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Polygon",
          "coordinates": [
            [
              [
                112.3975,
                -7.5499
              ],
              [
                113.0318,
                -7.5499
              ],
              [
                113.0318,
                -7.0143
              ],
              [
                112.3975,
                -7.0143
              ],
              [
                112.3975,
                -7.5499
              ]
            ]
          ]
        },
        "properties": {
          "code": "sby",
          "name": "Surabaya"
        }
      },
      {
        "type": "Feature",
        "geometry": {
          "type": "Polygon",
          "coordinates": [
            [
              [
                110.057,
                -7.33525
              ],
              [
                110.715,
                -7.33525
              ],
              [
                110.715,
                -6.72701
              ],
              [
                110.057,
                -6.72701
              ],
              [
                110.057,
                -7.33525
              ]
            ]
          ]
        },
        "properties": {
          "code": "srg",
          "name": "Semarang"
        }
      }
    ]
  }
}
```

This endpoint returns all cities covered by the CogniCity instance, including their three letter code and bounding box geometry.

### HTTP Request

`GET http://example.com/api/kittens`

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
