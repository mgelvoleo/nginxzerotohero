#  ⚖️ Section 4: Load Balancing with NGINX (Ubuntu/Linux)

## 🎯 Goal
Set up NGINX to distribute incoming traffic across multiple backend servers, enhancing your application's availability, reliability, and scalability.

## 🧠 What is Load Balancing?
Load balancing is the process of distributing incoming network requests across multiple servers (backends) to ensure no single server bears too much demand.

## ✅ Key Benefits:

⚙️ Improved Performance – Distributes load evenly, avoiding server overload.

🔄 High Availability – Ensures service continuity even if one server fails.

📈 Scalability – Makes it easier to add or remove servers as demand changes.


NGINX supports several load balancing algorithms right out of the box, including:

| Algorithm         | Behavior                                                               |
|-------------------|-------------------------------------------------------------------------|
| `round-robin`     | Default — rotates through all backends equally                         |
| `least_conn`      | Sends traffic to the backend with the fewest active connections         |
| `ip_hash`         | Uses client IP to consistently route requests to the same backend       |


---

## 📝 Basic Load Balancer Configuration

Edit:
```bash
sudo nano /etc/nginx/sites-available/default
```

Replace contents with:

```nginx
upstream backend_app {
    server 127.0.0.1:3001;
    server 127.0.0.1:3002;
}

server {
    listen 80;
    server_name localhost;

    location / {
        proxy_pass http://backend_app;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

---
