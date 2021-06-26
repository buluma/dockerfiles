## Mattermost

[![](https://images.microbadger.com/badges/image/mritd/mattermost.svg)](https://microbadger.com/images/mritd/mattermost "Get your own image badge on microbadger.com") [![](https://images.microbadger.com/badges/version/mritd/mattermost.svg)](https://microbadger.com/images/mritd/mattermost "Get your own version badge on microbadger.com")

> Mattermost is an open source IM tool that is currently mainly used by individuals for automated deployment, such as bot deployment through Hubot docking with Kuberntes, GitLab-CI deployment notification, Sentry error alarm push, etc.

This image is made based on Alpine, without integrated database, etc., start the test docker-compose as follows 

``` sh
version: '2'
services:
  mattermost:
    image: mritd/mattermost:3.10.0
    restart: always
    volumes:
      - ./etc/mattermost/config.json:/usr/local/mattermost/config/config.json
    links:
      - mysql
    ports:
      - 8065:8065
  mysql:
    image: mysql:5.7.17
    restart: always
    volumes:
      - ./data/mysql:/var/lib/mysql
      - ./init/init.sql:/docker-entrypoint-initdb.d/init.sql
    environment:
      - MYSQL_ROOT_PASSWORD
```

**For complete docker-compose configuration, please refer to [mritd/docker-compose](https://github.com/mritd/docker-compose/tree/master/mattermost)**

