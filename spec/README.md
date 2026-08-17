# Local-first voice and automation architecture

This is a shareable reference architecture for a private, local-first assistant built with Home Assistant, OpenClaw, local speech services, and optional local or cloud language models.

It intentionally excludes house-specific details such as rooms, devices, vendors, prices, IP addresses, network names, floor plans, credentials, and personal data.

## Reading order

1. [Architecture](00-architecture.md)
2. [Voice and model policy](01-voice-and-model-policy.md)
3. [Input routing and security](02-input-routing-and-security.md)
4. [Deployment and operations](03-deployment-and-operations.md)

## Design principle

> Use AMALIA where pt-PT wording matters: normal conversation and writing, not every request or device action.

The architecture keeps direct home control deterministic, fast, and independent from general-purpose LLMs.
