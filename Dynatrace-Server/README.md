![Docker Logo](https://github.com/Dynatrace/Dynatrace-Docker/blob/images/docker-logo.png)

# Dynatrace-Server

This project contains files for building and running the Dynatrace Server component of the [Dynatrace Application Monitoring](http://www.dynatrace.com/docker) enterprise solution for deep end-to-end application monitoring in Docker. Ready-made images are available on the [Docker Hub](https://hub.docker.com/r/dynatrace/server/).

**Note**: the `dynatrace/server` image has been designed to run in low-traffic, resource-constrained **demo and trial environments**. Dynatrace does not support its use in production or pre-production grade environments of any kind.


## Run a container via `docker-compose.yml`

[Docker Compose](https://docs.docker.com/compose/) is a tool for defining and running multi-container applications, where an application's services are configured in `docker-compose.yml` files. Typically, you would run an application via `docker-compose [-f docker-compose.yml] up`.


### Configuration

Configuration relies on supplying docker-compose with environment variables defined in .env file. Some variables need to be passed to Dockerfile via ARG for correct building an Server image, that's way it is recommended to change variables only in .env file.


| Environment Variable  | Defaults                    | Description
|:----------------------|:------------------------------------------------|:-----------
| COMPOSE_PROJECT_NAME  | "dynatracedocker"           | A name of the Project. Also used for network naming.
| DT_HOME               | "/opt/dynatrace"            | Path to dynatrace installation directory
| DT_SERVER_NAME        | "dtserver"                  | A name that applies to both the server and the container instance.
| DT_SERVER_LICENSE_KEY_FILE_URL     | N/A            | A URL to a Dynatrace License Key file (optional). If the variable remains unset, a license key has to be provided through the Dynatrace Client.
| VERSION               | "7.0"                       | GA version
| BUILD_VERSION         | "7.0.0.2469"                | Build version

Ports are also defined in .env file based on current [Communication Connections](https://community.dynatrace.com/community/display/DOCDT65/Set+up+Communication+Connections)

List of used ports for server:
```
APPMON_WEB_CLIENT_NONSSL_PORT=8020
APPMON_WEB_CLIENT_SSL_PORT=8021
APPMON_ONEAGENT_NONSSL_SERVER_PORT=8040
APPMON_ONEAGENT_SSL_SERVER_PORT=8041
APPMON_CLIENT_NONSSL_PORT=2021
APPMON_CLIENT_SSL_PORT=8023
APPMON_COLLECTOR_PORT=9998
APPMON_COLLECTOR_SERVER_SSL_PORT=6699
```

## Run a container

[Docker Compose](https://docs.docker.com/compose/) is a tool for defining and running multi-container applications, where an application's services are configured in `docker-compose.yml` files. Typically, you would run an application via `docker-compose [-f docker-compose.yml] up`.


Depending on what base image you want (slim alpine or bigger debian) you can switch it in docker-compose.yml file by changing the value for `dockerfile` attribute, e.g:

```
dockerfile: Dockerfile-debian
```

### Examples

Creates a Dockerized Dynatrace Server instance named `dtserver`:

```
docker-compose up
```

### Licensing

The examples above leave your Dynatrace environment without a proper license. However, you can conveniently have a license provisioned at container runtime by specifying a URL to a [Dynatrace License Key File](http://bit.ly/dttrial-docker-github) in the `DT_SERVER_LICENSE_KEY_FILE_URL` environment variable. If you don't happen to have a web server available to serve the license file to you, [Netcat](https://en.wikipedia.org/wiki/Netcat) can conveniently serve it from your command line, exactly once, via `nc -l 1337 < dtlicense.key`, where `1337` is an available port on your local machine. A `sudo` may be required depending on which port you eventually decide to choose.



## Dockerized Dynatrace Components

See the following Dockerized Dynatrace components and examples for more information:

- [Dockerized Dynatrace Agent](https://github.com/Dynatrace/Dynatrace-Docker/tree/master/Dynatrace-Agent) and [Examples](https://github.com/Dynatrace/Dynatrace-Docker/tree/master/Dynatrace-Agent-Examples)
- [Dockerized Dynatrace Collector](https://github.com/Dynatrace/Dynatrace-Docker/tree/master/Dynatrace-Collector)
- [Dockerized Dynatrace Server](https://github.com/Dynatrace/Dynatrace-Docker/tree/master/Dynatrace-Server)

## Problems? Questions? Suggestions?

This offering is [Dynatrace Community Supported](https://community.dynatrace.com/community/display/DL/Support+Levels#SupportLevels-Communitysupported/NotSupportedbyDynatrace(providedbyacommunitymember)). Feel free to share any problems, questions and suggestions with your peers on the Dynatrace Community's [Application Monitoring & UEM Forum](https://answers.dynatrace.com/spaces/146/index.html).

## License

Licensed under the MIT License. See the [LICENSE](https://github.com/Dynatrace/Dynatrace-Docker/blob/master/LICENSE) file for details.
[![analytics](https://www.google-analytics.com/collect?v=1&t=pageview&_s=1&dl=https%3A%2F%2Fgithub.com%2FdynaTrace&dp=%2FDynatrace-Docker%2FDynatrace-Server&dt=Dynatrace-Docker%2FDynatrace-Server&_u=Dynatrace~&cid=github.com%2FdynaTrace&tid=UA-54510554-5&aip=1)]()