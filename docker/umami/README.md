# Umami

Umami is a simple, fast, open-source web analytics alternative to Google Analytics.

## Installation and configuration

### Environment variables

Create a `.env` file with the following environment variables:

```bash
POSTGRES_DB=umami
POSTGRES_USER=umami
POSTGRES_PASSWORD=somesecret
HASH_SALT=somesecret
```

> _A quick way to generate a random password is to use the following command:_

```bash
openssl rand -base64 32
```

### Prepare the database

Create a `sql` directory and copy the `scheme.postgresql.sql` file from the [Umami repository](https://github.com/umami-software/umami/blob/master/sql/schema.sql) into it.

```bash
mkdir sql
wget https://raw.githubusercontent.com/umami-software/umami/master/sql/schema.sql -O sql/schema.postgresql.sql
```

### Start the container

Copy the contents from the `docker-compose.yaml` file from this repository into your `docker-compose.yaml` file.

_Make sure to replace the `<application-path>` placeholder in the volumes section with the path to your Umami application._

Finally, run the following command to start the Umami container:

```bash
docker-compose up -d
```

The Umami application should now be available at `http://localhost:3000`. (As it is exposed on port 3000 in the `docker-compose.yaml` file.)

## Post-installation

### Login

The first time you visit the Umami application, you will be prompted to enter a username and password. Enter the following credentials:

```bash
Username: admin
Password: umami
```

Click the `Login` button to continue and change the password.
