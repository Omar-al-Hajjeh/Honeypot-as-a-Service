# Project Scope

## In scope for the initial platform

- User authentication and basic workspace access control
- Creating and managing supported honeypot deployments
- Deployment lifecycle and health visibility
- Central collection and review of honeypot interaction events
- Basic event filtering and export
- Audit records for security-relevant actions
- Operational and security documentation

## Out of scope for the initial platform

- Production incident response or automated blocking of external systems
- Offensive security actions, exploitation, or credential use against third parties
- Arbitrary execution of user-provided code in the platform control plane
- A guarantee that honeypot observations identify a real-world person or organization
- Advanced analytics, machine learning attribution, or threat-intelligence enrichment
- Specific cloud-provider support or a fixed list of honeypot engines until selected

## Constraints and dependencies

- The platform must be deployed on infrastructure the operator is authorized to use.
- The deployment design must isolate decoys and limit egress before any public exposure.
- Supported honeypot types depend on the chosen runtime and integration interfaces.
- Data handling, retention, and user access must follow applicable organizational and legal requirements.

## Open decisions

- Initial honeypot engines and deployment targets
- Single-tenant versus multi-tenant deployment model
- Identity provider and account lifecycle
- Event schema, storage technology, and retention defaults
- Notification channels and export formats
- Availability, performance, and recovery targets

## Release boundary

The first release should deliver a secure, documented end-to-end flow for configuring a supported honeypot, observing its status, and reviewing associated events. Additional integrations and analytics can follow after this core flow is validated.
