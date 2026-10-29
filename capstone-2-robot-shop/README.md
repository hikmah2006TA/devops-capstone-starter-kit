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

- `alerts/` — Proposed Robot Shop alerting rules.
- `dashboards/` — Grafana dashboard configuration and metrics dashboard JSON.
- `helm/` — Robot Shop deployment values and supporting configuration.
- `logging/` — Loki and Fluent Bit configuration files.
- `tracing/` — Jaeger, OpenTelemetry Collector, and synthetic trace test files.

## 4. Metrics and Dashboards

Prometheus and Grafana were configured to monitor selected Robot Shop services. The dashboard includes panels for:

- CPU usage
- Memory usage
- Network receive throughput
- Network transmit throughput
- Cart activity
- Payment activity

Cart and payment application metrics were available for scraping. The dashboard covers selected infrastructure and application metrics; it does not represent complete HTTP request-rate, error-rate, and latency monitoring for every service.

## 5. Logging

Loki was deployed as the log backend, and Fluent Bit was configured to collect container logs and forward them to Loki.

Fluent Bit's metrics showed that records were read, filtered, and processed, with zero reported output errors during the check. However, Robot Shop-specific logs were not successfully verified as queryable in Loki during testing.

Therefore, the logging pipeline requires further end-to-end verification before it can be considered fully validated. Loki uses ephemeral storage in this setup, so stored logs may not survive pod replacement.

## 6. Distributed Tracing

Jaeger and the OpenTelemetry Collector were deployed and tested using a synthetic trace representing a workflow across the web, catalogue, cart, and payment components.

The test trace was accepted by the collector and found in Jaeger with four spans. This verifies the synthetic trace path, but does not prove that the Robot Shop application itself is instrumented to send live traces.

## 
## 7. Verification Summary

| Component | Verification result |
|---|---|
| Prometheus | Deployed; selected targets were up |
| Grafana | Dashboard created and metrics displayed |
| Loki | Deployed; datasource configured |
| Fluent Bit | Records processed with no reported output errors during the check |
| Robot Shop logs in Loki | Not yet verified end to end |
| Jaeger | Synthetic four-span trace found |
| Live application tracing | Not verified |

## 8. Limitations and Future Improvements

- Verify that Robot Shop container logs can be queried in Loki.
- Configure persistent storage where required.
- Add instrumentation for live distributed tracing.
- Validate alerting rules with a compatible Prometheus Operator setup.
- Add application HTTP request, error, and latency metrics where supported.
- Document a controlled failure-and-recovery exercise if required by the capstone rubric.

## 9. Conclusion

The project establishes a monitoring and observability foundation for Robot Shop on Amazon EKS. Metrics dashboards and synthetic distributed tracing were verified. Logging and live application tracing still require additional validation before the observability implementation can be considered fully complete.
