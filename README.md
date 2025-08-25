# d2s-workshop-starter

Starter repository with minimal files and step-by-step instructions for deploying Data to Science during the workshop.

## Purpose

This repository is a starter template with minimal files and clear, step-by-step
instructions for deploying Data to Science during the workshop. It will include
the necessary Docker configuration and example environment/config files to run
Data to Science locally.

## Requirements

- [Docker Engine](https://docs.docker.com/engine/install/)
- [Docker Compose](https://docs.docker.com/compose/install/)

### Verify installation

- Docker Engine
  ```bash
  docker --version
  docker run --rm hello-world
  ```
- Docker Compose
  ```bash
  docker compose version
  # if using the legacy binary:
  docker-compose --version
  ```

## What’s included

These files are provided and ready to use:

- `docker-compose.yml`: Orchestrates all required services for Data to Science.
- `backend.env`: Environment for the API service.
- `db.env`: Environment for the PostGIS database and pg_tileserv.
- `frontend.env`: Environment for the frontend app.
- `pg_tileserv.toml`: Configuration for pg_tileserv.

## Quick start

1. Clone this repository
   ```bash
   git clone https://github.com/<your-org>/d2s-workshop-starter.git
   cd d2s-workshop-starter
   ```
2. Launch the stack
   ```bash
   docker compose up -d
   # if using the legacy binary:
   # docker-compose up -d
   ```
3. Access the application
   - App via proxy: `http://localhost:8000`
   - Vector tiles (pg_tileserv): `http://localhost:7800`
4. Verify services
   ```bash
   docker compose ps
   ```
5. View logs (optional)
   ```bash
   docker compose logs -f
   ```

## Configuration

- No manual configuration is required for the workshop. The provided
  `.env` files (`backend.env`, `db.env`, `frontend.env`) and `pg_tileserv.toml`
  are pre-configured to work out of the box with `docker compose up -d`.

## Common commands

- Start services (detached)
  ```bash
  docker compose up -d
  ```
- View logs
  ```bash
  docker compose logs -f
  ```
- Stop services
  ```bash
  docker compose down
  ```
- Rebuild images after changes
  ```bash
  docker compose up -d --build
  ```

## Troubleshooting

- Ports already in use (8000 or 7800)
  - Stop the other process or container using the port, then re-run
    `docker compose up -d`.
- Docker Compose command not found
  - Install/upgrade Docker Compose or use `docker-compose` if you have the
    legacy binary.
- Permission errors with Docker socket
  - Ensure your user is in the `docker` group, then restart your session.

## Appendix: Generate a tile signing key

If you need a random base64-encoded 64-byte secret for tile signing, run:

```python
import base64
import secrets

# Create random byte string with 64 bytes
secret_key_bytes = secrets.token_bytes(64)

# Base64 encode secret_key and convert to str object
secret_key_str = base64.b64encode(secret_key_bytes).decode("utf-8")
print(secret_key_str)
```

## License

This project is licensed under the terms of the LICENSE file included in this
repository.
