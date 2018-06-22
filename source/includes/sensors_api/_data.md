## Sensor Data

### GET /:id

```shell
curl "/3"
```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/3')
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured like this:

```json
{
  "statusCode": 200,
  "result": [
    {
      "dataId": "24439",
      "sensorId": "3",
      "created": "2018-03-16T17:37:47.116Z",
      "properties": {
        "type": "observation",
        "observations": [
          {
            "value": "3.84",
            "dateTime": "2018-03-15T13:45:00.000-04:00"
          },
          {
            "value": "3.84",
            "dateTime": "2018-03-15T14:00:00.000-04:00"
          }
        ]
      }
    }
  ]
}
```

This endpoint retrieves a list of data for a specific sensor. Data are organised into records, indexed by the `id` attribute. The `created` attribute details when the record was last updated. The `properties` attribute contains the data for the record. The `properties` object may be in varying formats. The example shows a `properties` object for a single data record which contains an `observations` array of measurements. Data records are returned in reverse chronological order by `created` date.

<aside class="warn">
When a sensor does not have any data associated with it the endpoint will return a 404 error "No data found for sensor [ID]".
</aside>


#### HTTP Request

`GET /:id`

#### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the sensor to retrieve
type | Optional filter for the type field
limit | Optional limit on number of returned records

#### Response
Attribute | Type | Description |
--------- | --------- | ----------- |
dataId | integer | Unique data record identifier |
sensorId | integer | The ID of the sensor |
created | string | Data record update time (ISO 8601 format) |
properties | object | Record data |

### POST /:id

```shell
curl -X POST /4 -H 'Content-Type: application/json' -H 'x-api-key: key' -d '{
	"properties":{
		"METAR": "CYYQ 182200Z 07002KT 15SM OVC017 06/03 A2966 RMK SC10 3 POLAR BEARS ALNG RNWY==",
    "type": "observation"
  }
}'

```

```javascript
import axios from 'axios'; // package to make http requests

axios.post('/4', {
    properties: {
      METAR: "CYYQ 182200Z 07002KT 15SM OVC017 06/03 A2966 RMK SC10 3 POLAR BEARS ALNG RNWY==",
      type: "observation"
    },
  }, {headers: {'x-api-key': 'key'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))

```

> The above command returns JSON structured like this:

```json
{
    "statusCode": 200,
    "result": {
            "dataId": "240288",
            "sensorId": "4",
            "created": "2018-03-16T19:30:33.042Z"
    }
}
```

This endpoint adds a new data record to the specified sensor. On success the sensor ID and an updated timestamp are returned.

<aside class="success">
This request requires an API key for authorization using the `x-api-key` header.
</aside>

#### HTTP Request

`POST /:id`

#### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the sensor

#### New Sensor Attributes

Attribute | Type | Description | Required
--------- | ---- | ----------- | --------
properties | object | New data record to be added | Yes
properties.type | string | Optional type tag for different measurement types (e.g. observation vs manual, or mean vs daily max)

### DELETE /:id/:dataId

```sh
curl -X DELETE /4/2345 -H 'Content-Type: application/json' -H 'x-api-key: key'

```

```javascript
import axios from 'axios'; // http requests
// delete record 2345 from sensor 4
axios.delete('/sensors/4/2345', {headers: {'x-api-key': 'key'}, {'content-type': 'application/json'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

```json
{
    "statusCode": 200,
    "body": {}
}
```
This endpoint deletes a data record for the specified sensor. On success the statusCode and an empty body object are returned.

<aside class="success">
This request requires an API key for authorization using the `x-api-key` header.
</aside>

#### HTTP Request

`DELETE /:id/:dataId`

#### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the sensor
DATAID | The ID of the data record to delete


