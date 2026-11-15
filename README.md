# Fintech & Cloud Engineering Lab

**Anis Ahmed** · MEng Electronic Engineering, King's College London (graduating 2027)
[LinkedIn](https://www.linkedin.com/in/anis-ahmed-tech) · [GitHub](https://github.com/anisahm47)

A hands-on lab where I taught myself cloud engineering by building a small market-data pipeline end to end: Python, Docker, PostgreSQL, AWS and Terraform.

---

## Featured project: BTC market-data pipeline (`05_data_pipeline`)

A containerised Python service that collects the live BTC/USDT price from the Binance REST API every 30 seconds and stores it in PostgreSQL for analysis.

**How it works**
- `pipeline.py` requests the latest price from Binance (10-second timeout), and if a valid price comes back, inserts it into a `price_history` table.
- API and database errors are caught and logged, so one failed request doesn't stop the loop.
- The database password is not stored in the code: the service fetches it at startup from **AWS SSM Parameter Store** (encrypted).
- `docker-compose.yml` runs the bot and PostgreSQL as separate containers, both with `restart: always`, so a crash restarts automatically.
- Deployed and run on an **AWS EC2** instance in **eu-west-2 (London)**.

**Tech:** Python (requests, psycopg2, boto3) · Docker & Docker Compose · PostgreSQL · AWS (EC2, RDS, SSM, S3) · Terraform · Linux

---

## Infrastructure as code (Terraform)

| Folder | What it provisions |
|---|---|
| `07_terraform_basics` | S3 bucket (first Terraform exercise) |
| `08_cloud_compute` | Ubuntu EC2 instance with SSH key and firewall; Docker installed automatically on boot via `user_data` |
| `09_cloud_database` | PostgreSQL 15 on AWS RDS (free-tier instance) |

---

## Learning path

| Folder | Focus |
|---|---|
| `01_btc_ticker` | First containerised price ticker |
| `02_python_drills` | Python practice: transactions, simple fraud rules, a more robust ticker |
| `03_api_drills` | Working with REST APIs (exchange rates) |
| `04_db_integration` | SQL schema and queries in PostgreSQL |
| `05_data_pipeline` | The featured pipeline above |
| `07`–`09` | Terraform: S3, EC2, RDS |

---

## What I'd improve next

This was built as a learning project, so some settings are deliberately simple. Next steps:
- Move every credential into SSM or environment variables (some Terraform/Compose files still use placeholder passwords).
- Lock down security groups to my own IP and make the RDS instance private rather than publicly accessible.
- Add data validation, e.g. rejecting prices outside a sensible range.
- Switch from polling the REST API to Binance's WebSocket stream for real-time updates.
