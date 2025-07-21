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

## 🧪 Demo: Load Balance Two Local Backend Servers

📌 Scenario:
Nginx runs as a load balancer.

You have 2 Flask apps running on:

localhost:5001

localhost:5002


### ✅ Step 1: Run Flask Apps on Different Ports
📁 Create project directory:
```
mkdir -p ~/flask-loadbalance/app1 ~/flask-loadbalance/app2
```

📝 Create app.py in both folders:

app1/app.py


```
from flask import Flask
app = Flask(__name__)
z
@app.route('/')
def home():
    return "Hello from APP 1!"

if __name__ == "__main__":
    app.run(port=5001)
```

app2/app.py

```
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from APP 2!"

if __name__ == "__main__":
    app.run(port=5002)
```


Run both:

### Terminal 1
```cd ~/flask-loadbalance/app1
python3 app.py
```

### Terminal 2
```cd ~/flask-loadbalance/app2
python3 app.py
```

### ✅ Step 2: Configure Nginx as Load Balancer

📝 Edit config:

```
sudo nano /etc/nginx/sites-available/loadbalance
```

```
upstream flask_servers {
    server 127.0.0.1:5001;
    server 127.0.0.1:5002;
}

server {
    listen 80;
    server_name localhost;

    location / {
        proxy_pass http://flask_servers;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

}
```

🔗 Enable the config:
```
sudo ln -s /etc/nginx/sites-available/loadbalance /etc/nginx/sites-enabled/
sudo nginx -t
sudo systemctl reload nginx
```

### ✅ Step 3: Test the Load Balancer

Open your browser and go to:

http://localhost


Each refresh should alternate responses between:

Hello from APP 1!

Hello from APP 2!