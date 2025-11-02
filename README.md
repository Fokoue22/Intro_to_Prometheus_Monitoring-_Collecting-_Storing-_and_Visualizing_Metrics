# Intro_to_Prometheus_Monitoring-_Collecting-_Storing-_and_Visualizing_Metrics
To demonstrate how Prometheus can monitor system performance, collect metrics, and trigger alerts, while showing integration with Grafana for visualization.

## 📸 Project Diagram "PROMETHEUS ARCHITECTURE" 
![Alt text](images/prometheus-architecture.png)

By the end of the project, you’ll:
    - Set up a full Prometheus monitoring stack.
    - Monitor your system (or containerized app).
    - Visualize data on Grafana dashboards.
    - Configure alerts with Alertmanager.

🏗️ 1. System Architecture Overview

Main components and description:

1. Prometheus Server: Core component that scrapes metrics and stores them in a time-series database.
2. Exporters: Small agents that expose metrics (e.g., node_exporter for system metrics, app-specific exporters).
3. Pushgateway: Receives metrics from short-lived jobs that can’t be scraped directly.
4. Service Discovery: Automatically finds what to monitor (e.g., Kubernetes, EC2 instances).
5. Alertmanager: Handles alerts (e.g., send email, Slack, PagerDuty).
6. Grafana: Visualization dashboard for Prometheus metrics.

🧩 1. What is Prometheus?

Prometheus is an open-source monitoring and alerting toolkit originally built by SoundCloud.
It’s widely used in DevOps, Kubernetes, and Cloud environments to collect and query metrics.

Key Features:

- Pull-based metrics collection model.
- Powerful query language (PromQL).
- Time-series database (TSDB) built-in.
- Easy integration with Grafana and Alertmanager.