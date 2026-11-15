# Functional Requirements

Functional requirements define the services the platform provides and how users interact with them. Each requirement has a unique ID, priority, and observable acceptance check so it can be verified during implementation and testing.

## Supported MVP Honeypot Types

- **SSH Honeypot:** Simulates an SSH service to collect and monitor connection attempts and suspicious authentication activity.
- **HTTP/HTTPS Honeypot:** Simulates web services to collect and monitor suspicious HTTP requests and web interaction patterns.

**Priority:** Critical requirements protect tenant boundaries or core data correctness. High requirements are required for the MVP. Medium requirements are planned for the MVP where indicated below; otherwise they may follow the core workflow.

## 1.1 User and Authentication Management

| ID | Requirement | Priority | Acceptance check |
| --- | --- | --- | --- |
| FR-001 | Users can register an account. | High | Submit valid registration details; the system creates one account and confirms success. Invalid or duplicate details are rejected with a useful error. |
| FR-002 | Users can log in and log out. | High | Valid credentials establish an authenticated session; invalid credentials do not. Logging out invalidates the session and protected requests are denied afterward. |
| FR-003 | Users can reset their passwords. | Medium | Request a reset for a registered account; the system issues a time-limited reset flow. A valid reset changes the password; an expired or reused reset token is rejected. |
| FR-004 | The system supports role-based access control. | High | For each protected operation, verify that an allowed role succeeds and a role without permission is denied. |
| FR-005 | Users can update their profile information. | Medium | An authenticated user updates permitted profile fields; the new values are returned on the next profile read, while unauthorized fields remain unchanged. |

## 1.2 Organization Management

| ID | Requirement | Priority | Acceptance check |
| --- | --- | --- | --- |
| FR-006 | Users can create an organization. | High | Submit a valid organization name; the system creates the organization and assigns its creator the initial administrator role. |
| FR-007 | Organization administrators can invite members. | High | An administrator invites a valid email address; the system creates a pending invitation associated with that organization. A non-administrator cannot invite. |
| FR-008 | Administrators can assign roles to members. | High | An administrator changes a member's role; subsequent authorization checks reflect the new role. Unauthorized users cannot change roles. |
| FR-009 | Organizations can manage their members. | High | An authorized administrator can list, update access for, and remove members; removed members can no longer access that organization's protected data. |
| FR-010 | Each organization has isolated data. | Critical | Create two organizations with separate users, honeypots, events, and alerts; requests scoped to either organization never return or modify the other's records. |

## 1.3 Honeypot Management

| ID | Requirement | Priority | Acceptance check |
| --- | --- | --- | --- |
| FR-011 | Users can create an SSH honeypot. | High | An organization administrator submits a name and valid SSH honeypot configuration. The system validates it, records a deployment request, and returns a honeypot record with lifecycle status. On provisioning success, status becomes `RUNNING`; on failure, the error is recorded and reported. |
| FR-012 | Users can create an HTTP/HTTPS honeypot. | High | An organization administrator submits a name and valid HTTP/HTTPS honeypot configuration. The system validates it, records a deployment request, and returns a honeypot record with lifecycle status. On provisioning success, status becomes `RUNNING`; on failure, the error is recorded and reported. |
| FR-013 | Users can configure honeypot settings. | High | An authorized user submits supported settings; valid values are persisted and reflected in the configuration view. Invalid or disallowed values are rejected without changing the saved configuration. |
| FR-014 | Users can view deployed honeypots. | High | An authorized organization member receives a list of that organization's honeypots and their types; honeypots belonging to another organization are absent. |
| FR-015 | Users can start and stop honeypots. | High | An authorized user requests start or stop; the system records the requested lifecycle transition and eventually reports the resulting state or a recorded failure. Unauthorized requests are denied. |
| FR-016 | Users can view honeypot deployment status. | High | The honeypot details view returns the current lifecycle state and last status update for the selected deployment. |
| FR-017 | Users can delete honeypots. | Medium | An authorized user confirms deletion; the system removes the deployment and marks its lifecycle record as deleted. Unauthorized deletion is denied and the action is audited. |

## 1.4 Infrastructure Management

| ID | Requirement | Priority | Acceptance check |
| --- | --- | --- | --- |
| FR-018 | The platform provisions honeypot infrastructure. | High | A valid deployment request creates an infrastructure resource linked to the correct honeypot and organization, or returns a recorded provisioning error. |
| FR-019 | The platform manages honeypot lifecycle operations. | High | Start, stop, and delete requests invoke the corresponding provider operation and update the recorded lifecycle state based on its result. |
| FR-020 | The platform monitors infrastructure health. | High | When health data is available, the system records it and exposes a timestamped health state for the deployment. |
| FR-021 | The platform records deployment failures. | High | Force a provisioning or lifecycle operation to fail; the system stores the failure with deployment reference, time, and safe diagnostic detail, and exposes it to an authorized user. |
| FR-040 | Honeypots run in isolated environments, separate from production systems and other tenants. | Critical | Verify each honeypot is deployed in an isolated boundary with restricted network access. Attempts to access production resources or another tenant's honeypot are blocked, and the isolation configuration is auditable. |

