# Robot Shop Alert Runbook

## Status

The alert rules in `alerts/robot-shop-slo-rules.yaml` are proposed configuration. They have not been deployed because the Prometheus Operator `PrometheusRule` CRD is not installed in the current cluster.

## 1. RobotShopPaymentAvailabilitySLOBreached

**Severity:** Critical

**Meaning:** The payment service may be unready or unavailable.

**Investigation:**
1. Check payment pod status: `kubectl get pods -n robot-shop -l name=payment`
2. Inspect pod events and restarts: `kubectl describe pods -n robot-shop`
3. Review payment logs: `kubectl logs -n robot-shop deployment/payment --tail=100`

**Response:** Investigate failing readiness probes, application errors, resource constraints, and dependencies before restarting or changing workloads.

## 2. RobotShopWebAvailabilitySLOBreached

**Severity:** Critical

**Meaning:** The web frontend may be unready or unavailable.

**Investigation:**
1. Check Robot Shop pods: `kubectl get pods -n robot-shop`
2. Check services: `kubectl get services -n robot-shop`
3. Inspect web pod events and logs: `kubectl logs -n robot-shop deployment/web --tail=100`

**Response:** Check pod readiness, service endpoints, ingress or load balancer connectivity, and recent deployment changes.

## 3. RobotShopHighCrashLoopRate

**Severity:** Warning

**Meaning:** A pod may be restarting repeatedly.

**Investigation:**
1. Check pod status: `kubectl get pods -n robot-shop`
2. Inspect the affected pod: `kubectl describe pod -n robot-shop POD_NAME`
3. Review current or previous container logs as appropriate: `kubectl logs -n robot-shop POD_NAME --all-containers=true --tail=100`

**Response:** Identify the cause from events and logs. Check configuration, dependencies, probes, and resource limits before making changes.

## Important Notes

- These procedures are investigation guidance, not proof that the alerts are active.
- Validate the alert expressions and deploy them only after a compatible alert-rule mechanism is available.
- Confirm actual deployment names and selectors before running workload-specific commands.
- Avoid deleting or restarting production resources without understanding the impact.
