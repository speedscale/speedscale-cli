<img src="https://raw.githubusercontent.com/speedscale/assets/main/logo/gold_speedscale_logo_landscape_large.png" width="500">

# speedscale CLI

`speedscale` is a container-centric, capture and replay CLI tool created by [Speedscale](https://speedscale.com).
`speedscale` wraps your running application, capturing all inbound and outbound traffic while in use.  View all calls going into and out of your application in a slick text UI. Higher level details are shown for various protocols including gRPC, Postgres and others.

- Visualize inbound / outbound network communication
- Understand the relationship between an application and its external dependencies
- Pinpoint slow API endpoints or high latency from a third party service or database

As engineers, we want to understand the inner workings of our applications, and others, but it's often difficult to get the full picture from the outside.  Clients like `cURL` and Postman can give us external request / response data but fall short of capturing requests made from the application itself.  Also getting from code to a working curl command can be tedious.  `speedscale` is able to gain greater insight by running your application inside a docker container and intercepting all of the requests going in and out.  `speedscale` does more while providing a contextual view of your application traffic.

When a request is made to your application `speedscale` records the raw request / response data, along with metadata like request latency, encoding, detected technologies, etc.  This allows you to get to the specific bits of your network requests, but at a higher level than looking at packets and TCP streams in Wireshark.

# Getting Started

As you get started, come chat with us in the [Speedscale Community Slack](https://slack.speedscale.com)!

Download the latest version of speedscale, which will update the binary in your ~/.speedscale directory.
```
sh "$(curl -sL https://downloads.speedscale.com/speedscale-cli/install)"
```
Initialize speedscale and answer the questions that follow.
```
speedscale init
```
Now try one of the [guides](https://cli.speedscale.com/cli/local-observability/python-demo-app).

## Docker
`speedscale` does require access to the Docker socket to run and may create or delete docker resources.  Running `speedscale stop capture` should clean up docker resources but take a look at `docker ps --all` to list any remaining containers.

## Data Directory
By default, `speedscale`uses the $HOME/.speedscale directory to store configuration, binaries, data, etc.  Removing this directory will remove all Speedscale related files.  Be careful with this operation if you plan to continue to interact with speedscale or speedctl.

# Troubleshooting
Explore the available commands available by running `speedscale --help` or add `--help` to the end of any command for details on that command.
If you see something like `command not found: speedscale` then ensure the speedscale directory `(~/.speedscale)` has been added to your `$PATH`.
Still have questions? Join our [Speedscale Community Slack](https://slack.speedscale.com)!

# Docs
`speedscale` documentation can be found in our [public docs](https://cli.speedscale.com/)

[Container Mode](https://cli.speedscale.com/cli/introduction#supported-architectures)

[Proxy Mode](https://cli.speedscale.com/cli/introduction#supported-architectures)

[Explore Sample Data](https://cli.speedscale.com/cli/explore-sample-data)

[Python Demo App](https://cli.speedscale.com/cli/local-observability/python-demo-app)

[Docker Demo App](https://cli.speedscale.com/cli/docker-observability/demo-app)


Please also join us for a webinar where we go over why we built the CLI, use cases where we envisioned it to help, how-to and general opportunity to ask any questions you like!  [Register here](https://us02web.zoom.us/webinar/register/WN_SBGvlHAFS0GoKFqkEBsoXw) and attend January 12th, 2022, 2pm EST.

***

<img src="https://user-images.githubusercontent.com/29799065/148107570-4fde70d1-d2aa-40d4-8b71-bf7ba2bc8107.gif" width="800">

Inspect request/response transactions
<img src="/assets/screenshot-1.png" width=900>

Visualize dependencies of your API
<img src="/assets/screenshot-2.png" width=900>

# Help and Feedback

If you are having trouble with `speedscale` or would like to report a bug, please feel free to
[submit an issue](https://github.com/speedscale/speedscale-cli/issues/new/choose).

Interested in talking to us about this or other things we are building? Come hang out in the
[Speedscale community Slack](https://slack.speedscale.com)!

We appreciate any and all feedback, good or bad, that can help us make `speedscale` better for you.
