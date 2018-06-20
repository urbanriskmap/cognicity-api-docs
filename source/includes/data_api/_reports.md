## Reports

The reports endpoint contains CogniCity reports submitted by the public. Reports are represented by point-geometries and their accompanying properties (e.g. description, time etc.). Note that all times are UTC, and geometries use the WGS 1984 coordinate system.

### Get All Reports

```shell
curl "/reports?city=brw&geoformat=geojson"

```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/reports', {
  params: {
    city: 'brw',
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
          "type": "Point",
          "coordinates": [
            -80.0946879387,
            26.1381793399
          ]
        },
        "properties": {
          "pkey": "94",
          "created_at": "2018-06-19T17:53:43.229Z",
          "source": "grasp",
          "status": "confirmed",
          "url": "ad63ccb2-024f-4617-81a1-4e8782499afa",
          "image_url": "https://images.riskmap.us/ad63ccb2-024f-4617-81a1-4e8782499afa.jpg",
          "disaster_type": "flood",
          "report_data": {
            "report_type": "flood",
            "flood_depth": 8
          },
          "tags": {
            "district_id": null,
            "local_area_id": null,
            "instance_region_code": "brw"
          },
          "title": null,
          "text": "Test flood report (MIT)"
        }
      }
    ]
  }
}
```

This endpoint retrieves all reports.  Note that all times are UTC, and geometries use the WGS 1984 coordinate system.

#### HTTP Request

`GET /reports`

#### Query Parameters

Parameter | Required | Description | Default | Example |
--------- | ------- | ------------ | ------- | ------- |
city | false | Filter reports by 3-letter city code (see cities endpoint for details). If no city specified then reports for all cities in CogniCity instance are returned | none | brw |
geoformat | false | Specifies either 'geojson' or 'topojson' | topojson | geojson |
timeperiod | false | Time period in seconds to filter reports by, must be strictly between 1 and 604800 (1 week) | 3600 (1 hour) | 3600 | 3600 |

### Archive

```shell
curl "/reports/archive?city=brw&geoformat=geojson&start=2018-06-15T00:00:00-0400&end=2018-06-19T15:00:00-0400"

```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/reports/archive', {
  params: {
    city: 'brw',
    geoformat: 'geojson',
    start: '2018-06-15T00:00:00-0400',
    end: '2017-06-19T15:00:00-0400'
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
          "type": "Point",
          "coordinates": [
            -80.0977993011,
            26.140336808
          ]
        },
        "properties": {
          "pkey": "92",
          "created_at": "2018-06-15T18:48:57.084Z",
          "source": "grasp",
          "status": "confirmed",
          "url": "d56c91dc-15c9-4d3b-83f1-cc86b94ae330",
          "image_url": null,
          "disaster_type": "flood",
          "report_data": {
            "report_type": "flood",
            "flood_depth": 10
          },
          "tags": {
            "district_id": null,
            "local_area_id": "1375",
            "instance_region_code": "brw"
          },
          "title": null,
          "text": "test flood"
        }
      }
    ]
  }
}
```

This endpoint retrieves reports within the specified time period. The maximum duration between start and end times is one week. Note that all times are UTC, and geometries use the WGS 1984 coordinate system.

#### HTTP Request

`GET /reports/archive`

#### Query Parameters

Parameter | Required | Description | Default | Example |
--------- | ------- | ------------ | ------- | ------- |
city | false | Filter reports by 3-letter city code (see cities endpoint for details). If no city specified then reports for all cities in CogniCity instance are returned | none | brw |
geoformat | false | Specifies either 'geojson' or 'topojson' | topojson | geojson |
start | true | Start time for archive period in ISO 8601 string format | none | 2018-06-15T00:00:00-0400
end | true | End time for archive period in ISO 8601 string format. Must bet within 604800 seconds (1 week) from start time | none | 2017-06-19T15:00:00-0400

<aside class="success">
Start and end times require UTC offsets using either '+' or '-' which need to be URL encoded as '%2B' and '%2D' respectively.
</aside>


### Timeseries

```shell
curl "/reports/timeseries?city=brw&start=2018-06-19T13:00:00%2D0400&end=2018-06-19T15:00:00%2D0400"

```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/reports/timeseries', {
  params: {
    start: '2018-06-19T13:00:00-0400',
    end: '2018-06-19T15:00:00-0400'
    }
  })
  .then(response => console.log(response))
  .catch(err => console.log(err))

```


> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "result": [
    {
      "ts": "2018-06-19T17:00:00.000Z",
      "count": "1"
    },
    {
      "ts": "2018-06-19T18:00:00.000Z",
      "count": "0"
    },
    {
      "ts": "2018-06-19T19:00:00.000Z",
      "count": "0"
    }
  ]
}
```

This endpoint generates a time series of reports presented as a count of reports every hour within the specified time period. The maximum duration between start and end times is one week. Report count is recorded alongside an hourly UTC timestamp in ISO 8061 format.

#### HTTP Request

`GET /reports/timeseries`

#### Query Parameters

Parameter | Required | Description | Default | Example |
--------- | ------- | ------------ | ------- | ------- |
city | false | Filter reports by 3-letter city code (see cities endpoint for details). If no city specified then reports for all cities in CogniCity instance are returned | none | jbd |
start | true | Start time for archive period in ISO 8601 string format | none | 2017-02-21T07:00:00+0700
end | true | End time for archive period in ISO 8601 string format. Must bet within 604800 seconds (1 week) from start time | none | 2017-02-21T19:00:00+0700

<aside class="success">
Start and end times require UTC offsets using either '+' or '-' which need to be URL encoded as '%2B' and '%2D' respectively.
</aside>
