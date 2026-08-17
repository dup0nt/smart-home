# Architecture

## Goals

- Local-first voice control with an Internet-independent path for basic device actions.
- European-Portuguese conversation and writing where it adds value.
- Multiple input channels without exposing device APIs directly to messaging apps or LLMs.
- Clear separation between device control, conversation, and complex task execution.
- Least-privilege access to automation tools.

## Reference design

```mermaid
flowchart TD
    voice["Voice satellite"] --> stt["Local STT\nWhisper pt-PT by default"]
    chat["Chat channels\nWhatsApp, Telegram, WebChat"] --> claw["OpenClaw Gateway\nchannels and sessions"]

    stt --> ha["Home Assistant Assist"]
    ha -->|"Direct device command"| native["Native intents, scenes\nand automations"]
    native --> devices["Home Assistant devices\nand actuators"]

    ha -->|"Conversation"| claw
    claw -->|"Normal conversation"| amalia["AMALIA\npt-PT conversation and writing\nno device-control tools"]
    claw -->|"Explicit complex task"| task["Task agent\nstronger specialist model"]

    task -->|"restricted tools only"| mcp["Home Assistant\nAssist API / MCP"]
    mcp --> devices

    amalia --> response["Response text"]
    task --> response
    native --> response
    response --> tts["Local TTS\nChatterbox pt-PT preferred\nPiper fallback"]
    tts --> voice

    classDef local fill:#e8f5e9,stroke:#2e7d32,color:#1b5e20;
    classDef guarded fill:#fff3e0,stroke:#ef6c00,color:#e65100;
    class amalia,stt,tts local;
    class ha,native,mcp,task guarded;
```

## Ownership boundaries

| Component | Owns | Does not own |
|---|---|---|
| Home Assistant | Device state, automations, voice pipeline, permissions | General personal-agent memory |
| OpenClaw | Chat channels, sessions, agent routing | Direct device protocols |
| AMALIA | pt-PT conversation and writing | Device control or complex task planning |
| Task agent | Explicit research, planning, and other complex work | Unrestricted smart-home access |
