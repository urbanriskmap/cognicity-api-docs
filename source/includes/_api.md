
# API Responses

> Response structure:

```json
{
  "statusCode": { Number },
  "result": { Object | Array }
}
```

CogniCity provides responses in JSON format. The `statusCode` object gives the HTTP response status for the request (also available in the response header). The `response` property may be either an `Object` or an `Array` depending on the data returned.

The `/floods` endpoint also supports responses using the Common Alerting Protocol, an XML format.

CogniCity uses the [PostgreSQL BIGINT](https://www.postgresql.org/docs/current/static/datatype-numeric.html) data type. As these numbers are potentially greater than `Numbers.MAX_SAFE_INTEGER` they are returned as Strings.
