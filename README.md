<img src="https://raw.githubusercontent.com/speedscale/assets/main/logo/gold_speedscale_logo_landscape_large.png" width="500">

# speedscale CLI

`speedscale` is a container-centric, capture and replay CLI tool created by [Speedscale](https://speedscale.com).
`speedscale` wraps your running application, capturing all inbound and outbound traffic while in use.  Catputed traffic
is inspected to show data going to and from your application, with higher level details for various protocols.

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
curl -sL https://downloads.speedscale.com/speedscale-cli/install | sh
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

- [I don't want to capture, just let me play with some data](#inspect-prerecorded-snapshot)
- [I want batteries included, start with a demo app](#demo-app)
- [I have an containerized applicaton, show me my traffic](#capture-my-application)

### Inspect Prerecorded Snapshot

Just run the demo command to play with a prerecorded snapshot.

```bash
speedscale inspect demo
```

### Demo App

We'll use an echo server to play with some traffic capture.  The echo server responds with whatever we send it.
The echo server listens on port 80, which will be redirected to localhost port 8080.

```bash
speedscale start capture --image mendhak/http-https-echo --port 8080:80
```

Make some requests to the echo server on the local port.  We expect the response body to match the request body that we're sending.

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

Now [inspect](#screenshots) the snapshot you just created.

```
speedscale inspect
```

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

Now [inspect](#screenshots) the snapshot you just created.

```bash
speedscale inspect
```

# Screenshots

Inspect requests:

<img src="/assets/screenshot-1.png" width=900>

Visualize network dependencies:

<img src="/assets/screenshot-2.png" width=900>

## Help and Feedback

Having trouble with `speedscale`, or just want to chat about what we're building?
Come hang out in the [Speedscale community Slack](https://join.slack.com/t/speedscalecommunity/shared_invite/zt-x5rcrzn4-XHG1QqcHNXIM~4yozRrz8A)!
We appreciate any feedback, good or bad, that can help us make `speedscale` better for you.

Speedscale docs available at [docs.speedscale.com](https://docs.speedscale.com).

