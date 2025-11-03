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
2. `log`: Are detailed `records of events` that happen inside your system, application, or infrastructure. (e.g., Like in serverless computing we check the logs with CloudWatch log). Every time a server, container, or app performs an action, it can write a line to a log file.
    * Help debug errors or performance problems.
    * Provide a history of events (what happened and when).
    * Show the context of issues that metrics alone can’t reveal.
3. `Alerts`: It's how you notify your user when a threshold is met. Alerts are `automated notifications` triggered when metrics or conditions meet certain rules. (e.g., “If CPU usage > 80% for more than 2 minutes, send an alert.”).
    * They help detect problems early before they become outages.
    * Notify you when something is wrong (high latency, low memory, failed service, etc.).
    * Enable proactive monitoring — respond before users notice issues.
4. `Dashboards`: Is the visual representation of you metrics (e.g., “Just like a security guy with big monitor and bunch of cameras able to see everything that happen in the building.”). Dashboards are `visual interfaces` that display key performance metrics in `real time`
    * Provide a quick overview of the system.
    * Allow correlation between metrics (e.g., traffic spike → CPU spike → error rate increase).
 
#### In a complete monitoring setup, they’re connected like this:
- Metrics (Prometheus) → collected continuously.
- Dashboards (Grafana) → visualize metrics.
- Alerts (Alertmanager) → trigger notifications on anomalies.
- Logs (Loki/ELK) → used to investigate what caused the issue.

So the workflow is:

Dashboard shows a problem → Alert is triggered → You check logs → You fix the root cause.



## 🧩 2. What is Prometheus?

`Prometheus` is an open-source monitoring and alerting tool originally built by `SoundCloud`. 
   * It’s widely used in DevOps, Kubernetes, and Cloud environments to collect and query metrics.
   * What makes it different is that it collects and stores its metrics as tme series data. i.e. metrics information is stored with the timestamp at which it was recorded, alongside optional `key-value pairs`(because metrics you have alot of data so it makes it flexibility to access that data with programming language like `Python or Java`) called labels

### Key Features:
- `Multi-dimensional Data Model`: Prometheus is flexible because it store it data as a `key-value pairs`. So users have the possibility to associate `labels` to the data that they get and make it easy to analyse the data. 
- `Data Scraping`: Here, Prometheus will ask EC2 (e.g., what is the CPU) at this time then collect the data called matrics and send them back. SO prometheus will be like a `server` and the target system will be the `client`. 
- `Powerful query language (PromQL)`: This language allow you to manipulate, query, to retrieve and analyze `time series data` that are store on the Prometheus server.
- `Alerting and AlertManager`: Here you can set alerting (e.g., “If CPU usage reache a threshold of 80% you want to be alert for it, send an alert maybe on cell phone, email, slack or whatever.”). Easy integration with Grafana
- `Scalability`: Prometheus is designed to scale you can add instance when the workload becomes heavy. 
- Easy integration with Grafana.


### Main components and description:

1. `Prometheus Server`: `Core component` that scrapes metrics and stores them in a time-series database. It's responsible for colleting and storing querying the metrics. It periodically check for metrics data then store it localy and it available for you to query.
2. `Exporters`: It's and agents that you install on the target system (EC2 instance) that is responsible of exposing the metrics (e.g., node_exporter for system metrics, app-specific exporters).
3. `Prometheus Alertmanager`: Alertmanager is the one that handle alerts. So you need to install this to send you notification (e.g., send email, Slack, PagerDuty)
4. `Prometheus Web UI`: When you setup a server this Prometheus UI will give you a UI, which makes it easy for you to visualize and query it. So, It's just a basic web-based interface that allow you to run those PromQL queries on the UI don't need to do that from the CLI. 
5. `Data Storage`: Prometheus have it on `Time-series database (TSDB) built-in(already set up)` where it store the collected metrics in the form of `key-value pair`. This storage is optimized for high volume so don't have to wory about latency and all those.
6. Pushgateway: Receives metrics from short-lived jobs that can’t be scraped directly.
7. Service Discovery: Automatically finds what to monitor (e.g., Kubernetes, EC2 instances).
8. Grafana: Visualization dashboard for Prometheus metrics.

#### Main differences between Prometheus vs AWS CloudWatch

|Feature |              Prometheus          |          AWS CloudWatch       |
| --     | -------------------------------- | ----------------------------- |
| Type   |Open-source monitoring & alerting toolkit |Managed monitoring service by AWS |
| Metric Storage   |Uses local Time Series Database (TSDB) |Uses AWS-managed storage (no control over internal storage) |
| Query Language   |PromQL (Prometheus Query Language) — very flexible |CloudWatch Metric Math — less powerful and flexible |
| Deployment   |You install and manage it yourself (e.g., on EC2, Kubernetes, or Docker) |Fully managed by AWS — no installation needed |
| Alerting System   |Alertmanager — powerful and customizable |CloudWatch Alarms — simpler, managed alerts |
| Cost   |Free (open-source) but you pay for infrastructure |Pay-per-use (based on metrics, logs, and API calls) |



## 🪜 3. Project Setup Steps
### Step 1 — Prometheus Server Installation. 
1. Launched 2 ubuntu server: (Prometheuse-ubuntu-server and target-host)

![Alt text](images/prometheus-ubuntu-ec2.png)