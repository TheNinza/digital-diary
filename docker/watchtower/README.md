# Watchtower

[Watchtower](https://containrrr.dev/watchtower/) is a tool that automatically updates running Docker containers with the latest version of the image.

## Installation

The Watchtower addon can be installed as a docker container.

```bash
docker run -d \
  --name watchtower \
  --restart always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  containrrr/watchtower
```

## Configuration

Define the configuration in a `.env` file and run the container using the following command:

```bash
docker run -d \
  --name watchtower \
  --restart always \
  --env-file .env \
  -v /var/run/docker.sock:/var/run/docker.sock \
  containrrr/watchtower
```

## Configurations I use

| Variable                                        | Value            | Description                                                                                                                                            |
| ----------------------------------------------- | ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `TZ`                                            | `IST`            | Set the timezone.                                                                                                                                      |
| `WATCHTOWER_CLEANUP`                            | `true`           | Remove old images after updating.                                                                                                                      |
| `WATCHTOWER_DEBUG`                              | `true`           | Enable debug logging.                                                                                                                                  |
| `WATCHTOWER_MONITOR_ONLY`                       | `true`           | Only check for updates, do not pull and restart containers.                                                                                            |
| `WATCHTOWER_SCHEDULE`                           | `0 0 0 * * *`    | Check for updates every day at 12:00 AM.                                                                                                               |
| `WATCHTOWER_NOTIFICATIONS`                      | `email`          | Send notifications to email.                                                                                                                           |
| `WATCHTOWER_NOTIFICATION_EMAIL_FROM`            | `from@gmail.com` | Email address to send notifications from.                                                                                                              |
| `WATCHTOWER_NOTIFICATION_EMAIL_TO`              | `to@gmail.com`   | Email address to send notifications to.                                                                                                                |
| `WATCHTOWER_NOTIFICATION_EMAIL_SERVER`          | `smtp.gmail.com` | SMTP server to use for sending notifications.                                                                                                          |
| `WATCHTOWER_NOTIFICATION_EMAIL_SERVER_PORT`     | `587`            | SMTP server port to use for sending notifications.                                                                                                     |
| `WATCHTOWER_NOTIFICATION_EMAIL_SERVER_USER`     | `from@gmail.com` | SMTP server username to use for sending notifications. (Same as `WATCHTOWER_NOTIFICATION_EMAIL_FROM` in case of gmail)                                 |
| `WATCHTOWER_NOTIFICATION_EMAIL_SERVER_PASSWORD` | `password`       | SMTP server password to use for sending notifications. You can use [app passwords](https://support.google.com/accounts/answer/185833?hl=en) for gmail. |

To know more about the configurations, visit the [official documentation](https://containrrr.dev/watchtower/arguments/).

## Ignore containers

To ignore containers, add the label `com.centurylinklabs.watchtower.enable=false` to the container.

```bash
docker run -d \
  --name watchtower \
  --restart always \
  -v /var/run/docker.sock:/var/run/docker.sock \
  --label com.centurylinklabs.watchtower.enable=false \
  some-container
```
