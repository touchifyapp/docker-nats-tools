# Supported tags and respective Dockerfile links

*  [`0.1.0`, `0.1`, `latest` (Dockerfile)](https://github.com/touchifyapp/docker-nats-tools/blob/master/Dockerfile)

This image is updated via [pull requests to the `touchifyapp/docker-nats-tools` GitHub repo](https://github.com/touchifyapp/docker-nats-tools/pulls).

# Tools for [NATS](http://nats.io): A high-performance cloud native messaging system.

![NATS logo](https://raw.githubusercontent.com/docker-library/docs/45d33e1726fed03a2a40363a9699e0587e713c55/nats/logo.png)

`nats` is a high performance server for the NATS Messaging System.

## Tools included

 * [`nats`](https://github.com/soutenniza/nats): Go CLI Application that combines nats sub and pub.
 * [`nats-top`](https://github.com/nats-io/nats-top): Top like program monitor for NATS.

## How to use

### As a simple container

```
# Run NATS tools
$ docker run -it --name nats-tools --link nats-server touchify/nats-tools

# Use nats-cli
nats-tools:/# nats sub -s nats://nats-server:4222 topic &
nats-tools:/# nats pub -s nats://nats-server:4222 topic message

# Use nats-top
nats-tools:/# nats-top -s nats://nats-server:4222
```

### As a Docker 1.12 service cluster

```
# Run a NATS subscriber.

$ docker service create \
$     --name nats-subscriber \
$     --network nats-network \
$     --replicas 3 \
$     touchify/nats-tools \
$     nats sub -s nats://nats-server:4222 topic

# Run a NATS publisher.

$ docker service create \
$     --name nats-publisher \
$     --network nats-network \
$     --replicas 3 \
$     touchify/nats-tools \
$     I=0; while true; do I=$(expr $I + 1); nats public -s nats://nats-server:4222 topic "message$I"; sleep 1; done

# Run NATS top.

$ docker service create \
$     --name nats-publisher \
$     --network nats-network \
$     --replicas 3 \
$     touchify/nats-tools \
$     nats-top -s nats://nats-server:4222 topic
```

## License

View [license information](https://github.com/touchifyapp/docker-nats-tools/blob/master/LICENSE) for the software contained in this image.

## Supported Docker versions

This image is officially supported on Docker version 1.12+.

Please see [the Docker installation documentation](https://docs.docker.com/installation/) for details on how to upgrade your Docker daemon.

## User Feedback

### Documentation

Documentation for this image is stored in [the `touchifyapp/docker-nats-tools` GitHub repo](https://github.com/touchifyapp/docker-nats-tools).
Be sure to familiarize yourself with the repository's README.md file before attempting a pull request.

### Issues

If you have any problems with or questions about this image, please contact us through a [GitHub issue](https://github.com/touchifyapp/docker-nats-tools/issues).

### Contributing

You are invited to contribute new features, fixes, or updates, large or small; we are always thrilled to receive pull requests, and do our best to process them as fast as we can.

Before you start to code, we recommend discussing your plans through a [GitHub issue](https://github.com/touchifyapp/docker-nats-tools/issues), especially for more ambitious contributions. This gives other contributors a chance to point you in the right direction, give you feedback on your design, and help you find out if someone else is working on the same thing.
