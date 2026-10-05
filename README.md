# Django Notes App - Docker Compose

Nginx + Django + MySQL, run as 3 containers with Docker Compose.
I cloned an open-source Django notes app and wrote the Docker
setup for it as DevOps practice.
Original app: https://github.com/LondheShubham153/django-notes-app

Request flow: Browser -> Nginx (80) -> Django (8000) -> MySQL (3306)

## Run
docker compose up -d --build

## Problems I ran into
- Django couldn't find the DB: `.env` had the wrong host name. It must
  match the compose service name (`mysql`).
- Nginx kept restarting: it wasn't on the same network as Django.
- Nginx "host not found in upstream": the name in `nginx/default.conf`
  didn't match the service name (`django`).

All three came down to the same thing: names in config files must match
compose service names, and services must share a network.

Guided practice project, I used an AI assistant to help read some errors.
