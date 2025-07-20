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