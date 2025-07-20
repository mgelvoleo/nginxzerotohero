# 🌐 Section 2: NGINX as a Web Server
🚀 Goal
Learn how to configure NGINX to serve static content such as HTML, CSS, JavaScript, and images — a fundamental skill for DevOps and Cloud Engineers.

# 🧠 What Is a Web Server?
A web server is software that delivers static files (like .html, .css, .js, .png) over the HTTP protocol.
When a user visits your website, the web server responds with the appropriate files from its directory.

NGINX is one of the most popular and high-performance web servers used to deliver this content efficiently.
---

# 📁 Default Web Root in Linux

Directory	Purpose
/var/www/html/	Default location for static web files
/etc/nginx/sites-available/default	Default configuration file pointing to the web root

# 📝 Anatomy of a Basic server Block

```
server {
    listen 80;
    server_name localhost;

    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

---

# 🔍 Breakdown:

listen 80; → Tells NGINX to listen on HTTP port 80

server_name localhost; → Responds to requests for this domain or IP

root /var/www/html; → Directory where static files are served from

index index.html; → Default file to serve when a directory is requested

location / { ... } → Handles requests for the root URL (/), serving files or returning 404 if not found


---

# 🎁 Bonus: Setting Up a Custom Virtual Host
You can create multiple websites on a single server using virtual hosts. Here’s how to configure one for www.virtual.host.

# 📄 Step 1: Create a New Virtual Host Configuration
Edit or create a new config file:

```
sudo vi /etc/nginx/sites-available/virtual.host.conf

```

Add the following content:

```

server {
    listen       80;
    server_name  www.virtual.host;

    location / {
        root   /var/www/virtual.host;
        index  index.html index.htm;
    }
}


```



# 📁 Step 2: Create the Web Root Directory

```
sudo mkdir -p /var/www/virtual.host
```

You can now add your index.html or other static files in this directory.


# Step 3: Enable the Virtual Host

Create a symbolic link from sites-available to sites-enabled:

```
cd /etc/nginx/sites-enabled
sudo ln -s /etc/nginx/sites-available/virtual.host.conf ./

```

# 🔄 Step 4: Reload NGINX to Apply Changes

```
sudo systemctl reload nginx
```

# 🧠 Bonus Tip:
If you're testing locally, make sure to map www.virtual.host in your /etc/hosts file:


```
sudo vi /etc/hosts
```

Add this line:


```
127.0.0.1   www.virtual.host
```

---

# ✅ Summary
NGINX is highly efficient at serving static content like HTML, CSS, and JavaScript.

The root and index directives specify where to find files and which file to serve first.

You can use Docker volumes to serve content without modifying the host system.

Always reload NGINX (nginx -s reload or systemctl reload nginx) after updating configuration files to apply changes.