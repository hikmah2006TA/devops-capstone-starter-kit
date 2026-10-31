# Logging and Log Aggregation

## 1. Overview

This section describes the logging and log aggregation system implemented for the Robot Shop application in the DevOps Capstone 2 project.

The logging pipeline collects container logs from Kubernetes workloads, forwards them to Loki for storage, and makes them available for searching and analysis through Grafana.

## 2. Objectives

The objectives of the logging implementation are to:

- Collect logs from application containers running in Kubernetes.
- Centralise logs in one location for easier monitoring.
- Enrich logs with Kubernetes metadata.
- Filter logs by application service and severity level.
- Support troubleshooting and incident investigation.

## 3. Tools and Technologies

| Tool | Purpose |
|---|---|
| Fluent Bit | Collects and forwards container logs. |
| Loki | Stores and indexes log labels. |
| Grafana | Provides log visualisation and querying. |
| Kubernetes | Runs the application and logging components. |

## 4. Architecture and Workflow

The logging pipeline follows this workflow:

1. Robot Shop application containers generate logs.
2. Fluent Bit runs as a Kubernetes DaemonSet and collects container logs from the nodes.
3. The Kubernetes filter enriches the logs with metadata.
4. Fluent Bit forwards the logs to Loki.
5. Grafana queries Loki and displays the collected logs.

**Loki endpoint:**

`loki.monitoring.svc.cluster.local:3100`

## 5. Fluent Bit Configuration

Fluent Bit is deployed as a DaemonSet in the `monitoring` namespace.

The configuration includes:

- Tail input plugin to read container log files.
- CRI parser to process Kubernetes container log format.
- Kubernetes filter to retrieve pod and namespace metadata.
- Loki output plugin to forward logs to Loki.
- Automatic Kubernetes labels to make service-based filtering possible.

The input tag is configured as:

`kube.*`

This allows the Kubernetes filter to match the collected container logs correctly.

## 6. Loki Configuration

Loki is deployed in the `monitoring` namespace and receives logs from Fluent Bit.

The service is accessible internally through:

`loki.monitoring.svc.cluster.local:3100`

Loki stores the incoming logs and makes them available for querying through Grafana.

## 7. Grafana Log Queries

The following LogQL queries were used in Grafana Explore.

### View Cart service logs

```logql
{service="cart"}
```

### View Web service logs

```logql
{service="web"}
```

### View informational Cart logs

```logql
{service="cart", level="info"}
```

### View debug Cart logs

```logql
{service="cart", level="debug"}
```

### Search for error-level logs

```logql
{service=~".+", level="error"}
```

## 8. Verification and Results

The logging pipeline was verified using Grafana Explore.

| Verification | Result |
|---|---|
| Fluent Bit log collection | Successful |
| Logs forwarded to Loki | Successful |
| Kubernetes metadata labels | Available |
| Cart service log filtering | Successful |
| Web service log filtering | Successful |
| Severity labels | `info` and `debug` observed |
| Error-level logs | No matching entries observed in the selected time range |

The Web service query returned **46 log lines**, with approximately **36.0 kB** of data processed.

The Cart service query also returned application logs, confirming that logs from multiple Robot Shop services can be accessed.

No error-level entries were found during the selected observation period. This does not necessarily indicate a logging failure; it means no matching error-level entries were available in that time range.

## 9. Conclusion

The logging and log aggregation pipeline was successfully implemented and verified.

Fluent Bit collects container logs from Kubernetes workloads and forwards them to Loki. Grafana provides access to the logs and supports filtering by service and severity level.

This setup provides centralised application logging and supports troubleshooting and incident investigation for the Robot Shop application.

