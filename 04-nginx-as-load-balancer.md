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