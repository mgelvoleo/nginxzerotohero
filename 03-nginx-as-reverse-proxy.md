# 🔁 Section 3: NGINX as a Reverse Proxy (Ubuntu/Linux)

## 🧠 What is a Reverse Proxy?

A **reverse proxy** is a server that receives client requests and forwards them to backend servers, then sends the response back to the client.

NGINX is one of the most popular tools used as a reverse proxy in production.

---

## 🔄 Reverse Proxy vs Forward Proxy

| Feature         | Forward Proxy                       | Reverse Proxy                           |
|-----------------|--------------------------------------|------------------------------------------|
| Who configures it | Client                              | Server-side                              |
| Forwards requests to | External servers (internet)         | Internal backend servers (apps/services) |
| Use case         | Browsing anonymously, caching       | Load balancing, SSL termination, API gateway |
| Example          | Proxy server for office users       | NGINX between frontend and backend apps  |

---

## 📌 Why Use NGINX as a Reverse Proxy?

- Protect backend services from direct access
- Centralized SSL termination
- Load balancing backend apps
- Path-based routing (`/api` → backend1, `/app` → backend2)
- Easy caching and compression

---

## 📝 Reverse Proxy Configuration (Ubuntu/Linux)

### 🔧 File: `/etc/nginx/sites-available/default`

Update the existing `server` block or create a new one:

```nginx
server {
    listen 80;
    server_name localhost;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

### Breakdown:
- `proxy_pass` → forwards requests to your backend app
- `proxy_set_header` → preserves original request metadata (like IP and host)

---