# Voice and model policy

## Fast path first

Direct commands must not depend on an LLM:

```text
voice -> speech-to-text -> Home Assistant native intent -> automation/device -> short reply
```

This path remains local and operational when an LLM service or Internet connection is unavailable.

## Model roles

| Role | Default choice | Permissions |
|---|---|---|
| Speech-to-text | Whisper pt-PT | Transcription only |
| Conversation and writing | AMALIA | No device-control tools |
| Complex tasks | Stronger specialist model, selected explicitly | Only the tools required for that task |
| Text-to-speech | Chatterbox pt-PT preferred; Piper fallback | Speech synthesis only |

AMALIA-FALA is a possible future European-Portuguese speech-to-text engine. It should be added only after a local benchmark proves it meets the desired latency and hardware limits. It is not a prerequisite for the initial voice pipeline.

## Response policy

- Keep device-control replies short and deterministic.
- Use AMALIA for conversational and writing-oriented replies in pt-PT.
- Do not use a language-model rewrite for safety-critical confirmations or factual task output.
- Benchmark both first-response latency and full-response latency before replacing a stable voice component.
