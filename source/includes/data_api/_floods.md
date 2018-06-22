## Floods

The floods endpoint provides flood hazard seveirty by local area. This information is created through the CogniCity Risk Evaluation Matrix, and is nowt operational in all cities. Local areas are delineated by available local boundary data (e.g. Fire grids in the US, or RW districts in Indonesia).

In addition to topojson and geojson support the floods endpoint supports the Common Alerting Protocol (CAP).

<aside class="notice">
Flood states in the CAP format have a default expiry time of 6 hours from the time that the API request is made.
</aside>

**Flood State Codes**

Flood state by area is represneted by numberic code, as follows:

| Code | Severity | Description
| ---- | -------- | -----------
1 | Unknown | AN UNKNOWN LEVEL OF FLOODING - USE CAUTION
2 | Minor | FLOODING OF BETWEEN 10 AND 70 CENTIMETERS
3 | Moderate | FLOODING OF BETWEEN 71 and 150 CENTIMETERS
4 | Severe | FLOODING OF OVER 150 CENTIMETERS

### GET /floods

This endpoint gets flood hazard information by local area.

```shell
curl /floods
```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/floods')
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above commands returns JSON structured as follows (example taken from petabencana.id for Jakarta).

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
            "type": "Polygon",
            "properties": {
              "area_id": "5",
              "geom_id": "3174040004009000",
              "area_name": "RW 09",
              "parent_name": "GROGOL",
              "city_name": "Jakarta",
              "state": 1,
              "last_updated": "2016-12-19T13:53:52.274Z"
            },
            "arcs": [
              [
                0
              ]
            ]
          }
        ]
      }
    },
    "arcs": [
      [
        [
          9999,
          7847
        ],
        [
          -507,
          -6
        ],
        [
          -695,
          -70
        ],
        [
          -317,
          -221
        ],
        [
          -761,
          -18
        ],
        [
          -516,
          98
        ],
        [
          -641,
          -61
        ],
        [
          -649,
          -119
        ],
        [
          -169,
          -762
        ],
        [
          -181,
          -519
        ],
        [
          48,
          -602
        ],
        [
          -130,
          -162
        ],
        [
          64,
          -1235
        ],
        [
          81,
          -2351
        ],
        [
          136,
          -1098
        ],
        [
          15,
          -675
        ],
        [
          -1250,
          -40
        ],
        [
          -879,
          -6
        ],
        [
          -924,
          217
        ],
        [
          -924,
          425
        ],
        [
          -1800,
          138
        ],
        [
          830,
          1540
        ],
        [
          565,
          1455
        ],
        [
          764,
          1975
        ],
        [
          1018,
          2079
        ],
        [
          384,
          788
        ],
        [
          389,
          1061
        ],
        [
          1398,
          -76
        ],
        [
          296,
          -25
        ],
        [
          360,
          6
        ],
        [
          392,
          -9
        ],
        [
          360,
          -9
        ],
        [
          377,
          12
        ],
        [
          323,
          25
        ],
        [
          354,
          76
        ],
        [
          296,
          89
        ],
        [
          211,
          42
        ],
        [
          290,
          52
        ],
        [
          217,
          28
        ],
        [
          341,
          110
        ],
        [
          43,
          -67
        ],
        [
          57,
          -174
        ],
        [
          109,
          -159
        ],
        [
          154,
          -257
        ],
        [
          115,
          -370
        ],
        [
          99,
          -346
        ],
        [
          124,
          -357
        ],
        [
          133,
          -422
        ]
      ]
    ],
    "transform": {
      "scale": [
        0.0000003311331833192323,
        0.00000032713269326930546
      ],
      "translate": [
        106.7917869997,
        -6.158925
      ]
    },
    "bbox": [
      106.7917869997,
      -6.158925,
      106.7950980004,
      -6.1556540002
    ]
  }
}
```

> Data example when requested in CAP XML format.

```xml
<?xml version="1.0"?>
<feed xmlns="http://www.w3.org/2005/Atom">
    <id>https://data.petabencana.id/floods</id>
    <title>petabencana.id Flood Affected Areas</title>
    <updated>2016-12-19T23:08:52+07:00</updated>
    <author>
        <name>petabencana.id</name>
        <uri>https://petabencana.id/</uri>
    </author>
    <entry>
        <id>https://data.petabencana.id/floods?parent_name=GROGOL&amp;area_name=RW%2009&amp;time=2016-12-19T22:41:35+07:00</id>
        <title>GROGOL.RW_09.2016-12-19T22:41:35+07:00 Flood Affected Area</title>
        <updated>2016-12-19T22:41:35+07:00</updated>
        <content type="text/xml">
            <alert xmlns="urn:oasis:names:tc:emergency:cap:1.2">
                <identifier>GROGOL.RW_09.2016-12-19T22:41:35+07:00</identifier>
                <sender>BPBD.JAKARTA.GOV.ID</sender>
                <sent>2016-12-19T22:41:35+07:00</sent>
                <status>Actual</status>
                <msgType>Alert</msgType>
                <scope>Public</scope>
                <info>
                    <category>Met</category>
                    <event>FLOODING</event>
                    <urgency>Immediate</urgency>
                    <severity>Minor</severity>
                    <certainty>Observed</certainty>
                    <senderName>JAKARTA EMERGENCY MANAGEMENT AGENCY</senderName>
                    <headline>FLOOD WARNING</headline>
                    <description>AT 22:41 WIB THE JAKARTA EMERGENCY MANAGEMENT AGENCY OBSERVED FLOODING OF BETWEEN 10 and 70 CENTIMETERS IN GROGOL, RW 09.</description>
                    <web>https://petabencana.id/</web>
                    <area>
                        <areaDesc>RW 09, GROGOL</areaDesc>
                        <polygon>-6.1563580003,106.7950980004 -6.1563600004,106.7949299998 -6.1563829997,106.7947 -6.1564550003,106.7945949997 -6.1564609997,106.7943429997 -6.156429,106.7941719999 -6.156449,106.7939600001 -6.156488,106.793745 -6.1567369998,106.7936890001 -6.1569070004,106.7936290001 -6.1571040005,106.7936449999 -6.1571570003,106.7936019997 -6.157561,106.7936229998 -6.1583300004,106.7936500001 -6.1586889999,106.7936950004 -6.1589100002,106.7936999998 -6.1589229999,106.7932860005 -6.158925,106.7929949996 -6.1588540003,106.7926889999 -6.1587150002,106.7923830002 -6.1586699999,106.7917869997 -6.158166,106.7920619998 -6.1576899997,106.7922490003 -6.1570440005,106.7925020003 -6.1563639997,106.7928389996 -6.1561060004,106.7929660001 -6.1557589997,106.7930949997 -6.1557839999,106.7935580004 -6.1557920003,106.7936560004 -6.1557900002,106.7937749996 -6.1557930003,106.7939050002 -6.1557960005,106.7940240003 -6.1557920003,106.7941489998 -6.1557839999,106.7942560002 -6.1557589997,106.7943730002 -6.1557300001,106.7944710002 -6.1557160004,106.7945409999 -6.1556990005,106.7946369998 -6.1556900001,106.7947090004 -6.1556540002,106.7948220002 -6.1556760003,106.794836 -6.1557330003,106.794855 -6.155785,106.7948909998 -6.1558690002,106.7949420004 -6.1559900004,106.7949800003 -6.1561030002,106.7950130001 -6.1562200002,106.7950540001 -6.1563580003,106.7950980004 </polygon>
                    </area>
                </info>
            </alert>
        </content>
    </entry>
