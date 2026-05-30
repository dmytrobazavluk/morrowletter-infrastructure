# Infrastructure

## Local MySQL

Start MySQL:

```bash
docker compose up -d
```

Stop MySQL:

```bash
docker compose down
```

The database listens on `127.0.0.1:3306`.

Default local credentials:

- database: `morrowletter`
- user: `morrowletter`
- password: `morrowletter`

Data is persisted in `./mysql/data`.
