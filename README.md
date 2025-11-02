# Intro_to_Prometheus_Monitoring-_Collecting-_Storing-_and_Visualizing_Metrics
To demonstrate how Prometheus can monitor system performance, collect metrics, and trigger alerts, while showing integration with Grafana for visualization.

## 📸 Project Diagram "PROMETHEUS ARCHITECTURE" 
![Alt text](images/prometheus-architecture.png)

By the end of the project, you’ll:
   - Set up a full Prometheus monitoring stack.
   - Monitor your system (or containerized app).
   - Visualize data on Grafana dashboards.
   - Configure alerts with Alertmanager.

## 🏗️ 1. System Architecture Overview

### Monitoring key components and description:
1. `Metrics:` Monitoring is all about collecting and gathering matrics. Metrics are numeric data about system/app performance (e.g., CPU utilization, memory usage, request count). `So matrics basically provide data on the performance of your system`
2. `log`: Are detailed records of events that happen inside your system, application, or infrastructure. (e.g., Like in serverless computing we check the logs with CloudWatch log). Every time a server, container, or app performs an action, it can write a line to a log file.
    * Help debug errors or performance problems.
    * Provide a history of events (what happened and when).
    * Show the context of issues that metrics alone can’t reveal.
3. `Alerts`: It's how you notify your user when a threshold is met. Alerts are `automated notifications` triggered when metrics or conditions meet certain rules. (e.g., “If CPU usage > 80% for more than 2 minutes, send an alert.”).
    * They help detect problems early before they become outages.
    * Notify you when something is wrong (high latency, low memory, failed service, etc.).
    * Enable proactive monitoring — respond before users notice issues.
4. 
 

### Main components and description:

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