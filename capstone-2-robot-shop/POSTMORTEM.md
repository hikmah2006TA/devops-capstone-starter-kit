# Robot Shop Incident Postmortem

> **Status:** Incident simulation completed — timeline partially documented

## 1. Incident Summary

- **Incident time and timezone:** Slack firing notification at 7:14 AM and resolved notification at 7:19 AM WAT (UTC+1)
- **Duration:** Actual outage duration not yet confirmed; Slack notification interval was 5 minutes.
- **Affected service:** Robot Shop web service
- **Severity:** Controlled test — not a production incident
- **Incident lead:** DevOps trainee

## 2. Impact

The Robot Shop web service was intentionally made unavailable during a controlled incident drill.

The web deployment was scaled from one replica to zero replicas. During the simulation, the website was unavailable. Other Robot Shop application services remained running.

The exercise was designed to verify monitoring, alert delivery, and recovery procedures.

**Evidence:**
- Kubernetes pod listing showing no web pod during the simulation.
- Slack firing notification in `#robot-shop-alerts`.
- Kubernetes pod listing showing the restored web pod.

## 3. Detection

- **How was the incident detected?** Prometheus detected that the Robot Shop web endpoint was unavailable using the `RobotShopWebEndpointDown` alert rule.
- **Was the alert timely and actionable?** The alert was received in Slack through Alertmanager after the configured detection period.
- **Detection gaps:** Exact detection latency should be measured using the alert and Slack timestamps. The exercise also confirmed that recovery notifications may be delayed by Alertmanager's notification grouping interval.

## 4. Timeline

| Event | Time |
|---|---|
| Baseline checked; web deployment had one available replica | Record time |
| Web deployment scaled to zero replicas | Record time |
| Prometheus detected the unavailable web endpoint | Record time |
| Slack firing notification received | 7:14 AM WAT |
| Web deployment restored to one replica | Record time |
| Web pod returned to Running and Ready | Record time |
| Slack resolved notification received | 7:19 AM WAT |
*All times should be completed using the Slack notification timestamps and terminal history.*

## 5. Mitigation and Recovery

The web deployment was restored by scaling it back to one replica.

Command used to simulate the outage:

`kubectl scale deployment web -n robot-shop --replicas=0`

Command used to restore service:

`kubectl scale deployment web -n robot-shop --replicas=1`

Recovery was verified using:

`kubectl get pods -n robot-shop`

The web pod returned with status `Running` and readiness `1/1`. All 12 Robot Shop application pods were subsequently confirmed running.

## 6. Root Cause and Contributing Factors

- **Root cause:** The web deployment was intentionally scaled to zero replicas as part of the incident simulation.
- **Contributing factors:** The absence of web replicas caused the web endpoint to become unavailable.
- **Evidence:** Kubernetes deployment and pod outputs, Prometheus alert, and Slack notifications.

This was an intentional test action, not an unexpected application failure.

## 7. What Went Well

- Prometheus successfully detected the web endpoint outage.
- Alertmanager successfully delivered the firing notification to Slack.
- The web deployment was restored to its original replica count.
- Kubernetes confirmed that the web pod returned to a healthy state.
- Slack successfully delivered the resolved notification.

## 8. What Could Be Improved

- Record exact incident and recovery timestamps automatically.
- Improve incident timeline documentation.
- Review alert notification delays and grouping settings.
- Consider automating recovery verification.
- Continue testing monitoring alerts and recovery procedures.

## 9. Corrective Actions

| Action | Priority | Owner or role | Status |
|---|---|---|---|
| Document the incident simulation and evidence | High | DevOps trainee | Completed |
| Verify Slack firing and resolved notifications | High | DevOps trainee | Completed |
| Review alert timing and notification grouping | Medium | DevOps trainee | Pending |
| Improve incident response documentation | Medium | DevOps trainee | Pending |

## 10. Follow-up

- Review the `RobotShopWebEndpointDown` alert rule.
- Keep the Slack notification integration enabled.
- Review the Robot Shop runbook and SLO documentation.
- Perform additional controlled monitoring tests.
- Verify corrective actions and retain screenshots as capstone evidence.

**Final outcome:** The incident simulation successfully demonstrated outage detection, Slack notification delivery, service restoration, and recovery notification delivery.
