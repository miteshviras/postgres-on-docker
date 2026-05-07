# PostgreSQL on Docker

A simple setup to run PostgreSQL 16 using Docker Compose with persistent storage and automatic database initialization scripts.

---

## Prerequisites

Install:

* [Docker](https://www.docker.com/products/docker-desktop/?utm_source=chatgpt.com)
* [Docker Compose](https://docs.docker.com/compose/?utm_source=chatgpt.com)

Verify installation:

```bash
docker --version
docker compose version
```

---

# Project Structure

```bash
postgres-on-docker/
│
├── docker-compose.yml
├── init-db/
└── README.md
```

---

---

# Start PostgreSQL

Run PostgreSQL in background:

```bash
docker compose up -d
```

Check running containers:

```bash
docker ps
```

View logs:

```bash
docker compose logs -f
```

---

# Stop PostgreSQL

```bash
docker compose down
```

Stop and remove volumes (Deletes all database data):

```bash
docker compose down -v
```

---

# Connect to PostgreSQL Container

Open PostgreSQL shell:

```bash
docker exec -it postgres_multi_db psql -U admin -d default_db
```

---

# Database Connection Details

| Key      | Value      |
| -------- | ---------- |
| Host     | localhost  |
| Port     | 5432       |
| Database | default_db |
| Username | admin      |
| Password | secret     |

---

# Create Multiple Databases Automatically

Place SQL files inside:

```bash
init-db/
```

Example:

## init-db/init.sql

```sql
CREATE DATABASE app_db;
CREATE DATABASE analytics_db;
CREATE DATABASE testing_db;
```

These scripts run automatically during first container startup.

> NOTE:
> Initialization scripts execute only when the volume is empty.

To rerun initialization:

```bash
docker compose down -v
docker compose up -d
```

---

# Backup Database

```bash
docker exec postgres_multi_db pg_dump -U admin default_db > backup.sql
```

---

# Restore Database

```bash
cat backup.sql | docker exec -i postgres_multi_db psql -U admin -d default_db
```

---

# One-Line Install Command

Clone and start PostgreSQL:

```bash
git clone <YOUR_REPOSITORY_URL>
cd postgres-on-docker
docker compose up -d
```

---

# Useful Docker Commands

## Restart container

```bash
docker restart postgres_multi_db
```

## Enter container shell

```bash
docker exec -it postgres_multi_db bash
```

## Remove container

```bash
docker rm -f postgres_multi_db
```

---

# Access from Applications

Example connection string:

```bash
postgresql://admin:secret@localhost:5432/default_db
```

---

# PostgreSQL Version

```bash
PostgreSQL 16
```

---

# License

MIT License
