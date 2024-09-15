# satisfactory-docker

[![Docker Pulls](https://img.shields.io/docker/pulls/donimax/satisfactory-docker)](https://hub.docker.com/r/donimax/satisfactory-docker)
[![Docker Image Size (tag)](https://img.shields.io/docker/image-size/donimax/satisfactory-docker/latest)](https://hub.docker.com/r/donimax/satisfactory-docker)

This is a Dockerized version of the [Satisfactory](https://store.steampowered.com/app/526870/Satisfactory/) dedicated server.

## Docker-compose file

```yaml
version: '3.9'
services:
  satisfactory-server-unique:
    container_name: 'satisfactory-server-unique'
    hostname: 'satisfactory-server-unique'
    image: 'donimax/satisfactory-docker:latest'
    ports:
      - '7777:7777/udp'
      - '7777:7777/tcp'
      - '15000:15000/udp'
      - '15777:15777/udp'
    volumes:
      - '/opt/docker/satisfactory/config:/config'
    environment:
      - MAXPLAYERS=8
      - PGID=1000
      - PUID=1000
      - SERVERBEACONPORT=15000
      - SERVERGAMEPORT=7777
      - SERVERQUERYPORT=15777
      - SERVERIP=0.0.0.0
      - SATISFACTORY_MULTIHOME=0.0.0.0
      - STEAMAPPID=1690800
    restart: unless-stopped
    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"
    healthcheck:
      test: ["CMD-SHELL", "curl -f http://localhost:15777 || exit 1"]
      interval: 1m30s
      timeout: 10s
      retries: 5
      start_period: 40s

networks:
  default:
    driver: bridge

```

UPDATED BY ME FOR PORTAINER STACK
