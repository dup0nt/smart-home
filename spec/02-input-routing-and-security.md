# Input routing and security

## No standalone router initially

Use existing responsibilities instead of introducing another service:

- Home Assistant handles voice input and direct device commands.
- OpenClaw receives chat-channel messages and routes them to agents.
- Home Assistant forwards voice conversations to OpenClaw only when native handling is not the appropriate path.

Start with explicit routes:

| Input | Route |
|---|---|
| Direct home command | Home Assistant native intent, scene, or automation |
| Normal chat | AMALIA conversation agent |
| `!casa` or equivalent explicit command | Restricted Home Assistant control agent |
| `!tarefa` or equivalent explicit command | Stronger task agent |

Automatic classification can be added later as an OpenClaw skill after observing real requests. It does not require a separate microservice.

## Tool boundary

LLMs and chat channels must not call devices directly. Home Assistant is the only device-control boundary.

- Expose only approved Home Assistant entities, scenes, and scripts through its Assist API or MCP endpoint.
- Keep task-agent access separate from conversational access.
- Do not grant shell, file, browser, email, or messaging access to the home-control agent.
- Require explicit confirmation for safety-sensitive actions.
- Keep group chats disabled for device control unless deliberately allowlisted.

## Privacy boundary

The system may be local-first while a chat transport is not. Messages sent through a third-party chat application still traverse that service. Use a local web interface or self-hosted chat system when the transport itself must remain private.
