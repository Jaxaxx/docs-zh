# Docker Compose
___

## Installation

___

## Deploy Example

### 1. confluence
```shell
version: '3'

services:
  confluence:
    image: atlassian/confluence-server
    container_name: confluence
    ports:
      - 8090:8090
      - 8091:8091
    networks:
      - custom_net
    labels:
      - "traefik.enable=true"
      - "traefik.port=8090"
      - "traefik.frontend.rule=Host:${DOMAIN}"
      - "traefik.frontend.entryPoints=http,https"
    volumes:
      - ./data:/var/atlassian/application-data/confluence
      - ./mysql-connector-java-8.0.20.jar:/opt/atlassian/confluence/confluence/WEB-INF/lib/mysql-connector-java-8.0.20.jar
networks:
  custom_net:
    external:
      name: mynetwork
```

### 2. jira
```shell
version: '3.3'
services:
  jira:
    image: atlassian/jira-software
    container_name: jira
    restart: always
    ports:
      - "8080:8080"
    volumes:
      - ./data:/var/atlassian/application-data/
      - ./mysql-connector-java-8.0.20.jar:/opt/atlassian/jira/lib/mysql-connector-java-8.0.20.jar
networks:
  custom_net:
    external:
      name: mynetwork
```