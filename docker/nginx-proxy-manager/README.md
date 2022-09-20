# Nginx Proxy Manager

Nginx Proxy Manager is a web application that allows you to easily forward your domains to your servers. It also allows you to easily manage your SSL certificates.

## Pre-requisites

- Linux server with docker and docker-compose installed.
- A domain name that points to your server.

## Install

1. Create new directory in the opt directory and cd into it.

```bash
sudo mkdir /opt/nginxproxymanager
cd /opt/nginxproxymanager
```

2. Create a new docker-compose.yml file

```bash
sudo vim docker-compose.yml
```

3. Copy the following content to the docker-compose.yml file

4. Create the environment file

```bash
sudo vim .env
```

5. Copy the following content to the .env file

```bash
MYSQL_USER=<username>
MYSQL_PASSWORD=<password>
MYSQL_ROOT_PASSWORD=<root-password>
MYSQL_DATABASE=<database-name>
```

6. Start the container

```bash
sudo docker-compose up -d
```

7. Open the web application in your browser
   Now we can log in to the web UI on port 81. Log in with the **username** _"admin@example.com"_ and the **password** _"changeme"_. Next, you should change your username and password, and that’s it!

## SSL Certificates

1. Create a new A record in your DNS provider that points to your server's IP address.
