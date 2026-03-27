# Skill: Security Scanning

## Name
security-scanning

## Version
1.0.0

## Description
Scan code, configurations, dependencies, and infrastructure for security vulnerabilities. Covers SAST, DAST, dependency auditing, secret detection, and configuration security assessment with CVE mapping and remediation guidance.

## Parameters
- **scan_type**: Type of scan (SAST, DAST, dependency audit, secret detection, config audit)
- **target**: What to scan (source code, dependencies, Docker images, IaC templates, API endpoints)
- **severity_threshold**: Minimum severity to report (critical, high, medium, low)
- **compliance_framework**: Compliance framework to validate against (OWASP, CIS, PCI-DSS, SOC2)

## Outputs
- Security scan report with vulnerability findings and CVE references
- Severity-rated vulnerability list with affected components
- Remediation guidance for each finding with priority ordering
- Compliance status against the specified framework

## Prerequisites
- Scan targets must be accessible and specified in the task packet
- Severity threshold must be defined in the acceptance criteria
- Compliance framework must be specified if compliance validation is required

## Approved Categories
- 11_SECURITY_PRIVACY_AND_COMPLIANCE
- 23_ADVANCED_SECURITY_SPECIALISTS

## Usage Rules
- All critical and high severity findings must be reported regardless of threshold settings
- Scan results must include evidence (file, line, CVE ID) for each finding
- False positives must be documented with justification for exclusion
