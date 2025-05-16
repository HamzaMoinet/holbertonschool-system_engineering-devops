# Secured and Monitored Web Infrastructure

## Infrastructure Design
The web infrastructure consists of three servers, a load balancer, firewalls, SSL encryption, and monitoring tools. Below is the design:

1. **Load Balancer**: HAProxy to distribute traffic between two servers.
2. **Two Servers**:
   - **Web Server (Nginx)**: Handles HTTP/HTTPS requests and serves static files.
   - **Application Server**: Processes dynamic requests and runs the application code.
   - **Application Files**: The codebase for the website.
   - **Database**: MySQL configured in a Primary-Replica (Master-Slave) setup.
3. **Firewalls**: Three firewalls to filter incoming and outgoing traffic.
4. **SSL Certificate**: To serve traffic over HTTPS.
5. **Monitoring Clients**: Installed on all servers to collect metrics and logs for monitoring.

---

## Explanation of Components

### Firewalls
- **Why Add Them**: To protect the infrastructure by filtering malicious traffic and restricting access to specific ports.
- **Role**:
  - Blocks unauthorized access.
  - Allows only necessary traffic (e.g., HTTP/HTTPS on ports 80/443, SSH on port 22).
  - Prevents DDoS attacks and other threats.

### SSL Certificate
- **Why Add It**: To encrypt traffic between the user's browser and the server, ensuring data confidentiality and integrity.
- **Role**:
  - Protects sensitive information (e.g., login credentials).
  - Improves user trust and SEO rankings.

### Monitoring Clients
- **Why Add Them**: To collect metrics and logs for real-time monitoring and troubleshooting.
- **Role**:
  - Tracks server performance (CPU, memory, disk usage).
  - Monitors web server QPS (queries per second).
  - Detects anomalies and sends alerts.
- **How It Works**: Monitoring clients (e.g., Sumologic agents) collect data and send it to a centralized monitoring service for analysis.

---

## Issues with This Infrastructure

1. **SSL Termination at the Load Balancer**:
   - If SSL is terminated at the load balancer, traffic between the load balancer and backend servers is unencrypted, exposing sensitive data.
   - Solution: Use end-to-end encryption by enabling SSL on backend servers as well.

2. **Single MySQL Server for Writes**:
   - Having only one MySQL server capable of accepting writes creates a bottleneck and a single point of failure.
   - Solution: Implement a multi-primary setup or use database clustering for high availability.

3. **Servers with All Components**:
   - Combining the database, web server, and application server on the same machine can lead to resource contention.
   - Solution: Separate these components onto dedicated servers for better scalability and performance.

---

## Monitoring Web Server QPS
To monitor the web server's QPS:
1. Install a monitoring client (e.g., Sumologic, Prometheus) on the web server.
2. Configure the client to collect Nginx logs or metrics.
3. Use a centralized monitoring dashboard to visualize QPS in real-time.

---

## Diagram of the Infrastructure

```mermaid
graph TD
    Internet[Internet]
    FW1[Firewall #1]
    LB1[HAProxy + SSL LB1]
    FW2[Firewall #2]
    FW3[Firewall #3]
    ServerA[Server A]
    ServerB[Server B]
    NginxA[Nginx]
    NginxB[Nginx]
    AppA[App Server]
    AppB[App Server]
    DB1[MySQL Primary]
    DB2[MySQL Replica]
    MonA[Monitoring Agent A]
    MonB[Monitoring Agent B]
    MonLB[Monitoring Agent LB]
    Sumo[Sumologic/Monitoring Platform]

    Internet --> FW1 --> LB1
    LB1 --> FW2 --> ServerA
    LB1 --> FW3 --> ServerB
    ServerA --> NginxA --> AppA --> DB1
    ServerB --> NginxB --> AppB --> DB2
    DB1 <--> DB2

    MonLB --> Sumo
    MonA --> Sumo
    MonB --> Sumo
```
