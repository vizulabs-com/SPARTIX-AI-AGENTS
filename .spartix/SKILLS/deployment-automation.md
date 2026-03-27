# Skill: Deployment Automation

## Name
deployment-automation

## Version
1.0.0

## Description
Automate deployment processes including CI/CD pipeline configuration, infrastructure provisioning, container orchestration, rollback procedures, and environment promotion workflows with safety gates and validation checks.

## Parameters
- **pipeline_type**: Type of pipeline (CI, CD, CI/CD combined, infrastructure, container)
- **target_environment**: Deployment target (development, staging, production, preview)
- **strategy**: Deployment strategy (blue-green, canary, rolling, recreate, feature-flag)
- **platform**: Target platform (AWS, GCP, Azure, Kubernetes, Docker Compose)

## Outputs
- Pipeline configuration files (GitHub Actions, GitLab CI, Jenkins, etc.)
- Infrastructure as Code templates (Terraform, CloudFormation, Pulumi)
- Deployment scripts with rollback procedures
- Environment promotion workflow documentation

## Prerequisites
- Target platform and environment must be specified in the task packet
- Deployment strategy must be approved by CO before implementation
- Infrastructure access credentials must be available (via secrets management)

## Approved Categories
- 12_DEVOPS_INFRASTRUCTURE_AND_CLOUD
- 27_DOCKER_CONTAINERS_AND_DEPLOYMENT

## Usage Rules
- All deployment pipelines must include automated testing gates before production promotion
- Rollback procedures must be tested and documented for every deployment pipeline
- Secrets must never be hardcoded — always use secrets management integration
