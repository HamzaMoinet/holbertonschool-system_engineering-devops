# 3. Scale Up

This document outlines a scalable infrastructure by separating components and adding redundancy.

---

## ⚙️ Diagram

```mermaid
graph TD
    Internet[Internet]
    LB1[Load Balancer #1]
    LB2[Load Balancer #2]
    Web1[Web Server A Nginx]
    Web2[Web Server B Nginx]
    App1[App Server A]
    App2[App Server B]
    App3[App Server C New]
    DB[MySQL Primary]

    Internet --> LB1
    LB1 --> LB2
    LB2 --> Web1
    LB2 --> Web2
    Web1 --> App1
    Web2 --> App2
    Web2 --> App3
    App1 --> DB
    App2 --> DB
    App3 --> DB
```

---

## 💡 Explanation

### Why Add These Components?

- **Second Load Balancer**: Removes single point of failure.
- **New App Server**: Scales dynamic processing capacity.
- **Split Roles**: Web, App, DB on separate machines increases manageability.

---

## 📘 Application Server vs Web Server

| Web Server (Nginx)        | Application Server          |
|---------------------------|-----------------------------|
| Handles static files, HTTP| Runs backend logic (e.g. API)|
| Reverse proxy             | Processes dynamic content    |

---

This architecture improves scalability and fault tolerance while clearly separating system concerns.
