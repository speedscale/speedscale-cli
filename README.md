# codename-litespeed

NOTE: This name is just a placeholder.

codename-litespeed is a container-centric, capture and replay CLI tool.

TODO: Insert asciinema video here showing codename-litespeed in action.

## Why use codename-litespeed?

- Visualize inbound / outbound network communication.
- Understand the relationship between an application and its external dependencies.
- Pinpoint slow API endpoints or high latency from a third party service or database.
- Record once with a real database and test continuously without it.
- Load test an application with real traffic.

## Quick Start

NOTE: maybe we want to provide a curl statement here instead.
[Download](link/to/litespeed/latest/dl) the latest verion of codename-litespeed.

Before working with codename-litespeed your application will need to be built into a docker container.

Once built have codename-litespeed record a "snapshot" of your application traffic.

```bash
$ codename-litespeed init
$ codename-litespeed deploy <docker_image_name> # assuming application will serve on port 80
$ codename-litespeed start snapshot
```

Now codename-litespeed is serving your application on port 4143 and recording all requests in and out.
Generate some traffic by making requests. As an example, requests to your order service might look something like this.

```bash
$ curl -X POST http://localhost:4143/orders -d '{"customer_id":"1234", "amount": 123.45}'
{"order_id": 456}
$ curl http://localhost:4143/orders/456
```

Stop the recording.

```bash
$ codename-litespeed stop snapshot
$ codename-litespeed inspect <snapshot_id>
```

To remove codename-litespeed run:

```bash
codename-litespeed destroy && rm -f $(which codename-litespeed)
```

## Help

Having trouble with codename-litespeed, or just want to chat about what Speedscale is building?
Come hang out in the [Speedscale community Slack](https://join.slack.com/t/speedscalecommunity/shared_invite/zt-x5rcrzn4-XHG1QqcHNXIM~4yozRrz8A)!

