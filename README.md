

# PSUSphere (Docker)

A Django project (PSUSphere) containerized with Docker. Anyone can run it with a single command, with no need to install Python or Django.

## Requirements

- [Docker Desktop](https://www.docker.com/products/docker-desktop) (on Windows, with WSL 2 enabled)

Check that Docker is installed:

docker --version


## Option 1: Run from Docker Hub (for clients)

Image: `charsgerand/psusphere:latest`

1. Download or copy the `for_client/docker-compose.yml` file into an empty folder.
2. Open a terminal in that folder and run:


docker compose up -d


3. Open **http://localhost:8000** in your browser.
4. Create an account:


docker compose exec web python manage.py createsuperuser


5. Stop the app:


docker compose down


## Option 2: Build from source (for developers)

1. Clone this repository:


git clone https://github.com/Tazz022003/psusphere-docker.git
cd psusphere-docker

2. Build and run:

docker compose up --build

3. Open **http://localhost:8000**.

## Useful commands

| Command | Description |
|---|---|
| `docker compose up -d` | Start the app in the background |
| `docker compose ps` | Check running containers |
| `docker compose logs -f web` | View logs |
| `docker compose down` | Stop and remove the containers |
| `docker build -t my-django-app:latest .` | Build the image manually |

## Notes

- The database is a fresh SQLite database created on first run (`migrate` runs automatically). In `for_client`, data is kept inside the container and is lost after `docker compose down`.
- Google and GitHub login buttons use placeholder credentials, so they will not log you in. Use the username and password of the account you created with `createsuperuser`.
- Use `http://localhost:8000` or `http://127.0.0.1:8000`. Do not use `0.0.0.0`.

## Project files

- `Dockerfile`: instructions for building the image
- `docker-compose.yml`: builds the image and runs the app locally
- `for_client/docker-compose.yml`: pulls the image from Docker Hub and runs it
- `requirements.txt`: Python dependencies
- `.dockerignore`: files excluded from the image