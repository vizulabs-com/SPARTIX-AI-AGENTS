# Skill: Performance Profiling

## Name
performance-profiling

## Version
1.0.0

## Description
Profile and analyze performance characteristics of applications, services, databases, and infrastructure. Identifies bottlenecks, memory leaks, slow queries, rendering issues, and resource inefficiencies with optimization recommendations.

## Parameters
- **target**: What to profile (frontend app, backend service, database queries, API endpoints, infrastructure)
- **metrics**: Performance metrics to measure (response time, throughput, CPU, memory, I/O, render time)
- **baseline**: Performance baseline or SLA targets to compare against
- **tool**: Profiling tool to use (Chrome DevTools, flame graphs, query analyzers, APM tools)

## Outputs
- Performance profiling report with metrics, bottleneck identification, and evidence
- Flame graphs, waterfall charts, or query execution plans as applicable
- Optimization recommendations with expected impact estimates
- Before/after comparison if optimizations were applied

## Prerequisites
- Application or service must be accessible for profiling
- Performance baselines or SLA targets must be defined in the task packet
- Profiling scope must be specified (specific endpoints, pages, queries, or system-wide)

## Approved Categories
- 04_FRONTEND_WEB_SPECIALISTS
- 05_BACKEND_AND_API_SPECIALISTS
- 06_DATABASE_AND_DATA_FOUNDATION
- 12_DEVOPS_INFRASTRUCTURE_AND_CLOUD

## Usage Rules
- Profiling must be conducted under realistic load conditions — not just idle state
- All bottlenecks must be ranked by impact and effort to fix
- Recommendations must include specific implementation guidance, not just general advice
