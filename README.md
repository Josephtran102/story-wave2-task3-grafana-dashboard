<img src="assests/grafa-banner.png" alt="Grafa banner" style="width: 100%; height: 100%; object-fit: cover;" />

# Guide to Setting Up Grafana Dashboard for Node Monitoring
## Overview
To set up an effective node monitoring system, we'll use three main tools:

1. Prometheus: Collects and stores metrics.
2. Node Exporter: Gathers metrics from the system and hardware.
3. Grafana: Displays data in graphs and dashboards.

## System Requirements

- Operating System: Ubuntu 20.04 LTS or newer
- RAM: Minimum 2GB
- CPU: 2 cores or more
- Disk Space: At least 20GB free

## Implementation Steps

### 1. Installing Prometheus
Prometheus is an open-source monitoring system and time series database.
#### a) Download and install Prometheus:
```bash
cd $HOME
wget https://github.com/prometheus/prometheus/releases/download/v2.42.0/prometheus-2.42.0.linux-amd64.tar.gz
tar xvf prometheus-2.42.0.linux-amd64.tar.gz
sudo cp prometheus-2.42.0.linux-amd64 /opt/prometheus
```
