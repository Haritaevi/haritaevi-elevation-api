<h2 id="api-endpoints">📡 API Endpoints</h2>

## `GET /api/get_elevation`

Returns the elevation at one or more coordinates.

The GET API is limited to **1024** bytes in the request line. If you plan on making large requests, consider using the POST api.

### Parameters:

- **`country_code`**: Country Code, **`locations`**: List of locations, separated by `|` in `latitude, longitude` format.

### Response format

A JSON object with a single list of results, in the `results` field is returned. Each result contains `latitude`, `longitude`, `elevation`, `country`, `location` and `elevationModel`. The results are in the same order as the request parameters. **Elevation is in meters**.

If there is no recorded elevation at the provided coordinate, sea level (Elevation data not found) is returned.

```json
{
	"results":
	[
		{
			"lat": ...,
			"lng": ...,
			"elevation": ...,
			"country": ...,
			"location": ...,
			"elevationModel": ...
		},
		...
	]
}
```

### Example:

#### Request

```
curl -Method GET `
  -Uri "http://localhost:3004/api/get_elevation?country_code=TR|QA&locations=40.123063,32.998720|39.941192,32.561003|25.267555,51.516953" `
  -Headers @{ "Authorization" = "Bearer YOUR-API-KEY" }
```

#### Response

```json
{
  "results": [
    {
      "lat": 40.8785,
      "lng": 29.2905,
      "elevation": 46,
      "country": "TURKIYE",
      "location": "",
      "elevationModel": "Opentopo NASADEM"
    },
    {
      "lat": 25.276987,
      "lng": 51.520008,
      "elevation": 12,
      "country": "QATAR",
      "location": "",
      "elevationModel": "Opentopo NASADEM"
    },
    {
      "lat": 40.114978,
      "lng": 32.992147,
      "elevation": 951.598510742188,
      "country": "TURKIYE",
      "location": "ESENBOGA AIRPORT",
      "elevationModel": "Lidar"
    }
  ]
}
```

## `POST /api/get_elevation`

Returns the elevation at one or more `(latitude,longitude)` points.

The POST API currently has no limit

### Parameters:

- A JSON (and respective headers) is required with the format:

```json
{
  "apiKey": "...",
  "countryCode": "...",  // Country code (e.g., "TR", "MY", or "W" for auto-detection)
  "locations": [
    { "lat": ..., "lng": ... }
  ]
}

```

### GET Response format

A JSON object with a single list of results, in the `results` field is returned. Each result contains `latitude`, `longitude` and `elevation`. The results are in the same order as the request parameters. **Elevation is in meters**.

If there is no recorded elevation at the provided coordinate, sea level (0 meters) is returned.

```json
{
    "results": [
        {
            "lat": ...,
            "lng": ...,
            "elevation": ...,
            "country": "...",
            "location": ...,
            "elevationModel": ...
        }
    ]
}
```

### Example:

#### Request

```
curl -Method POST `
  -Uri "ttps://elevation.haritaevi.com/api/get_elevation" `
  -Headers @{
    "Content-Type" = "application/json"
    "Authorization" = "Bearer YOUR-API-KEY"
  } `
  -Body '{
    "countryCode": "TR|QA",
    "locations": [
      { "lat": 40.123063, "lng": 32.998720 },
      { "lat": 39.941192, "lng": 32.561003 },
      { "lat": 25.267555, "lng": 51.516953 }
    ]
  }'

```

#### POST Response Format

##### Example Success Response

```json
{
  "results": [
    {
      "lat": 40.123063,
      "lng": 32.99872,
      "elevation": 954.4552001953125,
      "country": "TURKIYE",
      "location": "ESENBOGA AIRPORT",
      "elevationModel": "Lidar"
    },
    {
      "lat": 40.109136,
      "lng": 32.880552,
      "elevation": 1089,
      "country": "TURKIYE",
      "location": "",
      "elevationModel": "Opentopo NASADEM"
    },
    {
      "lat": 39.941192,
      "lng": 32.561003,
      "elevation": 870,
      "country": "TURKIYE",
      "location": "",
      "elevationModel": "Opentopo NASADEM"
    },
    {
      "lat": 25.26755503311803,
      "lng": 51.516953,
      "elevation": 13,
      "country": "QATAR",
      "location": "",
      "elevationModel": "Opentopo NASADEM"
    }
  ]
}
```

##### Missing key:

```json
{ "error": "Your API key is invalid or unauthorized." }
```

##### Invalid coordinates:

```json
{ "error": "Your API key is invalid or unauthorized." }
```
