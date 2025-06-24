```md
# 🔁 Nginx Reverse Proxy + Docker Compose System

This project sets up two backend services (Golang and Python) and routes them behind a single **Nginx reverse proxy**, all running via Docker Compose.

---

## ⚙️ Architecture Overview

```
localhost:8080
├── /service1 → Golang Service (port 8001)
└── /service2 → Python Flask Service (port 8002)
```

All traffic is routed through **Nginx**, which acts as a reverse proxy.

---

## 🐳 How to Run

### 🔧 Prerequisites

- Docker
- Docker Compose

### ▶️ One-liner to Start Everything

```bash
docker-compose up --build
```

Then visit:

- http://localhost:8080/service1/ping
- http://localhost:8080/service2/hello

---

## 🔀 Reverse Proxy Logic

Nginx handles routing based on path prefixes:

| Route Prefix  | Backend Service | Port  |
|---------------|------------------|-------|
| `/service1`   | Golang           | 8001  |
| `/service2`   | Python Flask     | 8002  |

All routes are exposed via **http://localhost:8080/**.

---

## 🩺 Health Checks

Both services expose `/ping` endpoints and are monitored via Docker healthchecks.

---

## 📁 Project Structure

```
.
├── docker-compose.yml
├── nginx/
│   ├── nginx.conf
│   └── Dockerfile
├── service_1/
│   ├── main.go
│   ├── Dockerfile
│   └── README.md
├── service_2/
│   ├── app.py
│   ├── Dockerfile
│   └── README.md
└── README.md
```

---

## 📊 Logging

Nginx logs all incoming requests with:

- Timestamp
- Request method/path
- Status code

Logs can be seen with:

```bash
docker-compose logs nginx
```

---

## 🌟 Bonus

✅ Health checks  
✅ Centralized access via reverse proxy  
✅ Clean logs  
✅ Fully Dockerized with bridge networking  
```