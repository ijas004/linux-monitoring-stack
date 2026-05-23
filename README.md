# Linux Server Monitoring Stack
## Prometheus | Grafana | Alertmanager | Node Exporter | AWS EC2

A production-grade infrastructure monitoring system built on AWS EC2
using industry-standard open-source tools — same stack used by 
companies like Netflix, Uber and Google.

---

## Project Architecture

- **Target Server** (EC2 t2.micro · Ubuntu 24.04) — server being 
  monitored, running Nginx + Node Exporter
- **Monitoring Server** (EC2 t2.micro · Ubuntu 24.04) — runs 
  Prometheus, Grafana and Alertmanager

---

## Tools Used & Why

| Tool | Purpose |
|------|---------|
| Prometheus | Collects and stores metrics every 15 seconds |
| Node Exporter | Exposes Linux CPU, memory, disk, network metrics |
| Grafana | Visualizes metrics as real-time dashboards |
| Alertmanager | Sends email alerts when thresholds are breached |
| AWS EC2 | Cloud servers (free tier) |
| Nginx | Web server running on target server |
| Bash | Stress test script to trigger CPU alerts |

---

## How It Works

1. Node Exporter runs on target server and collects system metrics
2. Prometheus scrapes those metrics every 15 seconds
3. Prometheus evaluates alert rules continuously
4. If CPU goes above 70% for 1 minute — alert fires
5. Alertmanager receives alert and sends email via Gmail SMTP
6. Grafana pulls data from Prometheus and shows live dashboards

---

## Alert Rules Configured

- **HighCPUUsage** — fires when CPU > 70% for 1 minute
- **HighMemoryUsage** — fires when memory > 80% for 1 minute
- **InstanceDown** — fires immediately when server goes offline

---

## Screenshots

### Grafana Dashboard — CPU at 100% during stress test
![Grafana CPU 100%](screenshots/grafana-cpu-100.png)

### Prometheus Alert Firing at 93.82% CPU
![Prometheus Firing](screenshots/prometheus-firing.png)

### Gmail Alert Email Received
![Gmail Alert](screenshots/gmail-alert.png)

### Nginx Web Server Running on Target Server
![Nginx](screenshots/nginx-welcome.png)

### Node Exporter Metrics Page
![Node Exporter](screenshots/node-exporter-metrics.png)

---

## Key Commands Used

```bash
# Install and start Node Exporter on target server
sudo systemctl start node_exporter
sudo systemctl enable node_exporter

# Install and start Prometheus on monitoring server
sudo systemctl start prometheus
sudo systemctl enable prometheus

# Install and start Grafana
sudo systemctl start grafana-server
sudo systemctl enable grafana-server

# Install and start Alertmanager
sudo systemctl start alertmanager
sudo systemctl enable alertmanager

# Trigger CPU stress test to demonstrate alerting
stress --cpu 4 --timeout 180s
```

---

## Result

- CPU stress test pushed usage to **100%**
- Prometheus alert fired at **93.82% CPU**
- Email alert received in Gmail within **2 minutes**
- Grafana dashboard showed real-time CPU spike graph

---

## Skills Demonstrated

- Linux server administration (Ubuntu 24.04)
- AWS EC2 instance management and security groups
- Prometheus metrics collection and PromQL alert rules
- Grafana dashboard import and configuration (Dashboard ID: 1860)
- Alertmanager email notification setup via Gmail SMTP
- Systemd service management
- Bash scripting
