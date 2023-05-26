# docker-compose file to run the entire playtak ecosystem
## Requirements
### subdirectories

You may need to check out the `docker` branches (if there are no `Dockerfile`s in the repositories)

- `playtak-api` repository
- `playtak-games` repository
- `playtak-nui` repository
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
