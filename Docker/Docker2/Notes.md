# 🐳 DevOps 11 — Docker (Expanded & Detailed)

> Complete, corrected notes with examples, diagrams, troubleshooting and tips.

---

## Table of contents

1. Docker fundamentals (commands, images, tags)
2. Dockerfile — example + explanation
3. Running containers (run, exec, attach, logs)
4. NGINX: host a simple HTML project (step-by-step)
5. Volumes — concepts, examples, bind mounts vs named volumes
6. Docker Compose — full examples + `.env` usage
7. Networking basics (bridge, host, container-to-container)
8. Pushing images to Docker Hub (tag, push)
9. Troubleshooting & common errors
10. Quick cheat sheet & best practices

---

## 1 — Docker fundamentals

**Image vs Container**

* **Image**: read-only template (blueprint) for creating containers. Built from a `Dockerfile`.
* **Container**: a running instance of an image (read-write layer on top).

**Important commands**

```sh
# List images
docker images

# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Remove a container
docker rm <containerId_or_name>

# Remove an image
docker rmi <imageId_or_name>
```

**Tagging**

* `docker tag SOURCE_IMAGE[:TAG] TARGET_IMAGE[:TAG]`
* Tags help version and name images, and are required for pushing to registries.

Example:

```sh
docker build -t django-app-image:latest .
docker tag django-app-image:latest docker.io/ophidev/django-app-image:latest
```

---

## 2 — Dockerfile — explanation + example

A `Dockerfile` is a list of instructions to build an image.

**Simple Python/Django Dockerfile example**

```dockerfile
# Use official Python base image
FROM python:3.9-slim

# Set working directory inside container
WORKDIR /app

# Copy requirements and install first (leverages cache)
COPY requirements.txt /app/
RUN pip install --no-cache-dir -r requirements.txt

# Copy project source
COPY . /app

# Expose port used by app
EXPOSE 8000

# Default command to run app (example: Django dev server)
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
```

**Build image**

```sh
docker build -t my-django-app:1.0 .
```

**Tips**

* Use small base images (slim, alpine) when possible to reduce size.
* Put `COPY requirements.txt` and `RUN pip install` before copying the full project to use layer caching.
* Use `.dockerignore` to exclude node_modules, .git, large files.

---

## 3 — Running & interacting with containers

**Run a container**

```sh
docker run -d --name my-app -p 8000:8000 my-django-app:1.0
```

* `-d` runs detached (in background)
* `--name` gives the container a friendly name
* `-p hostPort:containerPort` publishes container port to host

**Execute commands inside a running container**

```sh
docker exec -it <containerId_or_name> bash
# or if no bash available
docker exec -it <containerId_or_name> sh
```

**Attach to a container's main process (stdin/out)**
`docker attach <containerId_or_name>`

* Attach to the primary process (useful for interactive processes).
* **Caution:** `CTRL+C` may send SIGINT to the process inside container (can stop it). For shell, prefer `docker exec`.

**View logs**

```sh
docker logs <containerId_or_name>
# Follow logs in real-time
docker logs -f <containerId_or_name>
# Show last N lines
docker logs --tail 100 <containerId_or_name>
```

**Stop and remove**

```sh
docker stop <containerId_or_name>
docker rm <containerId_or_name>
```

---

## 4 — NGINX: host a simple HTML project (step-by-step)

**Goal**: serve `index.html` using nginx Docker container.

1. Create `index.html` in current folder:

```html
<!-- index.html -->
<!doctype html>
<html><body><h1>Hello from NGINX Docker!</h1></body></html>
```

2. Run nginx and mount the file:

```sh
# Option A: copy into running container
docker run -d --name my-nginx -p 8080:80 nginx
docker cp index.html my-nginx:/usr/share/nginx/html/index.html

# Option B: bind mount local folder to nginx html folder
docker run -d --name my-nginx -p 8080:80 -v $(pwd):/usr/share/nginx/html:ro nginx
# :ro makes it read-only inside container
```

