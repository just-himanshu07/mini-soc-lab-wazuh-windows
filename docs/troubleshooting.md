# Troubleshooting Log

Record each issue and only mark a resolution after validating it.

## Issue template

- Date:
- Component:
- Symptom/error:
- Relevant sanitized logs:
- Root cause:
- Fix attempted:
- Verification result:

## Common checks

- Confirm all expected Wazuh containers are running.
- Check container logs for startup errors.
- Confirm Windows can reach the manager on the configured agent port.
- Verify the agent's manager address and service status.
- Check system clock and certificate validity if TLS errors occur.
- Confirm the required Windows audit policy is enabled.
- Verify a test event appears in Wazuh before claiming event collection works.
