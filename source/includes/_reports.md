# Reports

The reports endpoint contains CogniCity reports as GeoJSON or TopoJSON features. Reports are represented by point-geometries and their accompanying properties (e.g. description, time etc.). Note that all times are UTC, and geometries use the WGS 1984 coordinate system.

## Get All Reports

```shell
curl "/reports?city=jbd&geoformat=geojson"

```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/reports', {
  params: {
    city: 'jbd',
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
            106.835474968,
            -6.1795742571
          ]
        },
        "properties": {
          "pkey": "7904",
          "created_at": "2018-03-22T05:07:18.525Z",
          "source": "grasp",
          "status": "confirmed",
          "url": "8dddfd33-d995-4061-863e-57414993aa35",
          "image_url": "https://images-dev.petabencana.id/8dddfd33-d995-4061-863e-57414993aa35.jpg",
          "disaster_type": "flood",
          "report_data": {
            "report_type": "flood",
            "flood_depth": 92
          },
          "tags": {
            "district_id": "3173",
            "local_area_id": "508",
            "instance_region_code": "jbd"
          },
          "title": null,
          "text": "Test flood reporting"
        }
      }
    ]
  }
}
```

This endpoint retrieves all reports.  Note that all times are UTC, and geometries use the WGS 1984 coordinate system.

### HTTP Request

`GET /reports`

### Query Parameters

Parameter | Required | Description | Default | Example |
--------- | ------- | ------------ | ------- | ------- |
city | false | Filter reports by 3-letter city code (see cities endpoint for details). If no city specified then reports for all cities in CogniCity instance are returned | none | jbd |
geoformat | false | Specifies either 'geojson' or 'topojson' | topojson | geojson |
timeperiod | false | Time period in seconds to filter reports by, must be strictly between 1 and 604800 (1 week) | 3600 (1 hour) | 3600 | 3600 |

## Archive


```shell
curl "/reports/archive?start=2017-11-20T00:00:00%2B0700&end=2017-11-22T15:00:00%2B0700"

```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/reports/archive', {
  params: {
    city: 'jbd',
    geoformat: 'geojson',
    start: '2017-11-20T00:00:00+0700',
    end: '2017-11-22T15:00:00+0700'
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
            106.835474968,
            -6.1795742571
          ]
        },
        "properties": {
          "pkey": "7904",
          "created_at": "2018-03-22T05:07:18.525Z",
          "source": "grasp",
          "status": "confirmed",
          "url": "8dddfd33-d995-4061-863e-57414993aa35",
          "image_url": "https://images-dev.petabencana.id/8dddfd33-d995-4061-863e-57414993aa35.jpg",
          "disaster_type": "flood",
          "report_data": {
            "report_type": "flood",
            "flood_depth": 92
          },
          "tags": {
            "district_id": "3173",
            "local_area_id": "508",
            "instance_region_code": "jbd"
          },
          "title": null,
          "text": "Test flood reporting"
        }
      }
    ]
  }
}
```

This endpoint retrieves reports within the specified time period. The maximum duration between start and end times is one week. Note that all times are UTC, and geometries use the WGS 1984 coordinate system.

### HTTP Request

`GET /reports/archive`

### Query Parameters

Parameter | Required | Description | Default | Example |
--------- | ------- | ------------ | ------- | ------- |
city | false | Filter reports by 3-letter city code (see cities endpoint for details). If no city specified then reports for all cities in CogniCity instance are returned | none | jbd |
geoformat | false | Specifies either 'geojson' or 'topojson' | topojson | geojson |
start | true | Start time for archive period in ISO 8601 string format | none | 2017-02-21T07:00:00+0700
end | true | End time for archive period in ISO 8601 string format. Must bet within 604800 seconds (1 week) from start time | none | 2017-02-21T19:00:00+0700

<aside class="success">
Start and end times require UTC offsets using either '+' or '-' which need to be URL encoded as '%2B' and '%2D' respectively.
</aside>


## Timeseries

```shell
curl "/reports/timeseries?start=2017-11-20T00:00:00%2B0700&end=2017-11-22T15:00:00%2B0700"

```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/reports/timeseries', {
  params: {
    start: '2017-11-20T00:00:00+0700',
    end: '2017-11-22T15:00:00+0700'
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
            "ts": "2017-11-19T17:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-19T18:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-19T19:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-19T20:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-19T21:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-19T22:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-19T23:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T00:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T01:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T02:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T03:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T04:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T05:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T06:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T07:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T08:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T09:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T10:00:00.000Z",
            "count": "2"
        },
        {
            "ts": "2017-11-20T11:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T12:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T13:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T14:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T15:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T16:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T17:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T18:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T19:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T20:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T21:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-20T22:00:00.000Z",
            "count": "1"
        },
        {
            "ts": "2017-11-20T23:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T00:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T01:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T02:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T03:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T04:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T05:00:00.000Z",
            "count": "1"
        },
        {
            "ts": "2017-11-21T06:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T07:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T08:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T09:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T10:00:00.000Z",
            "count": "7"
        },
        {
            "ts": "2017-11-21T11:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T12:00:00.000Z",
            "count": "1"
        },
        {
            "ts": "2017-11-21T13:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T14:00:00.000Z",
            "count": "1"
        },
        {
            "ts": "2017-11-21T15:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T16:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T17:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T18:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T19:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T20:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T21:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T22:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-21T23:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-22T00:00:00.000Z",
            "count": "1"
        },
        {
            "ts": "2017-11-22T01:00:00.000Z",
            "count": "5"
        },
        {
            "ts": "2017-11-22T02:00:00.000Z",
            "count": "1"
        },
        {
            "ts": "2017-11-22T03:00:00.000Z",
            "count": "1"
        },
        {
            "ts": "2017-11-22T04:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-22T05:00:00.000Z",
            "count": "0"
        },
        {
            "ts": "2017-11-22T06:00:00.000Z",
            "count": "1"
        },
        {
            "ts": "2017-11-22T07:00:00.000Z",
            "count": "2"
        },
        {
            "ts": "2017-11-22T08:00:00.000Z",
            "count": "1"
        }
    ]
}

```

This endpoint generates a time series of reports presented as a count of reports every hour within the specified time period. The maximum duration between start and end times is one week. Report count is recorded alongside an hourly UTC timestamp in ISO 8061 format.

### HTTP Request

`GET /reports/timeseries`

### Query Parameters

Parameter | Required | Description | Default | Example |
--------- | ------- | ------------ | ------- | ------- |
city | false | Filter reports by 3-letter city code (see cities endpoint for details). If no city specified then reports for all cities in CogniCity instance are returned | none | jbd |
start | true | Start time for archive period in ISO 8601 string format | none | 2017-02-21T07:00:00+0700
end | true | End time for archive period in ISO 8601 string format. Must bet within 604800 seconds (1 week) from start time | none | 2017-02-21T19:00:00+0700

<aside class="success">
Start and end times require UTC offsets using either '+' or '-' which need to be URL encoded as '%2B' and '%2D' respectively.
</aside>