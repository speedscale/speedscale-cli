<img src="https://raw.githubusercontent.com/speedscale/assets/main/logo/gold_speedscale_logo_landscape_large.png" width="500">

# speedscale CLI

`speedscale` is a container-centric, capture and replay CLI tool created by [Speedscale](https://speedscale.com), as well
as the public API to the Speedscale cloud.  `speedscale` wraps your running application, capturing all inbound and outbound
traffic while in use.  Captured traffic is used to regression test later versions of your app, or load test by sending the same requests multiple times.

[![asciicast](https://asciinema.org/a/448099.svg)](https://asciinema.org/a/448099)

## Why use speedscale CLI?

- Visualize inbound / outbound network communication
- Understand the relationship between an application and its external dependencies
- Pinpoint slow API endpoints or high latency from a third party service or database
- Record once with a real database and test continuously without it
- Load test an application with real traffic

## Install

Install the latest verion of `speedscale`.

```bash
curl -sL https://downloads.speedscale.com/speedscale/install | sh
```

Need to remove `speedscale`?

```bash
speedscale stop capture; rm -f $(which speedscale)
```

## Getting Started

Quickly setup the default config.

```bash
speedscale init
```

Now try one of these flows to get a feel for the tool.

- [I want batteries included, start with a demo app](#demo-app)
- [I don't want to capture, just let me see what the results look like](#inspect-prerecorded-snapshot)
- [I have a container ready to go]()

### Demo App

We'll use an echo server to play with some traffic capture.  The echo server responds with whatever we send it.
The application port 80 will be redirected to localhost port 8080.

```bash
speedscale start capture --image mendhak/http-https-echo --port 8080:80
```

Make some requests to the echo server.  We expect the server to respond with the same body that we send.

```bash
curl http://localhost:8080/ping
curl -X POST http://localhost:8080/customer --data '{
  "id": 23456,
  "first_name": "Barry",
  "last_name": "Allen",
}'
curl -X POST http://localhost:8080/order --data '{
  "id": 12345,
  "customer_id": 23456,
  "product": "sandwich",
  "count": 2
}'
```

Stop the capture and process the requests.

```bash
speedscale stop capture
```

Inspect the snapshot you just created.

```
speedscale inspect latest
```

### Inspect Prerecorded Snapshot


### Capture My Application

This guide assumes your application is already built into a [docker](https://docs.docker.com/) container.
`speedscale` will run your application and record a "snapshot" of your application traffic.  Set your application details accordingly.

Let's run your application.  This assumes your app is listening on port 80.

```bash
speedscale start capture --image $YOUR_DOCKER_IMAGE --port 8080:80
```

Now `speedscale` is serving your application on localhost port 8080 and recording all requests in and out.
Generate some traffic by making requests. As an example, requests to your order service might look something like this.

```bash
curl -X POST http://localhost:4143/orders -d '{"customer_id":"1234", "amount": 123.45}'
{"order_id": 456}
curl http://localhost:4143/orders/456
```

Make as many requests as you like and then stop the recording.

```bash
speedscale stop snapshot
```

The snapshot is finalized, let's inspect it.

```bash
speedscale inspect $SNAPSHOT_ID
```

Inspect requests:

<img src="/assets/screenshot-1.png" width=900>

Visualize network dependencies:

<img src="/assets/screenshot-2.png" width=900>

## Help and Feedback

Having trouble with `speedscale`, or just want to chat about what we're building?
Come hang out in the [Speedscale community Slack](https://join.slack.com/t/speedscalecommunity/shared_invite/zt-x5rcrzn4-XHG1QqcHNXIM~4yozRrz8A)!
We appreciate any feedback, good or bad, that can help us make `speedscale` better for you.

Speedscale docs available at [docs.speedscale.com](https://docs.speedscale.com).

