# Context Diagram – Honeypot-as-a-Service (HaaS)

## 1. Overview

The Context Diagram illustrates the high-level interaction between the Honeypot-as-a-Service (HaaS) system and its external actors. It defines the system boundary and shows how external entities interact with the platform.

The diagram provides a simplified view of the system without describing its internal components or implementation details.

## 2. Purpose

The main purposes of this diagram are to:

- Identify the external actors interacting with the HaaS platform.
- Define the boundary between the system and its external environment.
- Illustrate the main interactions between actors and the system.
- Establish a clear understanding of the system scope.
- Provide a foundation for defining functional requirements and system architecture.

## 3. External Actors

The following actors interact with the HaaS platform:

| Actor | Description |
|---|---|
| Administrator | Manages the platform, users, system configurations, and overall operations. |
| Customer | Uses the platform to deploy and manage honeypots and monitor collected attack information. |
| Attacker | Interacts with deployed honeypots, generating activity that the system captures and records. |

## 4. System Scope

The HaaS platform provides honeypot deployment and monitoring capabilities through two main honeypot types:

- **SSH Honeypot:** Simulates an SSH service to capture and analyze suspicious interactions.
- **HTTP/HTTPS Honeypot:** Simulates web services to capture and analyze suspicious HTTP/HTTPS requests.

The platform acts as an intermediary between customers, administrators, attackers, and the deployed honeypot services.

## 5. Main Interactions

The diagram represents the following high-level interactions:

- **Administrator ↔ HaaS:** Platform administration, user management, and system configuration.
- **Customer ↔ HaaS:** Account access, honeypot deployment, configuration, monitoring, and attack-data visualization.
- **Attacker → Honeypots:** Interaction with exposed SSH and HTTP/HTTPS honeypot services.
- **HaaS → Customer:** Provides captured activity, logs, and monitoring information.

## 6. Diagram

![HaaS Context Diagram](context-diagram.png)

## 7. Scope and Limitations

This diagram focuses on the external environment and high-level system interactions. It does not represent:

- Internal software components and modules.
- Database structure and relationships.
- Detailed communication protocols.
- Internal processing workflows.
- Deployment infrastructure.

These details will be addressed in subsequent software design diagrams.

## 8. Related Documentation

- [Use Case Diagram](../use-case-diagram/README.md)
- [Functional Requirements](../../01-requirements/functional-requirements.md)

---

**Project:** Honeypot-as-a-Service (HaaS)  
**Document Type:** Software Design – Context Diagram