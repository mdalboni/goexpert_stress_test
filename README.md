# GoExpert Stress Test Challenge

Simple Stress Test tool for HTTP requests.

## Options

Available options are:
- `url`*: URL to send requests;
- `requests`: Number of requests to send;
- `concurrency`: Number of concurrent requests;
- `method`: HTTP method to use;

\* Are required parameters

## Usage

### Local run
To run the application use the following command:
```shell
go run cmd/stress_test/main.go -url=<url> -requests=<requests> -concurrency=<workers>
```

### Docker run
To build and run the image execute:
```shell
docker build -t go-stress-test .
docker run go-stress-test --url=<url> --requests=<requests> --concurrency=<workers>
```

## Example API
For testing purposes an Example API was developed at `cmd/mock_server`.

This server will return randomly one of the following status codes with a
random delay between 0 and 2 seconds:
- 500: Internal Server Error;
- 503: Service Unavailable;
- 404: Not Found;
- 401: Unauthorized;
- 200: OK;

To run the server execute:
```shell
go run cmd/mock_server/main.go
```

To run the stress tests against the server execute:
```shell
go run cmd/stress_test/main.go -url=http://localhost:8080 -requests=100 -concurrency=20
```

Example output of the stress test against the Example API:
```
Configuration:
- Concurrency: 20
- Requests: 100
- Timeout: 5s
- Method: GET
- URL: http://localhost:8080

Results:
- 404: 16/100 (16%)
- 200: 18/100 (18%)
- 503: 25/100 (25%)
- 401: 19/100 (19%)
- 500: 22/100 (22%)
Total tasks executed: 100

Total time: 5.02s
```

## Testing

To execute all the unit tests run 
```shell
go test ./...
```
