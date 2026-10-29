# Robot Shop SLO and Error Budget Policy

## 1. Purpose

This document defines a proposed availability Service Level Objective (SLO) for Robot Shop and explains how its error budget will guide reliability decisions.

## 2. Service Level Objective

- **Service:** Robot Shop
- **Objective:** 99% availability
- **Measurement window:** Rolling 30 days
- **Availability indicator:** Successful eligible user requests divided by all eligible user requests.
- **Status:** Proposed. Application-level request and error metrics must be validated before compliance can be measured reliably.

## 3. Error Budget

The error budget is the portion of the measurement window during which the service may be unavailable while still meeting the SLO.

At 99% availability over 30 days:

- Total time: 720 hours
- Allowed unavailability: 1% of 720 hours
- Error budget: 7.2 hours, or 7 hours and 12 minutes

This time-based calculation is illustrative. The actual request-based error budget must be calculated from eligible request counts once suitable application metrics are available.

## 4. Error Budget Policy

1. Monitor availability and error-budget consumption when reliable metrics are available.
2. Investigate incidents that cause failed requests or reduce availability.
3. When the error budget is nearly exhausted, prioritise reliability fixes and review the risk of non-essential changes.
4. When the error budget is exhausted, pause high-risk releases until the service has improved, except for urgent security or reliability fixes.
5. Review incidents without blame and record corrective actions.
6. Reassess the SLO periodically using service behaviour and user needs.

## 5. Monitoring and Validation

The current monitoring setup includes Prometheus, Grafana, Loki, Fluent Bit, Jaeger, and an OpenTelemetry Collector.

The existing dashboard primarily displays resource metrics. Reliable application-level request rate, error rate, and latency metrics still need to be established. The proposed SLO must not be reported as achieved until its measurement method is implemented and validated.

## 6. Review

Review this policy after the application metrics and alerting rules have been validated. Update the target and error-budget policy if operational evidence supports a change.
