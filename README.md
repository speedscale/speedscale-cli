<img src="/logo/gold_speedscale_logo_landscape_large.png" width="500">

# speedscale CLI

`speedscale` is a container-centric, capture and replay CLI tool created by [Speedscale](https://speedscale.com).  `speedscale` can wrap
your running application, capturing all inbount and outbount traffic while in use.  Captured traffic can be used to regression test later
versions of your app, or load test by sending the same requests multiple times.

See it in action!
TODO: Insert asciinema video here showing speedscale in action.

## Why use speedscale CLI?

- Visualize inbound / outbound network communication.
- Understand the relationship between an application and its external dependencies.
- Pinpoint slow API endpoints or high latency from a third party service or database.
- Record once with a real database and test continuously without it.
- Load test an application with real traffic.

## Quick Start

Install the latest verion of `speedscale`.

```bash
curl https://raw.githubusercontent.com/speedscale/speedscale/main/install | bash
```

Before working with `speedscale` your application will need to be built into a [docker](https://docs.docker.com/) container.

Once built have `speedscale` run your application and record a "snapshot" of your application traffic.

```bash
$ speedscale init
$ speedscale deploy <docker_image_name> # assuming your application listens on port 80
$ speedscale start snapshot
```

Now `speedscale` is serving your application on port 4143 and recording all requests in and out.
Generate some traffic by making requests. As an example, requests to your order service might look something like this.

```bash
$ curl -X POST http://localhost:4143/orders -d '{"customer_id":"1234", "amount": 123.45}'
{"order_id": 456}
$ curl http://localhost:4143/orders/456
```

Stop the recording.

```bash
$ speedscale stop snapshot
$ speedscale inspect <snapshot_id>
```

To remove `speedscale` run:

```bash
speedscale destroy && rm -f $(which speedscale)
```

## Help

Having trouble with `speedscale`, or just want to chat about what we're building?
Come hang out in the [Speedscale community Slack](https://join.slack.com/t/speedscalecommunity/shared_invite/zt-x5rcrzn4-XHG1QqcHNXIM~4yozRrz8A)!

