# Deployment and operations

## Services

Run the initial stack on one Linux host with Docker Compose:

- Home Assistant;
- OpenClaw Gateway;
- local speech-to-text;
- local text-to-speech;
- AMALIA text model;
- optional stronger task-model provider;
- optional MQTT broker for future integrations.

Kubernetes is not required for a single-host installation.

## Network boundaries

- Connect the server by Ethernet where possible.
- Put automation devices and voice satellites on a dedicated IoT network.
- Allow Home Assistant to reach automation devices.
- Do not allow IoT devices unrestricted access to personal computers or the Internet.
- Keep Home Assistant, OpenClaw, and model APIs private to the local network or a VPN.

## Operational rules

- Use persistent volumes and verified backups.
- Store credentials in an ignored `.env` file or a secret manager; never commit them.
- Pin and update services one at a time, testing voice control after every update.
- Use DHCP reservations or local DNS for infrastructure endpoints.
- Measure latency, GPU memory, and recovery after restarts before expanding the system.
