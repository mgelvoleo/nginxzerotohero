

#  📘 Section 1: Introduction to NGINX

NGINX (pronounced “engine-x”) is a powerful, open-source web server trusted by millions of websites worldwide. But it's more than just a web server — it’s a versatile tool built for speed, efficiency, and scalability.

NGINX can serve as:

- 🔁 **Reverse Proxy** – Routes client requests to backend servers
    
- ⚖️ **Load Balancer** – Distributes traffic evenly across multiple servers
    
- 📦 **HTTP Cache** – Improves performance by storing copies of content
    
- 📧 **Mail Proxy** – Handles IMAP, POP3, and SMTP traffic
    

Designed for **high concurrency**, **low resource usage**, and **maximum performance**, NGINX is a go-to choice for modern DevOps workflows, cloud-native environments, and scalable web infrastructure.

---

## Reverse Proxy


![[reverseproxy.png]]


## 📊 NGINX vs Apache: Why DevOps Prefer NGINX

|**Feature**|**NGINX**|**Apache**|
|---|---|---|
|**Architecture**|Event-driven (asynchronous)|Process/thread-based|
|**Performance**|Handles high concurrency efficiently|Slower under heavy load|
|**Memory Usage**|Lightweight and efficient|Higher memory consumption|
|**Static Content**|Extremely fast|Decent, but not as optimized|
|**Config Format**|Simple and declarative|Flexible but more complex|
|**Common Use Cases**|Web server, reverse proxy, load balancer|Primarily a traditional web server|

### 💡 Why DevOps Engineers Prefer NGINX

- 🚀 **Lightweight and high-performance** — perfect for scalable systems
    
- ⚙️ **Easy to automate** — fits seamlessly with CI/CD pipelines
    
- 🐳 **Docker & Kubernetes-friendly** — ideal for containerized environments

## 🧰 Common DevOps Use Cases for NGINX

|**Use Case**|**Example**|
|---|---|
|**Web Server**|Hosting static sites and frontend apps (e.g., React, Angular)|
|**Reverse Proxy**|Routing traffic to backend services (Node.js, Python, Java, etc.)|
|**Load Balancer**|Distributing requests across multiple backend servers for high availability|
|**SSL Termination**|Handling HTTPS connections and offloading SSL/TLS from backend apps|
|**Caching**|Storing frequently accessed responses to reduce backend load|
|**Ingress Controller (Kubernetes)**|Managing external access to services inside a Kubernetes cluster|
|**Rate Limiting & Security**|Protecting APIs from abuse, brute force attacks, or bots|

### 💡 NGINX plays a key role in building secure, scalable, and high-performing DevOps infrastructures.


---

## 🛠️ Installing NGINX

### 🐧 On Ubuntu/Debian

```shell
sudo apt update
sudo apt install nginx -y
```


### 🐳 Using Docker 

```shell
docker run --name nginx -p 8080:80 -d nginx
```

Visit: `http://localhost:8080`


## 📁 NGINX File Structure in Linux

|**File/Directory**|**Purpose**|
|---|---|
|`/etc/nginx/nginx.conf`|Main NGINX configuration file|
|`/etc/nginx/sites-available/`|Stores configuration files for individual sites (server blocks)|
|`/etc/nginx/sites-enabled/`|Contains symlinks to active site configurations|
|`/var/www/html/`|Default web root directory for serving static content|
|`/var/log/nginx/`|Location of NGINX access and error logs|

### 🧠 Tip: Use `sites-available` to manage your configs and enable them with symlinks in `sites-enabled`.


## 🎯 Summary

- **NGINX** is a fast, lightweight, and high-performance web server and reverse proxy.
    
- It’s widely adopted in **DevOps** for tasks like load balancing, SSL termination, and traffic routing.
    
- Easy to install via **Linux package managers** or **Docker** containers.
    
- Supports **modular, declarative configuration** — making it ideal for automation, scripting, and CI/CD pipelines.
