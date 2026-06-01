# Infrastructure

## Local Stack

Start the full local stack:

```bash
docker compose up --build -d
```

Start the stack with multiple backend instances behind Envoy:

```bash
docker compose up --build -d --scale backend=2
```

Stop the stack:

```bash
docker compose down
```

Envoy listens on `127.0.0.1:8080` and balances traffic across the `backend`
containers.

The database listens on `127.0.0.1:3307`.

The stack includes:

- `mysql`
- `backend`
- `envoy`

Default database credentials:

- database: `morrowletter`
- user: `morrowletter`
- password: `morrowletter`

Data is persisted in `./mysql/data`.

## Backend Routing

Envoy is the only service exposed on backend HTTP port `8080`.

- Requests to `127.0.0.1:8080` go to Envoy first.
- Envoy forwards them to the internal `backend:8080` service.
- When `backend` is scaled above `1`, Envoy round-robins across the backend containers.

The backend containers are not published directly to the host. They are only
reachable on the Compose network.

## Scaling

Start two backend instances behind Envoy:

```bash
docker compose up --build -d --scale backend=2
```

Change the backend replica count later without rebuilding:

```bash
docker compose up -d --scale backend=3
```

## Logs

Tail Envoy logs:

```bash
docker compose logs -f envoy
```

Tail all backend container logs:

```bash
docker compose logs -f backend
```

List the actual backend containers created by scaling:

```bash
docker compose ps backend
```

Rebuild the backend image after backend changes:

```bash
docker compose up --build -d backend
```

Rebuild and restart the load-balanced local stack:

```bash
docker compose up --build -d --scale backend=2 backend envoy
```

## Health Check Example

Check the backend through Envoy:

```bash
curl http://127.0.0.1:8080/health
```

Check readiness through Envoy:

```bash
curl http://127.0.0.1:8080/ready
```
