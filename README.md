# docker-compose file to run the entire playtak ecosystem
## Requirements
### subdirectories

You may need to check out the `docker` branches (if there are no `Dockerfile`s in the repositories)

- `playtak-api` repository
- `playtak-nui` repository
- `playtak-ui` repository
- `tak-server` repository
  - `properties.xml` configured with
    - `<event-subscriber-url>http://tak-api/v1/tournaments/game/update</event-subscriber-url>`
    - `<db-path>/playtakdb/</db-path>`
- `playtakdb` containing `players.db` and `games.db`

# Usage
`docker-compose up --build --remove-orphans -d`

- [/](http://localhost/) for playtak UI
- [/nui/](http://localhost/nui/) for new playtak ui
- [/v1/](http://localhost/v1/) for playtak-api

# Development
## Setup
- `git clone` this repository
- `git submodule init`
- `git submodule update` consider using `--force`, needs to be done whenever this repository updated its submodules
- `docker-compose up --build --remove-orphans -d`
  - run this whenever a special config (`nginx.conf`, `docker-compose.yml`, ...) changed

If you like to commit changes, make sure to set `git config --global diff.ignoreSubmodules dirty` so that "dirty" (non-committed files) submodules are not
highlighted as changes to the root-repository

## nginx configuration
*2024-06-17 I don't remember why I added this here, websocket seems to be working fine as long as the reverseproxy runs on the standard HTTP/HTTPS ports*

to support websocket, use something like the following
```nginx
location / {
        # WebSocket support
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
        # forward to server
        proxy_pass http://localhost:8900;
}
```