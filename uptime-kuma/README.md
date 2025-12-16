# Uptime Kuma + MariaDB (Docker Compose)

Production-ready deployment of **Uptime Kuma v2** with **MariaDB** using Docker Compose.

---

## 📦 Stack

* **Uptime Kuma**: `louislam/uptime-kuma:2.0.2`
* **Database**: `mariadb:10.11` (LTS)
* **Docker Compose**: v3.9

---

## 📁 Directory Structure

```
/var/uptime-kuma/my-compose/uptime-kuma
├── docker-compose.yml
├── .env
└── volumes/
```

---

## 🔐 Environment Variables

Create a `.env` file:

```env
KUMA_DB_USER=kumadbuser
KUMA_DB_PASSWORD_SECURE=kumapass
MARIADB_ROOT_PASSWORD_SECURE=rootpass
```

Secure it:

```bash
chmod 600 .env
```

---

## 🚀 Start the Stack

```bash
docker compose pull
docker compose up -d
```

Check status:

```bash
docker compose ps
docker compose logs -f uptime-kuma
```

---

## 🌐 Access Uptime Kuma

Open your browser:

```
http://<server-ip>:3001
```

You will see the **initial setup wizard**.

---

## 🗄️ Database Setup (Wizard Screen)

Fill the form **exactly** as follows:

| Field         | Value         |
| ------------- | ------------- |
| Database      | MariaDB/MySQL |
| Hostname      | `db`          |
| Port          | `3306`        |
| Username      | `kumadbuser`  |
| Password      | `kumapass`    |
| Database Name | `uptime_kuma` |

⚠️ **Do NOT use** `localhost` or `127.0.0.1`

Click **Next** → create admin user → finish setup.

---

## 🧠 Important Notes

* The hostname **must be `db`** (Docker internal DNS)
* MariaDB runs on a private Docker network (no exposed DB port)
* Persistent data is stored in Docker volumes:

  * `kuma-data`
  * `kuma-db-data`

---

## 🔄 Reset (Only If Needed)

If you want a **fresh install**:

```bash
docker compose down
docker volume rm uptime-kuma_kuma-data uptime-kuma_kuma-db-data
docker compose up -d
```

⚠️ This deletes all monitoring data.

---

## 🔒 Production Recommendations

* Put Uptime Kuma behind **Nginx + HTTPS (Let’s Encrypt)**
* Schedule **MariaDB backups**
* Restrict access via **firewall / reverse proxy**
* Monitor with **Prometheus + Grafana**

---

## ✅ Verified Working

* Docker DNS database connection
* MariaDB 10.11 LTS
* Uptime Kuma v2.0.2
* Clean startup without `127.0.0.1` DB issues

---

## 📞 Support

If you encounter issues:

```bash
docker compose logs -f uptime-kuma
docker compose logs -f db
```

Happy monitoring 🚀
