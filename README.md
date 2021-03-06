# Sprankle-Pod!

How to get the attention of Docker Engineering?

PLEASE FIX DOCKER_COMPOSE - THIS IS HOW!

add: `docker-compose use`

## AngelBox

AngelBox provides a framework for running compositions of docker images.
The obvious tool for this is docker-compose. Ironically, the one thing that
docker-compose is lousy at, is "composition".

Docker-compose prefers one single `yaml` file that specifies a 'composition' of all of your
services. But, what you cant do is "COMPOSE" that 'composition' by assembly.

AngelBox uses a simple method to create this 'composition' that can be applied to any and
every docker image. Each docker image is represented by its own `yaml` file in which all
of the important features are made customisable through variables.

see: http://github.com/keithy/angelbox

## Docker-Compose-USE <composition-list.env>

The script `docker-compose-use` creates a `.env` file for `docker-compose` to use.
It processes an input `composition-list.env` file which  provides the list of services to be composed and values for the variables. This file format is just the original .env file format but with comments and line continuations allowed, thats it! That is the only change necessary to make docker-compose "composable".

```
usage:
#> docker-compose-use ./config-example/server.env
```
where `./config-example/server.env` is:
```
MYSQL_IMAGE=mariadb/10.4-bionic
MYSQL_PORTS_3306=4000

COMPOSE_FILE=common.yml:\
    hub/official/mysql.yml:\
    hub/official/mysql/+file-secrets.yml:\
    common-end.yml
```

#### Conventions

- Additions/Variations are provided in a folder with the name of the service.
- Overrides are indicated by the `+` in the filename.
- comments and blank lines are ignored.
- Variables are named (strictly) according to their position in the `yaml` structure.

## Docker-Compose-USE <composition.env> <deployment.env>

A second `env` file can be provided with additional values that relate to a specific
deployment instance, which can be used like so.

```
docker-compose-use my-services.env $(hostname).env
```


