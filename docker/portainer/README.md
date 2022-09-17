# Potainer - Docker Management UI

[Portainer](https://www.portainer.io/) is a lightweight management UI which allows you to easily manage your Docker host or Swarm cluster.

## Usage

To use this image, you need to have a running Docker host. The easiest way to achieve this is by using Docker itself.

## Install Portainer

1. First, create the volume that Portainer Server will use to store its database:

```bash
docker volume create portainer_data
```

2. Download and run the Portainer image:

```bash
docker run -d -p 8000:8000 -p 9443:9443 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

> Alternatively, you can use the docker-compose.yaml file provided in this repository. Make sure you have created the volume first.

## Post Installation

1. Open your browser and navigate to `http://localhost:9000` or `https://localhost:9443` (if you have enabled TLS).