## 1.5 Event Collection and Processing

| ID | Requirement | Priority | Acceptance check |
| --- | --- | --- | --- |
| FR-022 | The platform collects SSH interaction events. | High | Send a supported SSH interaction to a running SSH honeypot; a corresponding event is accepted into the ingestion flow with event time and source deployment. |
| FR-023 | The platform collects HTTP/HTTPS request events. | High | Send an HTTP or HTTPS request to a running web honeypot; a corresponding event is accepted into the ingestion flow with event time and source deployment. |
| FR-024 | The platform associates events with their honeypots. | High | Ingest an event from a known deployment; its stored record references that deployment. Events with unknown deployment references are rejected or quarantined and do not appear under another honeypot. |
| FR-025 | The platform associates events with the correct organization. | Critical | Ingest events for deployments in two organizations; each event is stored and returned only within its deployment's organization scope. |
| FR-026 | The platform processes events asynchronously. | High | Submit an event; ingestion acknowledges or queues it without waiting for downstream processing, and a worker later records a success or retryable failure state. |
| FR-027 | The platform stores collected events. | High | Successfully processed events can be retrieved with their original event time, type, deployment, and organization references intact. |
| FR-028 | Users can search and filter events. | High | An authorized user applies supported filters and search terms; only matching events from that user's organization are returned, with pagination for larger results. |

## 1.6 Dashboard and Analytics

| ID | Requirement | Priority | Acceptance check |
| --- | --- | --- | --- |
| FR-029 | Users can view an overview dashboard. | High | An authorized organization member opens the dashboard and receives summary data scoped to their organization. |
| FR-030 | Users can view total collected events. | High | The dashboard's event total matches the count of stored events for the selected organization and time range. |
| FR-031 | Users can view events grouped by honeypot type. | Medium | The dashboard returns event counts grouped by honeypot type; group totals reconcile with the total for the same time range. |
| FR-032 | Users can view event activity over time. | Medium | The dashboard returns time-bucketed event counts for the selected range, including empty buckets where applicable. |
| FR-033 | Users can view individual event details. | High | Selecting an event returns its stored details only if the user is authorized for the event's organization; otherwise access is denied. |

## 1.7 Alert Management

| ID | Requirement | Priority | Acceptance check |
| --- | --- | --- | --- |
| FR-034 | The platform generates alerts based on configured conditions. | Medium | Create a supported alert condition and produce a matching event; the system creates one alert linked to the triggering event and organization. Non-matching events do not trigger it. |
| FR-035 | Users can view generated alerts. | Medium | An authorized organization member lists alerts; only alerts for that organization are returned, including their condition and status. |
| FR-036 | Users can mark alerts as read. | Medium | An authorized user marks an unread alert as read; subsequent reads show the updated status and read timestamp. |

## 1.8 Audit and Administration

| ID | Requirement | Priority | Acceptance check |
| --- | --- | --- | --- |
| FR-037 | The platform records important user actions. | High | Perform a security-relevant action; an audit record captures actor, action, target, organization where applicable, and timestamp without exposing secrets. |
| FR-038 | Platform administrators can manage organizations. | High | A platform administrator can list and update organization status; a non-platform administrator is denied, and each change is audited. |
| FR-039 | Platform administrators can monitor system health. | High | A platform administrator can view service health and recent operational errors; users without that role cannot access the platform-wide view. |

## 2. MVP Boundaries

| Feature | MVP | Notes |
| --- | --- | --- |
| Authentication | Yes | Registration, login/logout, and role enforcement; password reset may follow if not needed for the first deployable slice. |
| Multi-tenancy | Yes | Organization membership and strict tenant data isolation are required. |
| SSH honeypot | Yes | Create, configure, deploy, inspect, start, and stop. |
| HTTP/HTTPS honeypot | Yes | Create, configure, deploy, inspect, start, and stop. |
| Event collection | Yes | SSH and HTTP/HTTPS event ingestion, organization association, storage, and filtering. |
| Dashboard | Yes | Overview, event totals, and event details; basic activity/grouping views can be delivered incrementally. |
| Basic alerts | Yes | Configured conditions, alert listing, and read status. |
| Advanced analytics | Later | Beyond basic event counts, grouping, and activity over time. |
| Multiple honeypot providers | Later | Start with the provider or runtime selected for the initial implementation. |
| Advanced reporting | Later | Scheduled, customizable, or cross-organization reports. |

## 3. MVP Acceptance Boundary

The MVP is complete when an authenticated organization administrator can create an organization, deploy an SSH or HTTP/HTTPS honeypot into an isolated environment, view its lifecycle status, and review events collected for that honeypot. Organization boundaries must be enforced for all deployment, event, dashboard, and alert data. Basic configured alerts and audit records must be available. Provisioning and lifecycle failures must be visible and recorded.

