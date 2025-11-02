# Intro_to_Prometheus_Monitoring-_Collecting-_Storing-_and_Visualizing_Metrics
To demonstrate how Prometheus can monitor system performance, collect metrics, and trigger alerts, while showing integration with Grafana for visualization.

## 📸 Project Diagram "PROMETHEUS ARCHITECTURE" 
![Alt text](images/prometheus-architecture.png)

By the end of the project, you’ll:
  - Set up a full Prometheus monitoring stack.
  - Monitor your system (or containerized app).
  - Visualize data on Grafana dashboards.
  - Configure alerts with Alertmanager.



🧩 1. What is Prometheus?

Prometheus is an open-source monitoring and alerting toolkit originally built by SoundCloud.
It’s widely used in DevOps, Kubernetes, and Cloud environments to collect and query metrics.

Key Features:

- Pull-based metrics collection model.
- Powerful query language (PromQL).
- Time-series database (TSDB) built-in.
- Easy integration with Grafana and Alertmanager.