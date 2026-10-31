# Robot Shop SLO and Error Budget Policy

## 1. Purpose

This document defines the availability Service Level Objective (SLO) for Robot Shop and explains how its error budget will guide reliability decisions and incident response.

## 2. Service Level Objective

- **Service:** Robot Shop
- **Availability target:** 99%
- **Measurement window:** Rolling 30 days
- **Service Level Indicator (SLI):** Successful eligible requests divided by total eligible requests.
- **Status:** Proposed; full compliance measurement is pending validated application-level request metrics.

## 3. Availability Monitoring

Robot Shop availability is monitored using Prometheus and Blackbox Exporter.

The current black-box monitoring checks:

- **Web endpoint:** `http://web.robot-shop.svc.cluster.local:8080/`
- **Payment metrics endpoint:** `http://payment.robot-shop.svc.cluster.local:8080/metrics`

Both endpoints currently return successful HTTP 200 responses.

Prometheus collects probe results every 30 seconds. Endpoint-down alerts are configured to trigger after 2 minutes of continuous probe failure.

**Measurement limitation:** The payment metrics endpoint check confirms that the endpoint is reachable; it does not confirm successful payment transactions. Application-level request, error and latency metrics are still required for a complete user-request-based SLI.

Prometheus currently has 6 hours of data retention. Therefore, a rolling 30-day availability measurement is not yet available.

## 4. Error Budget

The error budget represents the allowable unavailability within the SLO measurement window.

For a 99% availability target over 30 days:

- Total measurement period: 720 hours
- Allowed unavailability: 1%
- Error budget: 7.2 hours (7 hours and 12 minutes)

This is an illustrative time-based calculation. Actual request-based error-budget consumption must be calculated when suitable application metrics are available.

## 5. Error Budget Policy

1. Monitor availability and error-budget consumption using reliable metrics.
2. Investigate incidents that cause endpoint failures or unsuccessful user requests.
3. When the error budget is nearly exhausted, prioritise reliability improvements.
4. When the error budget is exhausted, pause high-risk releases except urgent security and reliability fixes.
5. Record incidents, root causes, mitigation steps and corrective actions.
6. Review the SLO periodically based on application performance and user needs.

## 6. Alerting Strategy

Prometheus currently has three alert rules:

- `RobotShopHighCPUUsage` – detects sustained high CPU usage.
- `RobotShopWebEndpointDown` – detects web endpoint probe failures.
- `RobotShopPaymentMetricsEndpointDown` – detects payment metrics endpoint probe failures.

The two endpoint alerts trigger after 2 minutes of continuous failure.

The alerts are evaluated by Prometheus. Slack notification delivery is not yet configured because Alertmanager is currently disabled.

## 7. Monitoring Tools

The monitoring architecture uses:

- **Prometheus:** Metrics collection and alert evaluation.
- **Grafana:** Monitoring dashboards and visualisation.
- **Blackbox Exporter:** HTTP endpoint availability checks.
- **Fluent Bit:** Container log collection.
- **Loki:** Centralised log storage.
- **OpenTelemetry Collector:** Telemetry collection and forwarding.
- **Jaeger:** Distributed trace visualisation.

## 8. Review and Improvement

The SLO policy will be reviewed after:

1. Application-level request, error and latency metrics are validated.
2. A suitable method for retaining 30 days of monitoring data is established.
3. Slack alert notifications are configured and tested.
4. An incident simulation is completed and documented.

The 99% availability target remains proposed until the measurement system can reliably calculate actual service availability.# Robot Shop SLO and Error Budget Policy

## 1. Purpose

This document defines the availability Service Level Objective (SLO) for Robot Shop and explains how its error budget will guide reliability decisions and incident response.

## 2. Service Level Objective

- **Service:** Robot Shop
- **Availability target:** 99%
- **Measurement window:** Rolling 30 days
- **Service Level Indicator (SLI):** Successful eligible requests divided by total eligible requests.
- **Status:** Proposed; full compliance measurement is pending validated application-level request metrics.

## 3. Availability Monitoring

Robot Shop availability is monitored using Prometheus and Blackbox Exporter.

The current black-box monitoring checks:

- **Web endpoint:** `http://web.robot-shop.svc.cluster.local:8080/`
- **Payment metrics endpoint:** `http://payment.robot-shop.svc.cluster.local:8080/metrics`

Both endpoints currently return successful HTTP 200 responses.

Prometheus collects probe results every 30 seconds. Endpoint-down alerts are configured to trigger after 2 minutes of continuous probe failure.

**Measurement limitation:** The payment metrics endpoint check confirms that the endpoint is reachable; it does not confirm successful payment transactions. Application-level request, error and latency metrics are still required for a complete user-request-based SLI.

Prometheus currently has 6 hours of data retention. Therefore, a rolling 30-day availability measurement is not yet available.

## 4. Error Budget

The error budget represents the allowable unavailability within the SLO measurement window.

For a 99% availability target over 30 days:

- Total measurement period: 720 hours
- Allowed unavailability: 1%
- Error budget: 7.2 hours (7 hours and 12 minutes)

This is an illustrative time-based calculation. Actual request-based error-budget consumption must be calculated when suitable application metrics are available.

## 5. Error Budget Policy

1. Monitor availability and error-budget consumption using reliable metrics.
2. Investigate incidents that cause endpoint failures or unsuccessful user requests.
3. When the error budget is nearly exhausted, prioritise reliability improvements.
4. When the error budget is exhausted, pause high-risk releases except urgent security and reliability fixes.
5. Record incidents, root causes, mitigation steps and corrective actions.
6. Review the SLO periodically based on application performance and user needs.

## 6. Alerting Strategy

Prometheus currently has three alert rules:

- `RobotShopHighCPUUsage` – detects sustained high CPU usage.
- `RobotShopWebEndpointDown` – detects web endpoint probe failures.
- `RobotShopPaymentMetricsEndpointDown` – detects payment metrics endpoint probe failures.

The two endpoint alerts trigger after 2 minutes of continuous failure.

The alerts are evaluated by Prometheus. Slack notification delivery is not yet configured because Alertmanager is currently disabled.

## 7. Monitoring Tools

The monitoring architecture uses:

- **Prometheus:** Metrics collection and alert evaluation.
- **Grafana:** Monitoring dashboards and visualisation.
- **Blackbox Exporter:** HTTP endpoint availability checks.
- **Fluent Bit:** Container log collection.
- **Loki:** Centralised log storage.
- **OpenTelemetry Collector:** Telemetry collection and forwarding.
- **Jaeger:** Distributed trace visualisation.

## 8. Review and Improvement

The SLO policy will be reviewed after:

1. Application-level request, error and latency metrics are validated.
2. A suitable method for retaining 30 days of monitoring data is established.
3. Slack alert notifications are configured and tested.
4. An incident simulation is completed and documented.

The 99% availability target remains proposed until the measurement system can reliably calculate actual service availability.