3. Open `http://localhost:8080` — you should see the page.

**Troubleshooting**

* If blank or default page: confirm path `/usr/share/nginx/html/index.html`
* Use `docker logs my-nginx` to see nginx logs
* `docker exec -it my-nginx ls /usr/share/nginx/html` to inspect files

---

## 5 — Volumes — persistent storage

**Why volumes?**

* Container filesystem is ephemeral. Volumes persist data independently of container lifecycle.
* Use volumes for databases, logs, or user content.

### Types

1. **Named volume (Docker-managed)** — good for production and portability
2. **Bind mount (host directory)** — direct mapping to a host folder (useful for dev)

### Create named volume (bind to host path)

You earlier used `docker volume create --opt device=... --opt o=bind --opt type=none --name name`

* That creates a named volume but bound to a host directory (advanced use).
* Simpler options exist (see examples).

**Example — named volume (Docker-managed)**

```sh
# Create a named volume
docker volume create my_data

# Use it with run
docker run -d --name my-app -v my_data:/app/data my-django-app
```

**Example — bind mount (host folder)**

```sh
mkdir -p ~/projects/appdata
docker run -d --name my-app -v ~/projects/appdata:/app/data my-django-app
```

**Inspect volume**

```sh
docker volume ls
docker volume inspect my_data
```

**Example demonstrating persistence**

1. Run container mounting host path:

```sh
docker run -d --name demo -v ~/vol_demo:/data alpine tail -f /dev/null
```

2. Create file inside container:

```sh
docker exec -it demo sh -c "echo 'hello' > /data/test.txt"
```

3. On host check `~/vol_demo/test.txt` → contains `hello`

### Mountpoint vs device

* `Mountpoint` in `docker inspect` output is where Docker stores the volume data on the host (usually under `/var/lib/docker/volumes/<vol>/_data`).
* `device` option is used when creating a volume with a specific host directory (bind).

---

## 6 — Docker Compose (full examples & `.env`)

**When to use Compose?**

* Multiple services that must run together (frontend,backend, Db).
* Easier `up`, `down`, networking and shared volumes.

### Basic `docker-compose.yaml`

```yaml
version: '3.9'

services:
  web:
    build: .
    container_name: django-app
    ports:
      - "8001:8000"
    volumes:
      - django_app_volume:/app
    depends_on:
      - db

  db:
    image: mysql:5.7
    container_name: mysql_ctr
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: "${MYSQL_ROOT_PASSWORD}"
    volumes:
      - db_data:/var/lib/mysql

volumes:
  django_app_volume:
  db_data:
```

**.env file**

```
MYSQL_ROOT_PASSWORD=test@123
```

* Compose will load `.env` in same folder and substitute `${VAR}`.

**Common commands**

```sh
docker-compose up               # foreground (shows logs)
docker-compose up -d            # background
docker-compose down             # stop & remove containers, networks, but keep named volumes by default
docker-compose down -v          # also remove volumes
docker-compose ps               # show compose managed containers
```

**Notes**

* `depends_on` ensures start order but does *not* wait for service readiness (e.g., MySQL ready to accept connections). For that, use healthchecks or wait-for scripts.
* Compose auto-creates a network `project_default` for services; services can refer to each other by service name (DNS).

---

## 7 — Docker Networking basics

**Default network modes**

* **bridge (default)**: isolates containers; containers talk using container IP or service name on same user-defined bridge.
* **host**: container uses host network stack (no port mapping).
* **none**: no networking.
* **overlay** (swarm/k8s): multi-host networks.

**Using service name DNS**

* In Compose, service `db` is reachable as `db:3306` from `web` service.

**Create a user-defined bridge network** (allows container name DNS lookup)

```sh
docker network create my_bridge
docker run -d --name redis --network my_bridge redis
docker run -d --name app --network my_bridge my-app
# From app, connect to redis:6379
```

