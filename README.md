# Prometheus and Grafana Setup Guide

![Prometheus Logo](https://cdn.jsdelivr.net/gh/prometheus/prometheus/documentation/images/prometheus-logo.png)

![Grafana Logo](https://raw.githubusercontent.com/grafana/grafana/main/public/img/grafana_icon.svg)

This guide provides step-by-step instructions to download and set up Prometheus and Grafana on your system.

## Prerequisites

- A Linux-based system (Ubuntu/Debian/CentOS preferred) or a Windows system with WSL.
- Basic knowledge of terminal commands.
- `wget` or `curl` for downloading files (Linux/WSL).
- Administrator/root privileges.

---

## Step 1: Download Prometheus

### For Linux:
1. Navigate to the [Prometheus download page](https://prometheus.io/download/):
   ```bash
   wget https://github.com/prometheus/prometheus/releases/latest/download/prometheus-*.linux-amd64.tar.gz
   ```

2. Extract the downloaded tar file:
   ```bash
   tar -xvf prometheus-*.linux-amd64.tar.gz
   ```

3. Move Prometheus to a directory for system-wide use:
   ```bash
   sudo mv prometheus-* /usr/local/bin/prometheus
   ```

4. Verify installation:
   ```bash
   prometheus --version
   ```

### For Windows:
1. Download the Prometheus `.zip` file from the [Prometheus download page](https://prometheus.io/download/).
2. Extract the file to a preferred directory.
3. Run Prometheus using the `prometheus.exe` file.

---

## Step 2: Download Grafana

### For Linux:
1. Navigate to the [Grafana download page](https://grafana.com/grafana/download):
   ```bash
   wget https://dl.grafana.com/enterprise/release/grafana-enterprise-*.linux-amd64.tar.gz
   ```

2. Extract the downloaded tar file:
   ```bash
   tar -xvf grafana-enterprise-*.linux-amd64.tar.gz
   ```

3. Move Grafana to a directory for system-wide use:
   ```bash
   sudo mv grafana-* /usr/local/bin/grafana
   ```

4. Verify installation:
   ```bash
   grafana-server -v
   ```

### For Windows:
1. Download the Grafana `.zip` file from the [Grafana download page](https://grafana.com/grafana/download).
2. Extract the file to a preferred directory.
3. Run Grafana using the `grafana-server.exe` file.

---

## Step 3: Start Services

### Prometheus:
1. Create a `prometheus.yml` configuration file in the extracted directory.
   Example configuration:
   ```yaml
   global:
     scrape_interval: 15s

   scrape_configs:
     - job_name: 'prometheus'
       static_configs:
         - targets: ['localhost:9090']
   ```

2. Start Prometheus:
   ```bash
   ./prometheus --config.file=prometheus.yml
   ```

### Grafana:
1. Start Grafana:
   ```bash
   ./grafana-server
   ```
2. Access Grafana at: `http://localhost:3000`
   - Default username: `admin`
   - Default password: `admin`

---

## Step 4: Integrate Prometheus with Grafana

1. Log in to Grafana.
2. Navigate to **Configuration > Data Sources > Add Data Source**.
3. Select **Prometheus**.
4. Enter Prometheus URL: `http://localhost:9090`.
5. Click **Save & Test**.

---

## Step 5: Visualize Metrics
1. Create a new dashboard in Grafana.
2. Add panels and select Prometheus as the data source.
3. Use Prometheus queries (e.g., `up`, `node_cpu_seconds_total`) to visualize metrics.

---

## Troubleshooting

- Ensure Prometheus is running on `localhost:9090`.
- Ensure Grafana is running on `localhost:3000`.
- Check firewall settings if accessing Grafana or Prometheus remotely.

---

Congratulations! You have successfully set up Prometheus and Grafana for monitoring and visualization.
