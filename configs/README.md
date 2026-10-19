# Configuration Examples

This directory contains sanitized configuration examples for the Mini SOC Lab using Wazuh SIEM, Docker, Kali Linux, and Windows 11.

## Purpose

- Document Wazuh agent and manager configuration settings.
- Maintain safe, reusable examples for lab deployment.
- Help troubleshoot agent connectivity and event collection.

## Security Guidelines

- Never commit passwords, API tokens, private keys, agent enrollment keys, or certificates.
- Replace real IP addresses and hostnames with placeholders where appropriate.
- Remove sensitive information before publishing configuration files.
- Keep local environment files and secrets outside the public repository.

## Configuration Files

Add only configuration examples that have been reviewed and sanitized.

- `ossec.conf.example` — example Wazuh agent configuration.
- `docker.env.example` — placeholder environment variable names for local setup.

These are example filenames; add the files only when you have prepared valid configurations for your actual lab.

**Note:** Example configurations must be reviewed and adapted to the installed Wazuh version before use.
