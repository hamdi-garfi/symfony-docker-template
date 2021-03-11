# Docker Template


Is a based [Docker](https://www.docker.com/) project to create [Symfony](https://symfony.com) application with docker. this project include a full [HTTP/2](https://symfony.com/doc/current/weblink.html) and HTTPS support..

## Getting Started

1. Run `docker-compose up` (the logs will be displayed in the current shell)
2. Open `https://localhost` in your favorite web browser 

## Selecting a Specific Symfony Version

Use the `SYMFONY_VERSION` environment variable to select a specific Symfony version.

For instance, use the following command to install Symfony 4.4 LTS:

`SYMFONY_VERSION=4.4.* docker-compose up --build`

To install a non-stable version of Symfony, use the `STABILITY` environment variable during the build.
The value must be [a valid Composer stability option](https://getcomposer.org/doc/04-schema.md#minimum-stability)) .

For instance, use the following command to use the `master` branch of Symfony:

```bash
docker-compose up --build
```

## Debugging

The default Docker stack is shipped without a Xdebug stage.
It's easy though to add [Xdebug](https://xdebug.org/) to your project, for development purposes such as debugging tests or API requests remotely.

### Add a Development Stage to the Dockerfile

To avoid deploying Symfony Docker to production with an active Xdebug extension,
it's recommended to add a custom stage to the end of the `Dockerfile`.

```Dockerfile
# Dockerfile
FROM sf_app as sf_app_dev

ARG XDEBUG_VERSION=2.8.0
RUN set -eux; \
	apk add --no-cache --virtual .build-deps $PHPIZE_DEPS; \
	pecl install xdebug-$XDEBUG_VERSION; \
	docker-php-ext-enable xdebug; \
	apk del .build-deps
```


