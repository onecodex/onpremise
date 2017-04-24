# Sentry On-Premise [![Build Status][build-status-image]][build-status-url]

Official bootstrap for running your own [Sentry](https://sentry.io/) with [Docker](https://www.docker.com/).

## Sentry On-Premise with Aptible

To run as an app on Aptible:

1. Provision a PostgreSQL database, either from the Aptible Dashboard or the Aptible CLI.

1. Provision a Redis database, either from the Aptible Dashboard or Aptible CLI.

1. Provision an Aptible app, either from the Aptible Dashboard or the Aptible CLI.

1. Configure the following (required and optional) environment variables for your Sentry app:

| Variable | Description | Required? | Default Value |
| -------- | ----------- | --------- | ------------- |
| `ADMIN_PASSWORD` | Admin password | Yes | - |
| `DATABASE_URL` | PostgreSQL database URL | Yes | - |
| `SENTRY_REDIS_HOST` | Redis host | Yes | - |
| `SENTRY_REDIS_PASSWORD` | Redis password | Yes | - |
| `SENTRY_REDIS_PORT` | Redis port | Yes | - |
| `SENTRY_URL_PREFIX` | Base URL for server | Yes | - |
| `ADMIN_USERNAME` | Admin username | No | Aptible |
| `AWS_ACCESS_KEY_ID` | AWS Access Key for S3 filestore | No | - |
| `AWS_SECRET_ACCESS_KEY` | AWS Secret Access Key for S3 filestore | No | - |
| `AWS_STORAGE_BUCKET_NAME` | AWS S3 bucket for S3 filestore | No | - |
| `AWS_S3_ENCRYPTION` | Use AES-256 encryption for S3 filetore | No | `True` |
| `GITHUB_APP_ID` | GitHub OAuth application ID (for GitHub integration) | No | - |
| `GITHUB_API_SECRET` | GitHub API secret | No | - |
| `MAILGUN_SERVER_NAME` | Your email domain (eg yourcompany.com) | No | - |
| `MAILGUN_ACCESS_KEY` | Mailgun API Key | No | - |
| `SENTRY_EMAIL_HOST` | SMTP hostname | No | - |
| `SENTRY_EMAIL_PASSWORD` | SMTP password | No | - |
| `SENTRY_EMAIL_PORT` | SMTP port | No | 25 |
| `SENTRY_EMAIL_USER` | SMTP user | No | - |
| `SENTRY_EMAIL_USE_TLS` | Use TLS for email? | No | `False` |
| `SENTRY_KEY` | Sentry key | No | (random) |
| `SENTRY_SECRET_KEY` | Secret key for [DSN clients](http://raven.readthedocs.org/en/latest/config/#the-sentry-dsn) sending events | No | (random) |
| `SSLIFY_DISABLE` | Disable forced HTTPS redirection? | No | `False` |
| `TEAM_NAME` | Team name | No | `Aptible` |


## Requirements

 * Docker 17.05.0+
 * Compose 1.17.0+

## Minimum Hardware Requirements:

 * You need at least 3GB RAM

## Setup

To get started with all the defaults, simply clone the repo and run `./install.sh` in your local check-out.

There may need to be modifications to the included `docker-compose.yml` file to accommodate your needs or your environment (such as adding GitHub credentials). If you want to perform these, do them before you run the install script.

The recommended way to customize your configuration is using the files below, in that order:

 * `config.yml`
 * `sentry.conf.py`
 * `.env` w/ environment variables

If you have any issues or questions, our [Community Forum](https://forum.sentry.io/c/on-premise) is at your service!

## Securing Sentry with SSL/TLS

If you'd like to protect your Sentry install with SSL/TLS, there are
fantastic SSL/TLS proxies like [HAProxy](http://www.haproxy.org/)
and [Nginx](http://nginx.org/). You'll likely to add this service to your `docker-compose.yml` file.

## Updating Sentry

Updating Sentry using Compose is relatively simple. Just use the following steps to update. Make sure that you have the latest version set in your Dockerfile. Or use the latest version of this repository.

Use the following steps after updating this repository or your Dockerfile:
```sh
docker-compose build --pull # Build the services again after updating, and make sure we're up to date on patch version
docker-compose run --rm web upgrade # Run new migrations
docker-compose up -d # Recreate the services
```

## Resources

 * [Documentation](https://docs.sentry.io/server/installation/docker/)
 * [Bug Tracker](https://github.com/getsentry/onpremise/issues)
 * [Forums](https://forum.sentry.io/c/on-premise)
 * [IRC](irc://chat.freenode.net/sentry) (chat.freenode.net, #sentry)


[build-status-image]: https://api.travis-ci.com/getsentry/onpremise.svg?branch=master
[build-status-url]: https://travis-ci.com/getsentry/onpremise
