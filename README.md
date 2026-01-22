# Local Databases

This repository contains Docker Compose configurations for running local database instances.

## Prerequisites

- [Docker](https://www.docker.com) and Docker Compose installed
- Git (optional, for cloning this repository)

## Available Databases

- [MySQL](#mysql)
- [PostgreSQL](#postgresql)
- [Supabase](#supabase)

---

## MySQL

### Setup

1. Navigate to the MySQL directory:
   ```bash
   cd mysql
   ```

2. Copy the `.env.example` file to `.env` and update the values as required:
   ```bash
   cp .env.example .env
   ```
   
   Then edit `.env` and update the password values with your secure credentials.

3. Start the MySQL container:
   ```bash
   docker compose up -d
   ```

4. Verify the container is running:
   ```bash
   docker compose ps
   ```

### Connection Details

- **Host:** `localhost`
- **Port:** `33061` (or value from `MYSQL_PORT` in `.env`)
- **Root User:** `root`
- **Root Password:** Value from `MYSQL_ROOT_PASSWORD` in `.env`
- **Database User:** Value from `MYSQL_USER` in `.env` (default: `user`)
- **Database Password:** Value from `MYSQL_PASSWORD` in `.env`

### Connection String Example

```
mysql://user:your_secure_user_password@localhost:33061
```

### Stop the Database

```bash
docker compose down
```

### Remove Data

```bash
docker compose down -v
```

---

## PostgreSQL

### Setup

1. Navigate to the PostgreSQL directory:
   ```bash
   cd postgresql
   ```

2. Copy the `.env.example` file to `.env` and update the values as required:
   ```bash
   cp .env.example .env
   ```
   
   Then edit `.env` and update the password values with your secure credentials.

3. Start the PostgreSQL container:
   ```bash
   docker compose up -d
   ```

4. Verify the container is running:
   ```bash
   docker compose ps
   ```

### Connection Details

- **Host:** `localhost`
- **Port:** `54321` (or value from `POSTGRES_PORT` in `.env`)
- **User:** Value from `POSTGRES_USER` in `.env` (default: `user`)
- **Password:** Value from `POSTGRES_PASSWORD` in `.env`
- **Database:** `postgres` (default database)

### Connection String Example

```
postgresql://user:your_secure_password@localhost:54321/postgres
```

### Stop the Database

```bash
docker compose down
```

### Remove Data

```bash
docker compose down -v
```

---

## Supabase

### Setup

1. Navigate to the Supabase directory:
   ```bash
   cd supabase
   ```

2. Copy the `.env.example` file to `.env` and update the values as required:
   ```bash
   cp .env.example .env
   ```
   
   Then edit `.env` and update the password and JWT secret values with your secure credentials.

3. Start the Supabase services:
   ```bash
   docker compose up -d
   ```

4. Wait for all services to be healthy (this may take a minute):
   ```bash
   docker compose ps
   ```

### Services

Supabase runs three services:

1. **Database (PostgreSQL)** - The main database
   - Port: `54328` (or value from `POSTGRES_PORT` in `.env`)
   - Container: `common-supabase-db`

2. **Meta Service** - Database metadata API
   - Port: `8888` (or value from `PG_META_PORT` in `.env`)
   - Container: `common-supabase-meta`

3. **Studio** - Supabase web interface
   - Port: `4008` (or value from `STUDIO_PORT` in `.env`)
   - Container: `common-supabase-studio`
   - Access at: `http://localhost:4008`

### Connection Details

- **Database Host:** `localhost`
- **Database Port:** `54328` (or value from `POSTGRES_PORT` in `.env`)
- **Database User:** `postgres`
- **Database Password:** Value from `POSTGRES_PASSWORD` in `.env`
- **Database Name:** Value from `POSTGRES_DB` in `.env` (default: `postgres`)

### Connection String Example

```
postgresql://postgres:your_secure_password@localhost:54328/postgres
```

### Access Supabase Studio

Open your browser and navigate to:
```
http://localhost:4008
```

### Stop the Services

```bash
docker compose down
```

### Remove Data (Clean Start)

```bash
docker compose down -v
```

---

## General Notes

- Each database directory contains a `.env.example` file with default configuration values
- Copy `.env.example` to `.env` and update the values (especially passwords and secrets) before starting services
- All `.env` files are gitignored and should not be committed to version control
- Database data is persisted in Docker volumes
- Default ports are chosen to avoid conflicts with standard database installations
- For production use, ensure all passwords are strong and secure
- To view logs for any service, use: `docker compose logs [service-name]`
