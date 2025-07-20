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


# 🧪 Demo: Reverse Proxy to a python flask App

## ✅ Step 1: Install Dependencies

📍 On Ubuntu/Debian:

## ✅ Step 2: Create and Run a Flask App

📁 1. Create a directory:

```
mkdir ~/flask-app
cd ~/flask-app
```

2. Create the app file:

```
vi app.py
```

Paste this basic Flask code:

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def hello():
    return "Hello from Flask behind Nginx!"

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=5000)


```

## 📦 3. Install Flask:

```pip3 install flask```

## ▶️ 4. Run the app:
```
python3 app.py
```

Check: Open browser and go to http://your_server_ip:5000


## ✅ Step 5: Configure Nginx as Reverse Proxy
📝 Create Nginx config file:
```
sudo nano /etc/nginx/sites-available/flask-app
```

Paste the following:

```
server {
    listen 80;
    server_name your_domain_or_ip;

    location / {
        proxy_pass http://127.0.0.1:5000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```

## 🔗 Enable the config:

```
sudo ln -s /etc/nginx/sites-available/flask-app /etc/nginx/sites-enabled/ 
```

### ✔️ Test and reload Nginx:

```
sudo nginx -t
sudo systemctl reload nginx
```

Now, going to http://your_domain_or_ip will show the Flask app.