</feed>
```

#### HTTP Request
`GET /floods`

#### Request Parameters
Attribute | Type | Description | Required | Default |
--------- | ---- | ----------- | -------- | ------- |
city | string | Which city do we want data for (e.g. 'jbd')? | No | None
format | string | Format to return data in (one of 'json', 'xml') | No | json 
geoformat | string | What format should geographic result use (one of 'topojson', 'geojson', 'cap') | No | topojson
minimum_state | number | The minimum flood state that should be returned (min: 1, max: 4) | No | None

### GET /floods/states

Get flooded areas without geospatial boundary data. Areas are referenced by `area_id` property. This is useful for updating state without the overhead of requesting the complete geographic data-set.

Example lists flooded areas in Jakarta with a state of 1 of higher.

```shell
curl /floods/states?minimum_state=1&city=jbd
```

```javascript
import axios from 'axios'; // package to make http requests

axios.get('/floods/states?minimum_state=1&city=jbd')
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured as shown below.

```json
{
  "statusCode": 200,
  "result": [
    {
      "area_id": "5",
      "state": 1,
      "last_updated": "2016-12-19T13:53:52.274Z"
    }
  ]
}
```

#### Request Parameters
Attribute | Type | Description | Required | Default |
--------- | ---- | ----------- | -------- | ------- |
city | string | Which city do we want data for (e.g. 'jbd')? | No | None
minimum_state | number | The minimum flood state that should be returned (min: 1, max: 4) | No | None

#### HTTP Request
`GET /floods/states?minimum_state=1&city=jbd`

### PUT /floods/:id

This endpoint receives new flood state information for a given local area.

```shell
curl -X PUT /floods/:id
    -H 'Content-Type: application/json'
    -H 'Authorization': 'token',
    -d '{
        "state": 2
    }'
```

```javascript
import axios from 'axios'; // package to make http requests

axios.put('/floods/:id', {
    state: 2
  }, {headers: {'Authorization': 'token'}})
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured like this:

```json
{
    "localAreaId": "<id>",
    "state": 2,
    "updated": true
}
```

#### HTTP Request
`PUT /floods/:id`

#### Flood State Attributes
Attribute | Type | Description | Required |
--------- | ---- | ----------- | -------- |
state | number | Flood severity | Yes 

<aside class="success">
This endpoint requires authorization in the form of a JSON web token.
</aside>

### DELETE /floods/:id

This endpoint clears the flood state for a given local area.

```shell
curl -X DELETE /floods/:id
```

```javascript
import axios from 'axios'; // package to make http requests

axios.delete('/floods/:id/')
  .then(response => console.log(response))
  .catch(err => console.log(err))
```

> The above command returns JSON structured as show below.

```json
{
  "localAreaId": "<id>",
  "state": null,
  "updated": true
}
```

#### HTTP Request
`DELETE /floods/:id`

<aside class="success">
This endpoint requires authorization in the form of a JSON web token.
</aside>