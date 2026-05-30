# Infrastructure

## Local Stack

Start the full local stack:

```bash
docker compose up --build -d
```

Stop the stack:

```bash
docker compose down
```

The backend listens on `127.0.0.1:8080`.

The database listens on `127.0.0.1:3306`.

The stack includes:

- `mysql`
- `backend`

Default database credentials:

- database: `morrowletter`
- user: `morrowletter`
- password: `morrowletter`

Data is persisted in `./mysql/data`.

Rebuild the backend image after backend changes:

```bash
docker compose up --build -d backend
```
