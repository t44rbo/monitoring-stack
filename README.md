# Monitoring Stack

A self-hosted monitoring solution built on a VPS running Ubuntu 24.04.

## Stack
- **Prometheus** — metrics collection (pull model)
- **Node Exporter** — host metrics via /proc
- **Grafana** — dashboards and visualization
- **Alertmanager** — alert routing to Telegram
- **Nginx** — reverse proxy, single entry point

## What it monitors
- CPU load average
- RAM usage
- Disk space (/)
- Container availability

## Quick Start

```bash
git clone https://github.com/t44rbo/monitoring-stack.git
cd monitoring-stack

# Configure secrets
cp .env.example .env
nano .env

# Set Nginx basic auth for Prometheus UI
echo "admin:$(openssl passwd -apr1 'your_password')" > nginx/.htpasswd

# Create Alertmanager config with your Telegram credentials
cp alertmanager/alertmanager.yml.example alertmanager/alertmanager.yml
nano alertmanager/alertmanager.yml

# Start
docker compose up -d
```
## Import Grafana dashboard "VPS_overview.json"
- log in to grafana GUI
- click "+" button at the top right corner
- click "Import dashboard"
- upload "VPS_overview.json"
- click "Import" button

## Access
| Service    | URL                  | Auth         |
|------------|----------------------|--------------|
| Grafana    | http://IP/grafana/   | admin + .env |
| Prometheus | http://IP/prometheus/| basic auth   |

## Project Structure
```
monitoring-stack/
├── .env                    # secrets (not in git)
├── docker-compose.yml
├── prometheus/
│   ├── prometheus.yml
│   └── alert.rules.yml
├── alertmanager/
│   └── alertmanager.yml    # not in git, contains tokens
└── nginx/
    ├── nginx.conf
    └── .htpasswd           # not in git
```
