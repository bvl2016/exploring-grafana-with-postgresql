# exploring-grafana-with-postgresql
If you are the kind of person who is looking for open source tools for data visualization. 

# Exploring Grafana with PostgreSQL: A 1-Minute Guide

I recently explored **Grafana** with **PostgreSQL**, and it’s amazing how quickly you can turn raw data into interactive dashboards. 
This mini-guide walks you through installing PostgreSQL, configuring Grafana, and getting started with your first dashboards.

---

## Requirements

Before starting, make sure you have:

- **PostgreSQL** installed and running  
- **Grafana** installed  

---

## 1. Install PostgreSQL (within a Linux system)

Install PostgreSQL and its contrib package:

```bash
sudo apt update
sudo apt install postgresql postgresql-contrib
sudo systemctl start postgresql
sudo systemctl enable postgresql
```

## 2. Create a PostgreSQL user and database for Grafana:
```bash
sudo -u postgres psql
CREATE DATABASE grafana_db;
CREATE USER grafana_user WITH ENCRYPTED PASSWORD 'your_password';
GRANT ALL PRIVILEGES ON DATABASE grafana_db TO grafana_user;
```

## 3. Configure Grafana to Use PostgreSQL
Locate your **default.ini** (usually in /etc/grafana/) and edit:

**Database section**
```bash
[database]
type = postgres
host = 127.0.0.1:5432
name = grafana_db
user = grafana_user
password = your_password
ssl_mode = disable
```

**Server section**
```bash
[server]
http_port = 3000 (or 4000 in case of a conflict)
root_url = http://localhost:3000
```

## 4. Start Grafana
Restart Grafana to apply changes:
```bash
sudo systemctl restart grafana-server
```
Open your browser at **http://localhost:3000**, log in (default: admin/admin), and start creating dashboards using SQL queries from your PostgreSQL database.
