# Mini SOC Lab: Wazuh SIEM & Windows Endpoint Monitoring

**Project type:** Cybersecurity | SOC Operations | SIEM | Endpoint Monitoring  
**SIEM:** Wazuh  
**Host environment:** Kali Linux  
**Virtualization:** VMware Workstation  
**Monitored endpoint:** Windows 11  
**Deployment approach:** Docker-based Wazuh single-node lab

## 1. Project Overview

This project documents the setup and validation of a small Security Operations Center (SOC) lab using Wazuh SIEM and a Windows 11 endpoint.

The goal is to understand how endpoint security events are collected, centralized, and investigated. The lab focuses on configuring the Wazuh platform, connecting a Windows agent, validating event collection, and investigating Windows Security events such as failed logon attempts.

**Current status:** Setup and integration are being validated. Mark a component as completed only after confirming it works in the lab.

## 2. Objectives

- Deploy Wazuh components for a home lab.
- Connect a Windows 11 endpoint to Wazuh using the Wazuh agent.
- Verify agent connectivity and event ingestion.
- Understand Windows Security Event Logs.
- Investigate failed logon attempts (Event ID 4625).
- Practice alert triage, evidence collection, and basic incident investigation.
- Document setup issues and troubleshooting steps.

## 3. Lab Architecture

```text
Windows 11 Endpoint
      |
      | Wazuh Agent
      | Security Event Logs
      v
Kali Linux Host
  └── Docker
      ├── Wazuh Manager
      ├── Wazuh Indexer
      └── Wazuh Dashboard
              |
              v
      Alert Review & Investigation
```

The Windows endpoint and Kali host should have network connectivity that allows the agent to reach the Wazuh manager. Configure VMware networking and host firewall rules to suit the lab network.

## 4. Lab Environment

| Component | Role |
|---|---|
| Kali Linux | Host environment for the Wazuh stack |
| VMware Workstation | Virtualization |
| Windows 11 | Endpoint generating security events |
| Wazuh Manager | Receives and analyzes agent data |
| Wazuh Indexer | Stores and indexes alert data |
| Wazuh Dashboard | Interface for reviewing alerts |
| Docker | Runs the Wazuh components |

Record your actual versions and network settings in `docs/lab-environment.md`. Do not publish passwords, private keys, tokens, or sensitive network details.

## 5. Implementation Plan

### Step 1 — Deploy Wazuh

- Deploy the Wazuh single-node Docker environment.
- Confirm that the manager, indexer, and dashboard containers are running.
- Check service logs for startup or certificate errors.
- Open the dashboard and verify that it is accessible.

### Step 2 — Configure Network Connectivity

- Confirm that Kali Linux and Windows can communicate over the selected lab network.
- Verify the Wazuh agent can reach the manager on the configured agent communication port.
- Review host firewall and VMware network settings if the agent cannot connect.
- Avoid exposing the dashboard or agent ports publicly; keep the lab on a trusted network.

### Step 3 — Install and Enroll the Windows Agent

- Install the Wazuh agent on Windows 11.
- Configure the manager address to point to the Kali host's reachable lab IP.
- Enroll or register the agent using the supported Wazuh workflow.
- Start the agent service.
- Confirm the endpoint appears as active in the Wazuh dashboard.

### Step 4 — Validate Event Collection

- Generate a controlled test event on the Windows endpoint.
- Confirm the event is collected and visible in Wazuh.
- Record the event timestamp, endpoint name, event ID, and alert details.
- Do not proceed to claim detection success until the event is visible in the platform.

## 6. Windows Event Investigation: Failed Logons

**Event ID:** `4625`  
**Meaning:** A user account failed to log on.

Investigation questions:

- Which account was involved?
- What host generated the event?
- What was the logon type?
- What source workstation or IP is recorded, if available?
- Were there repeated failures in a short period?
- Did a successful logon occur after the failures?
- Is the behavior expected, or does it need escalation?

A single failed logon does not prove a brute-force attack. Validate repetition, timing, account context, source information, and related events before concluding.

## 7. Investigation Workflow

```text
Alert or Security Event
        |
        v
Validate timestamp and endpoint
        |
        v
Review account and logon details
        |
        v
Correlate related failed/successful logons
        |
        v
Assess frequency and context
        |
        v
Document findings and next steps
```

## 8. Troubleshooting Notes

Document issues and their verified resolutions in `docs/troubleshooting.md`.

Useful checks include:

- Are all Wazuh containers running?
- Is the dashboard reachable from the lab network?
- Does the Windows agent point to the correct manager address?
- Is the configured agent communication port reachable?
- Is the agent service running?
- Are certificates valid and system clocks synchronized?
- Are relevant Windows audit policies enabled?
- Is the expected event visible in the Wazuh dashboard?

Do not paste credentials, API keys, agent keys, or private certificates into public issues or repository files.

## 9. Evidence & Screenshots

Add genuine screenshots from your own lab to the `screenshots/` directory, for example:

- `wazuh-dashboard.png`
- `docker-containers.png`
- `windows-agent-active.png`
- `event-4625-investigation.png`

Only include screenshots that you have actually captured. Redact public IPs, usernames, tokens, internal details, and other sensitive information where necessary.

## 10. Skills Practiced

- SIEM deployment concepts
- Wazuh manager, indexer, and dashboard
- Docker-based lab deployment
- Windows endpoint monitoring
- Windows Security Event Log analysis
- Failed-logon investigation
- Agent connectivity troubleshooting
- Basic alert triage and incident documentation

## 11. Future Improvements

- Create a dashboard for authentication events.
- Build and validate a threshold-based detection for repeated failed logons.
- Correlate failed logons with subsequent successful logons.
- Add Sysmon telemetry and investigate process creation events.
- Document a complete incident timeline and recommended response steps.

## Disclaimer

This project is for educational and defensive security monitoring. Perform testing only on systems you own or are authorized to monitor. Do not expose lab services publicly or commit secrets to this repository.
