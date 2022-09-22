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
docker run -d -p 8000:8000 -p 9000:9000 --name portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```

> Alternatively, you can use the docker-compose.yaml file provided in this repository. Make sure you have created the volume first.

> Note: export port 8000 if you want to use the edge compute features.

## Post Installation

1. A good practice is to not expose ports to the internet. You can use a reverse proxy to access Portainer from the internet. For example, if you are using a nginx-proxy-manager on docker with a network named _nginxproxymanager_default_, you can use the following command to create a container that will expose Portainer on port 80 and 443:

```bash
docker run -d --network nginxproxymanager_default --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest
```
