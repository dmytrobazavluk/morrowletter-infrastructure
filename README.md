# Infrastructure

## Local Stack

Start MySQL and the backend:

```bash
docker compose up --build -d
```

Stop the stack:

```bash
docker compose down
```

The backend listens on `127.0.0.1:8080`.

The database listens on `127.0.0.1:3306`.

Default local credentials:

- database: `morrowletter`
- user: `morrowletter`
- password: `morrowletter`

Data is persisted in `./mysql/data`.
