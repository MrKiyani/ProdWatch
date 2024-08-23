# Monitoring Production Services

This project is a comprehensive monitoring solution for production services using Prometheus, Grafana, Loki, and Alertmanager. It includes custom alerting rules and website monitoring configurations.

## Project Structure

```
├── blackbox_exporter
│   └── blackbox.yml
├── loki
│   ├── docker-compose.yml
│   └── loki-config.yaml
├── alert_rules.yml
├── alertmanager.yml
├── docker-compose.yml
└── prometheus.yml
```

## Components

1. **Prometheus**: Collects metrics from various targets and stores them. Configured to scrape metrics from different servers and services.
2. **Alertmanager**: Handles alerts sent by Prometheus, managing notifications through email.
3. **Grafana**: Provides a dashboard for visualizing data from Prometheus.
4. **Loki**: A log aggregation system that works with Grafana to enable log querying and monitoring.
5. **Blackbox Exporter**: Probes endpoints such as HTTP services to ensure they are reachable and performing as expected.

## Prerequisites

- Docker
- Docker Compose

## Deployment

### Step 1: Clone the Repository

```bash
git clone https://github.com/mrkiyani/monitoring-prod-services.git
cd monitoring-prod-services
```

### Step 2: Configure Environment

Ensure all the necessary configurations are in place. Update email addresses and server IPs in the `alertmanager.yml` and `prometheus.yml` files as needed.

### Step 3: Start the Services

```bash
docker-compose up -d
```

This command will start Prometheus, Grafana, Alertmanager, and Blackbox Exporter.

For Loki, navigate to the `loki` directory and run:

```bash
docker-compose up -d
```

### Step 4: Access the Services

- **Prometheus**: [http://localhost:9090](http://localhost:9090)
- **Grafana**: [http://localhost:3000](http://localhost:3000) (Default credentials: `admin/admin`)
- **Alertmanager**: [http://localhost:9093](http://localhost:9093)
- **Loki**: [http://localhost:3100](http://localhost:3100)

### Step 5: Configure Grafana

1. Log in to Grafana.
2. Add Prometheus as a data source: `http://prometheus:9090`.
3. Add Loki as a data source: `http://loki:3100`.
4. Import dashboards or create custom dashboards to visualize your metrics and logs.

## Custom Alerting Rules

The alerting rules are defined in `alert_rules.yml`. These include:

- **Container Monitoring**: Alerts when a container is down.
- **Host Monitoring**: Alerts for high CPU, RAM, or disk usage, and when instances are unreachable.
- **Website Monitoring**: Alerts if the monitored websites are down.

## Blackbox Exporter Configuration

The Blackbox Exporter configuration in `blackbox.yml` defines the probing modules, such as `http_2xx`, to check for successful HTTP responses from the specified endpoints.

## Loki Configuration

Loki’s configuration is stored in `loki/loki-config.yaml`. This setup includes ingester and storage configurations, schema settings, and retention policies.

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

---