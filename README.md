# DevOps Capstone Projects

This repository contains two DevOps capstone projects completed using AWS, Docker, Kubernetes, CI/CD automation, monitoring, logging, and distributed tracing.

## Capstone 1: Voting Application

A containerized voting application deployed to Amazon EKS using Terraform and Helm.

**Key technologies:**
- AWS EKS and Terraform
- Docker and Docker Hub
- Kubernetes and Helm
- GitHub Actions and Trivy
- Python Flask, C#/.NET, Node.js
- Redis and PostgreSQL

**Key achievements:**
- Provisioned AWS EKS infrastructure using Terraform.
- Containerized and deployed the application.
- Configured a GitHub Actions CI/CD pipeline.
- Verified Kubernetes deployments and services.
- Tested Helm upgrades and rollback.

Documentation: [Capstone 1 – Voting Application](capstone-1-voting-app/README.md)

## Capstone 2: Robot Shop Monitoring and Observability

A microservices monitoring and observability project deployed on Amazon EKS.

**Key technologies:**
- AWS EKS and Kubernetes
- Prometheus and Grafana
- Loki and Fluent Bit
- Jaeger and OpenTelemetry
- Blackbox Exporter
- Alertmanager and Slack

**Key achievements:**
- Deployed monitoring and observability components.
- Configured metrics collection and Grafana dashboards.
- Implemented centralized logging with Loki and Fluent Bit.
- Verified distributed tracing with Jaeger.
- Configured alert notifications to Slack.
- Documented SLOs, error-budget policy, and incident postmortem.

Documentation: [Capstone 2 – Robot Shop](capstone-2-robot-shop/README.md)

## Repository Structure

```text
devops-capstone-starter-kit/
├── .github/
│   └── workflows/
├── capstone-1-voting-app/
│   └── README.md
├── capstone-2-robot-shop/
│   ├── README.md
│   └── logging/
│       └── README.md
└── README.md
```

## AWS Environment

- Region: `eu-north-1`
- EKS Cluster: `voting-app-cluster`

See each capstone's README for its architecture, configuration, deployment instructions, and verification details.