---

## 8 — Pushing images to Docker Hub

**Steps**

1. Login:

```sh
docker login
# If 2FA on Docker Hub, use a Personal Access Token as password
```

2. Tag the image using your Docker Hub namespace:

```sh
docker tag local-image:tag docker.io/<yourusername>/repo-name:tag
```

3. Push:

```sh
docker push docker.io/<yourusername>/repo-name:tag
```

**Example**

```sh
docker build -t django-app-image:latest .
docker tag django-app-image:latest docker.io/ophidev/django-app-image:latest
docker push docker.io/ophidev/django-app-image:latest
```

**Common errors**

* `denied: requested access to the resource is denied`: you don't own the target repo — ensure tag includes your username.
* `no basic auth credentials`: not logged in or token expired.

---

## 9 — Troubleshooting & common errors

### MySQL in Compose asks for password

Error:

```
[ERROR] Database is uninitialized and password option is not specified
```

Fix: add environment variable `MYSQL_ROOT_PASSWORD` or one of accepted envs in `docker-compose.yaml` or `.env`.

### Container immediately exits

* Check `docker logs <container>` for reason.
* If the process inside exited (e.g., script finished), container will stop. Keep a long-running process (e.g., server or `tail -f /dev/null` for debugging).

### Permission issues with bind mounts

* Host filesystem permissions may prevent container process from writing.
* Fix: chown/chmod on host folder or run container with user mapping.

### `docker: unknown command: docker pc`

* Typo. Correct command is `docker ps` or `docker-compose`.

### Ports already in use

* `Error starting userland proxy: listen tcp 0.0.0.0:8000: bind: address already in use`

  * Kill the host process using the port or map to another host port.

### Network name not found on `docker-compose down`

* Compose already removed the network; repeated `down` may warn that network not found — harmless.

---

## 10 — Quick Cheat Sheet & Best Practices

### Quick commands

```sh
# Build
docker build -t my-image:tag .

# Run
docker run -d --name c1 -p 8080:80 my-image:tag

# Exec
docker exec -it c1 bash

# Logs (follow)
docker logs -f c1

# Inspect volume
docker volume inspect my_volume

# Compose up
docker-compose up -d

# Compose down
docker-compose down
```

### Best practices

* Use `.dockerignore` to reduce image context size.
* Keep container processes single-purpose (one main process).
* Use ENV variables for secrets in dev; for production use secret managers.
* Prefer named volumes for DB persistence, not ephemeral containers.
* Keep images small (multi-stage builds when building artifacts).
* Use healthchecks in Compose to detect service readiness.

**Example healthcheck in Dockerfile**

```dockerfile
HEALTHCHECK --interval=30s --timeout=5s \
  CMD curl -f http://localhost:8000/health || exit 1
```

---

## Appendices

### A — `docker-compose` with a wait-for-db pattern

If your web app needs DB ready, either:

* implement retry logic in app, or
* use a small script like `wait-for-it.sh` or `dockerize` to wait for DB port.

Example service in compose:

```yaml
services:
  web:
    build: .
    command: ["./wait-for-it.sh", "db:3306", "--", "python", "manage.py", "runserver", "0.0.0.0:8000"]
    depends_on:
      - db
```

### B — Example: NGINX reverse proxy for multiple services

`docker-compose.yaml` snippet:

```yaml
services:
  nginx:
    image: nginx:stable
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    depends_on:
      - web
```

`nginx.conf` with upstreams can route `example.com/api` to `web:8000` and `example.com/` to static service.

---

## Final notes & next steps

You were right — more examples and clearer explanations helped. I included:

* Basic → advanced examples
* Full `Dockerfile`, `docker run`, `docker-compose` examples
* NGINX hosting steps and reverse proxy notes
* Volume details and persistence test
* Troubleshooting and tips


