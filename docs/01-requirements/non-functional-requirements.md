# Non-Functional Requirements

These are initial quality goals. Numeric service targets and retention periods must be agreed before production deployment.

## Security and isolation

- **NFR-01:** Honeypot workloads shall be isolated from platform control services and customer production systems.
- **NFR-02:** Network access from honeypot workloads shall follow an explicit allowlist and least-privilege policy.
- **NFR-03:** Secrets shall not be stored in source code or exposed in logs, event views, or error messages.
- **NFR-04:** The platform shall protect data in transit and apply access controls to stored data.
- **NFR-05:** Administrative and security-relevant actions shall be auditable.
- **NFR-06:** The platform shall provide safe defaults and validate user-supplied configuration.

## Reliability and recovery

- **NFR-07:** The platform shall report service and deployment failures clearly and preserve diagnostic context for authorized operators.
- **NFR-08:** Event ingestion shall handle transient failures without silently losing acknowledged data.
- **NFR-09:** Backup, restoration, and recovery procedures shall be documented before production use.

## Performance and scale

- **NFR-10:** The event interface shall support pagination and filtering so large event collections remain usable.
- **NFR-11:** Capacity limits for users, deployments, event rates, and storage shall be configurable or documented.
- **NFR-12:** Performance targets shall be measured under representative load before release.

## Privacy and data management

- **NFR-13:** Event data collection and retention shall be documented and configurable where practical.
- **NFR-14:** The platform shall provide a controlled process for deleting deployments and their associated data.
- **NFR-15:** The system shall avoid collecting unnecessary personal data and restrict access to sensitive telemetry.

## Usability and maintainability

- **NFR-16:** The user interface shall communicate deployment status, validation failures, and destructive actions clearly.
- **NFR-17:** APIs and configuration formats shall be documented and versioned.
- **NFR-18:** Services shall emit structured logs and health information suitable for operational monitoring.
- **NFR-19:** The codebase shall support repeatable development and deployment through documented setup instructions.
- **NFR-20:** The interface shall support keyboard navigation and readable contrast for core workflows.
