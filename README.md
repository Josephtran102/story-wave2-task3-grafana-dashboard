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
- Download and install Prometheus:
```bash
cd $HOME
wget https://github.com/prometheus/prometheus/releases/download/v2.42.0/prometheus-2.42.0.linux-amd64.tar.gz
tar xvf prometheus-2.42.0.linux-amd64.tar.gz
sudo cp prometheus-2.42.0.linux-amd64 /opt/prometheus
```
- Create Prometheus user:
```bash
sudo useradd --no-create-home --shell /bin/false prometheus
```
- Create necessary directories:
```
sudo mkdir /etc/prometheus
sudo mkdir /var/lib/prometheus
sudo touch /etc/default/prometheus
```
- Configure permissions:
```bash
sudo chown prometheus:prometheus /etc/prometheus
sudo chown prometheus:prometheus /var/lib/prometheus
sudo chown -R prometheus:prometheus /opt/prometheus
sudo chown -R prometheus:prometheus /etc/prometheus
sudo chown -R prometheus:prometheus /var/lib/prometheus
sudo chmod 755 /opt/prometheus/prometheus
```
- Create Prometheus configuration file:
```
sudo nano /etc/prometheus/prometheus.yml
```
[Insert Prometheus configuration content from the original post]
- Create service file:
```bash
sudo nano /lib/systemd/system/prometheus.service
```
[Insert service file content from the original post]
- Start Prometheus:
```
sudo systemctl daemon-reload
sudo systemctl enable prometheus
sudo systemctl restart prometheus
```
### 2. Installing Node Exporter
Node Exporter collects hardware and OS metrics.
- Download and install Node Exporter:
```
cd ~
wget https://github.com/prometheus/node_exporter/releases/download/v1.5.0/node_exporter-1.5.0.linux-amd64.tar.gz
tar xvf node_exporter-1.5.0.linux-amd64.tar.gz
sudo cp node_exporter-1.5.0.linux-amd64/node_exporter /usr/local/bin/
```
- Create service file:
```
sudo nano /etc/systemd/system/node_exporter.service
```
[Insert service file content from the original post]

c) Start Node Exporter:
```
chmod +x /root/node_exporter-1.5.0.linux-amd64/node_exporter
systemctl daemon-reload
sudo systemctl enable node_exporter
systemctl restart node_exporter
```
### 3. Installing Grafana
Grafana is an open-source platform for data analytics and visualization.
- Install Grafana:
```bash
sudo apt-get install -y software-properties-common
sudo add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
wget -q -O - https://packages.grafana.com/gpg.key | sudo apt-key add -
sudo apt-get update
sudo apt-get install grafana
sudo systemctl enable grafana-server
```
- Start Grafana:
```
sudo systemctl restart grafana-server
```
### 4. Configuring Grafana Dashboard
- Access Grafana web interface:
Open your browser and navigate to http://your_server_ip:3000
Default login: admin/admin
b) Add Prometheus as a data source:

Click "Add new data source" and select Prometheus
Enter http://localhost:9099 as the Prometheus server URL
Click "Save & Test" at the bottom

- Import Dashboard:

Go to Dashboards and click "Upload JSON file"
Download the 0G-grafana-json-file from https://josephtran.co/0g_validator.json
Upload the downloaded JSON file
Select the Prometheus data source you just added

- Customize Dashboard:

Adjust time ranges, add new panels, or modify existing ones as needed

### 5. Troubleshooting

If Prometheus fails to start, check the configuration file for syntax errors
Ensure all necessary ports are open in your firewall
Check service logs using journalctl -u [service_name] for any error messages

### 6. Maintenance

Regularly update Prometheus, Node Exporter, and Grafana to their latest versions
Backup your Grafana dashboards and Prometheus data periodically
Monitor disk usage of the Prometheus data directory

Conclusion
You now have a fully functional monitoring system for your node. This setup allows you to visualize system metrics, set up alerts, and gain insights into your node's performance. Remember to regularly check and update your monitoring setup to ensure it remains effective and secure.

This comprehensive guide should provide a solid foundation for setting up Grafana to monitor your node. It covers all the necessary steps from installation to configuration, and includes some basic troubleshooting and maintenance tips.
