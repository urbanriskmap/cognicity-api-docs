## Infrastructure

CogniCity stores the locations of local infrastructure including flood gates, pumps, waterways and drainage basins to assist mapping. Note that not all infrastructure are necessarily available in each instance.

**Available Infrastructure Types**

The following types of infrastructure are available:

- floodgates
- pumps
- waterways
- sites (measurement stations) 
- basins (drainage)

### GET /infrastructure

This endpoint returns the location and attributes of the specific infrastructure.

```shell
curl /infrastructure/pumps
```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/infrastructure/pumps',
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "result": {
    "type": "Topology",
    "objects": {
      "output": {
        "type": "GeometryCollection",
        "geometries": [
          {
            "type": "Point",
            "properties": {
              "name": "PA Marina"
            },
            "coordinates": [
              7164,
              7352,
              0
            ]
          },
          {
            "type": "Point",
            "properties": {
              "name": "Pompa Waduk Setia Budi Barat"
            },
            "coordinates": [
              5312,
              5077,
              0
            ]
          },
          // etc. etc. //
          {
            "type": "Point",
            "properties": {
              "name": "Pompa UP Senen"
            },
            "coordinates": [
              6143,
              6544,
              0
            ]
          }
        ]
      }
    },
    "arcs": [],
    "transform": {
      "scale": [
        0.000020651319451945148,
        0.000020217245084508508
      ],
      "translate": [
        106.7188310623,
        -6.3060956581
      ]
    },
    "bbox": [
      106.7188310623,
      -6.3060956581,
      106.9253236055,
      -6.1039434245
    ]
  }
}
```

#### HTTP Request
GET /infrastructure/:type

#### Request Parameters
Attribute | Type | Description | Required | Default |
--------- | ---- | ----------- | -------- | ------- |
city | string | Which city do we want data for (e.g. 'jbd')? | No | None
format | string | Format of the returned data (must be 'json') | No | json
geoformat | string | Format for geographical objects (one of 'geojson' or 'topojson') | No | topojson