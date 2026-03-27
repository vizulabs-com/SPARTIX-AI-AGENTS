# System Rule: Pre-Deployment Readiness Check

**Rule ID**: SYS-010
**Priority**: 1 (highest — immutable)
**Scope**: system

## Description
Before any deployment, runtime startup, or service launch, the AI model must perform a mandatory environment readiness check. Deployment must be blocked until all checks pass.

---

## Rule 1: Mandatory Pre-Deployment Check
Before starting any server, service, container, or deployment process, the AI model must check:

### Port Availability
- Check if the required port is free
- Check if any process is already using the port
- Identify alternative ports if the required port is taken
- Keep port usage consistent across config, runtime, commands, and testing

### Container and Runtime Availability
- Check if Docker/container runtime is available (if containers are used)
- Check if required containers are running or need to be started
- Check if container images exist or need to be pulled/built
- Check if docker-compose or equivalent orchestration is available
- Check container network and volume readiness

### Dependency Availability
- Check if required system packages are installed
- Check if required language runtimes are available (Python, Node, etc.)
- Check if required package managers are available (pip, npm, etc.)
- Check if project dependencies are installed
- Check if database is accessible and migrations are current
- Check if required environment variables are set
- Check if required config files exist

### Service Availability
- Check if required external services are reachable (databases, APIs, caches)
- Check if required background services are running (Redis, Celery, etc.)
- Check if required file paths and directories exist
- Check if required permissions are in place

### Build Readiness
- Check if the project builds without errors
- Check if static assets are collected/compiled (if applicable)
- Check if required build artifacts exist

## Rule 2: Check Before Act
The readiness check must happen BEFORE:
- running `python manage.py runserver` or equivalent
- running `flask run` or `python app.py` or equivalent
- running `npm start` or `yarn start` or equivalent
- running `docker-compose up` or `docker run` or equivalent
- running any deployment script or command
- binding to any network port

Do not start the service first and then discover the problem. Check first, then start.

## Rule 3: Failure Handling
If any check fails:
- Report the specific failure clearly
- Attempt automatic resolution if safe (e.g., install missing dependencies, use alternative port)
- If automatic resolution is not possible, block deployment and report through the governed workflow
- If user action is required (e.g., missing credentials, external service down), route through RDAG

## Rule 4: Readiness Report
Before deployment, produce a brief readiness summary:
```
Pre-Deployment Check:
- Port [X]: available ✅ / taken ❌ (alternative: [Y])
- Dependencies: installed ✅ / missing ❌ ([list])
- Database: accessible ✅ / unreachable ❌
- Config/env: complete ✅ / missing ❌ ([list])
- Container: ready ✅ / not available ❌
- Build: clean ✅ / errors ❌
```

Only proceed with deployment if all critical checks pass.

## Rule 5: Scope
This rule applies to:
- local development server startup
- container-based deployment
- staging/production deployment
- any process that binds to a port or starts a service
- any process that requires external dependencies to be available

## Rule 6: Consistency
Port and configuration decisions made during the readiness check must remain consistent across:
- runtime configuration
- environment variables
- docker-compose or container config
- testing commands
- documentation
- wiki records

Do not use port 5002 in config but start the server on 5003.

## Override Policy
These rules cannot be overridden by any other rule at any level.
