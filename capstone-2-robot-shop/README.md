# Capstone 2: Robot Shop Observability

## 1. Project Overview

This project implements an observability stack for the Robot Shop application running on Amazon EKS. It uses metrics, logs, and distributed tracing to help monitor application behaviour and investigate issues.

## 2. Tools Used

- **Amazon EKS:** Kubernetes cluster for running the application.
- **Prometheus:** Collects metrics from Kubernetes and selected Robot Shop services.
- **Grafana:** Visualizes metrics through dashboards.
- **Loki:** Stores and queries application logs.
- **Fluent Bit:** Collects container logs and forwards them to Loki.
- **Jaeger:** Provides distributed trace visualization.
- **OpenTelemetry Collector:** Receives and forwards telemetry data.

## 3. Project Structure

- `alerts/` — Robot Shop alerting rules and supporting configuration.
- `dashboards/` — Grafana dashboard configuration and exported dashboard JSON files.
- `helm/` — Robot Shop deployment values and supporting configuration.
- `logging/` — Loki and Fluent Bit configuration files.
- `tracing/` — Jaeger, OpenTelemetry Collector, and synthetic trace test files.

## 4. Metrics and Dashboards

Prometheus and Grafana were configured to monitor selected Robot Shop services. The metrics dashboard includes panels for:

- CPU usage
- Memory usage
- Network receive throughput
- Network transmit throughput
- Cart activity
- Payment activity

Cart and payment application metrics were available for scraping. The dashboard covers selected infrastructure and application metrics; it does not represent complete HTTP request-rate, error-rate, and latency monitoring for every service.

### HTTP Logging Dashboards

Four Grafana dashboards were created using Loki queries against web-service logs:

| Dashboard file | Purpose |
|---|---|
| `http-requests.json` | Displays HTTP request counts over a five-minute window. |
| `http-4xx-errors.json` | Displays HTTP 4xx client-error counts over a five-minute window. |
| `http-5xx-errors.json` | Displays HTTP 5xx server-error counts over a one-hour window. |
| `http-5xx-error-rate.json` | Displays the percentage of HTTP 5xx errors among HTTP requests over a one-hour window. |

These dashboards focus on the Robot Shop web service and do not establish complete HTTP monitoring for every application service.

## 5. Logging

Loki was deployed as the log backend, and Fluent Bit was configured to collect container logs and forward them to Loki.

Fluent Bit's metrics showed that records were read, filtered, and processed, with zero reported output errors during the check. Loki queries were also used to create and verify four HTTP dashboards based on web-service logs.

This verifies the use of web-service logs for the HTTP dashboards; it does not establish that logs from every Robot Shop service have been fully validated. Loki uses ephemeral storage in this setup, so stored logs may not survive pod replacement.

## 6. Distributed Tracing

Jaeger and the OpenTelemetry Collector were deployed and tested using a synthetic trace representing a workflow across the web, catalogue, cart, and payment components.

The test trace was accepted by the collector and found in Jaeger with four spans. This verifies the synthetic trace path, but does not prove that the Robot Shop application itself is instrumented to send live traces.

## 7. Verification Summary

| Component | Verification result |
|---|---|
| Prometheus | Deployed; selected targets were up |
| Grafana | Metrics dashboards and four HTTP logging dashboards created |
| Loki | Deployed; datasource configured and web-service log queries used |
| Fluent Bit | Records processed with no reported output errors during the check |
| HTTP logging dashboards | Four dashboards created from web-service log queries |
| Robot Shop logs across all services | Not fully verified end to end |
| Jaeger | Synthetic four-span trace found |
| Live application tracing | Not verified |
| Incident simulation | Verified; Prometheus alert and Slack firing/resolved notifications received |

## 8. Limitations and Future Improvements

- Verify log collection and querying for all Robot Shop services.
- Configure persistent storage where required.
- Add instrumentation for live distributed tracing.
- Validate alerting rules with a compatible Prometheus Operator setup.
- Add application HTTP request, error, and latency metrics for services where supported.
- Retain screenshots and complete the incident timeline for the controlled failure-and-recovery exercise.

## 9. Conclusion

The project establishes a monitoring and observability foundation for Robot Shop on Amazon EKS. Selected infrastructure and application metrics, four HTTP logging dashboards based on web-service logs, and synthetic distributed tracing were verified. Full log validation across all services and live application tracing still require additional work.
