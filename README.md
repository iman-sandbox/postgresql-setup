# 🐘 PostgreSQL Docker Setup with Test Data Types Table

This project sets up a local PostgreSQL instance using Docker, creates a test table with a wide variety of PostgreSQL data types, inserts 50 random records, and opens an interactive `psql` CLI.

---

## 📦 Features

- Pulls PostgreSQL image from a custom Harbor registry
- Removes old container if exists
- Starts a fresh PostgreSQL container
- Waits for initialization
- Creates a `test_data_types` table with:
  - Numeric types: `INTEGER`, `BIGINT`, `NUMERIC`, `REAL`, `SMALLINT`
  - Character types: `TEXT`, `VARCHAR`, `CHAR(1)`
  - Boolean: `BOOLEAN`
  - Temporal: `TIMESTAMP`, `DATE`, `INTERVAL`
  - Special types: `BYTEA`, `UUID`, `INET`, `JSON`, `TEXT[]`
- Inserts 50 random test rows using a PL/pgSQL loop
- Prints all inserted rows
- Opens PostgreSQL CLI inside container

---

## 🚀 How to Use

### 1. Clone or Download

Download this repository or the zip containing:

- `setup_postgres.sh`

### 2. Make Script Executable

```bash
chmod +x setup_postgres.sh
```

### 3. Run It

```bash
sudo ./setup_postgres.sh
```

This will:
- Start PostgreSQL on `localhost:5432`
- Insert test data
- Drop you into the interactive `psql` shell

---

## 🛠 Dependencies

- Docker
- Bash (Linux or WSL recommended)

---

## 🧪 Sample Table Schema

```sql
CREATE TABLE test_data_types (
    id SERIAL PRIMARY KEY,
    name TEXT,
    description VARCHAR(255),
    age INTEGER,
    balance NUMERIC(10,2),
    active BOOLEAN,
    created_at TIMESTAMP,
    updated_date DATE,
    rating REAL,
    big_value BIGINT,
    small_value SMALLINT,
    byte_value BYTEA,
    uuid_value UUID,
    inet_value INET,
    json_value JSON,
    tags TEXT[],
    status CHAR(1),
    interval_value INTERVAL
);
```

---

## 📤 Example Output (First Row)

```text
 id |   name   |     description     | age | balance | active |     created_at     | updated_date | rating | big_value | small_value |      byte_value       |            uuid_value            | inet_value |     json_value     |       tags       | status | interval_value
----+----------+---------------------+-----+---------+--------+---------------------+--------------+--------+-----------+-------------+------------------------+------------------------------------+-------------+--------------------+------------------+--------+-----------------
  1 | Name_1   | Description for ... |  33 | 7812.32 | t      | 2025-07-01 14:15:...| 2024-10-02   | 3.142  | 76433     | 14          | \xa887c8a...           | 548e3767-...                      | 192.168.0.42| {"key": "value_1"} | {tag1,tag2,tag1} |   C    | 5 days
```

---

## 🧹 Cleanup

To remove the container after testing:

```bash
docker stop postgres && docker rm postgres
```
