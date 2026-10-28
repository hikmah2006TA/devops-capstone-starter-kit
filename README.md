## How to Use This Scaffold

> [!IMPORTANT]
> **Starter Kit Guidance & Academic Honesty**
> 
> Because baseline starter configurations were not provided for our capstone, this repository provides clean, working architectural templates and configuration scaffolding to help you get unstuck and complete your requirements before the submission deadline.
> 
> To ensure you learn the core DevOps and SRE principles and avoid submitting identical work:
> 1. **Customize Your Infrastructure Settings:** Do not copy-paste identical resource names. Update `capstone-1-voting-app/terraform/variables.tf` to use your own AWS region, cluster name, and node group names.
> 2. **Set Your Own Container Registry:** In `capstone-1-voting-app/ci-cd/deploy.yml` and `helm/voting-app/values.yaml`, replace Docker Hub image references with your own Docker Hub username and repositories.
> 3. **Update Alerting URLs:** In `capstone-2-robot-shop/alerts/robot-shop-slo-rules.yaml`, replace `<YOUR_GITHUB_USERNAME>` with your personal GitHub handle for the runbook links.
> 4. **Execute Your Own SRE Failure Drill:** Do not copy static postmortem timelines or numbers. Trigger the fault injection drill in your own cluster, record your own start and recovery times, and compute your actual error budget consumption.

---

## Support & Appreciation ⭐

If these templates saved you time, helped you solve tricky EKS issues, or made your capstone easier to complete, please consider:

- Dropping a **Star ⭐** on this repository so other students can easily find it.
- **Forking 🍴** this repository to use and customize the templates in your own projects.
- [Following me on GitHub](https://github.com/tamecalm) for more cloud, Kubernetes, and DevOps resources.


## Capstone Validation

- Deployed the Voting App to AWS EKS using Helm.
- Verified voting and result updates.
- Tested Helm upgrade and rollback.
- Configured GitHub Actions for Trivy scanning and Docker image builds.
Good luck with your capstone!
