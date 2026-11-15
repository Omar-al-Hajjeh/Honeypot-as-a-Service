# Honeypot-as-a-Service Platform

Honeypot-as-a-Service (HaaS) is a platform for provisioning and managing isolated honeypots, collecting interaction data, and helping operators review suspicious activity from one place.

## Project structure

- `docs/01-requirements/` — project overview, requirements, and scope
- `backend/` — backend services (to be implemented)
- `frontend/` — web interface (to be implemented)

## Status

Requirements and initial project structure are being established. Backend and frontend implementation has not started.

## Requirements documents

- [Project overview](docs/01-requirements/project-overview.md)
- [Functional requirements](docs/01-requirements/functional-requirements.md)
- [Non-functional requirements](docs/01-requirements/non-functional-requirements.md)
- [Project scope](docs/01-requirements/project-scope.md)

## Security note

Honeypots are intentionally exposed decoys. Deploy them only on infrastructure you control, isolate them from production systems, and follow applicable laws and organizational policies.
