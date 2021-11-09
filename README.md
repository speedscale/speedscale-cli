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

### Demo App



Before working with `speedscale` your application must be built into a [docker](https://docs.docker.com/) container.  Once built,
have `speedscale` run your application and record a "snapshot" of your application traffic.

```bash
speedscale start capture --image $DOCKER_IMAGE # assuming your application listens on port 80
```
```bash
speedscale start snapshot
```

Now `speedscale` is serving your application on port 4143 and recording all requests in and out.
Generate some traffic by making requests. As an example, requests to your order service might look something like this.

```bash
curl -X POST http://localhost:4143/orders -d '{"customer_id":"1234", "amount": 123.45}'
{"order_id": 456}
curl http://localhost:4143/orders/456
```

Stop the recording.

```bash
speedscale stop snapshot
```
```bash
speedscale inspect <snapshot_id>
```

With a snapshot created you can inspect the requests made or run a replay.  See `speedscale help` for details.

Inspect requests:

<img src="/assets/screenshot-1.png" width=900>

Visualize network dependencies:

<img src="/assets/screenshot-2.png" width=900>

## Help and Feedback

Having trouble with `speedscale`, or just want to chat about what we're building?
Come hang out in the [Speedscale community Slack](https://join.slack.com/t/speedscalecommunity/shared_invite/zt-x5rcrzn4-XHG1QqcHNXIM~4yozRrz8A)!
We appreciate any feedback, good or bad, that can help us make `speedscale` better for you.

Speedscale docs available at [docs.speedscale.com](https://docs.speedscale.com).

