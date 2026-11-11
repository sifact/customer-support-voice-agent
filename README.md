# Customer Support Voice Agent

Phone voice agent for customer support: Twilio, speech-to-text, LLM with RAG and tools, text-to-speech. Turn detection, interruption handling, model routing and human handoff.

> **Status: in progress.** The repository is set up and the design is being written. The code, results and demo are added as each step on the roadmap below is finished. All numbers in this README come from evaluation runs in this repo; until a run exists, a metric is listed as planned, not reported.

## The problem
Support lines spend most of their time on the same questions: order status, opening hours, booking a technician. Callers wait in queues while agents repeat themselves.

## What it does
- Answers the phone, listens, and replies in a natural voice.
- Answers FAQs from the company knowledge base (RAG).
- Checks order status and books appointments through tools.
- Hands complex or upset callers to a human, with a summary.
- Handles real-call problems: end of turn, interruptions, silence.
- Routes simple intents to a cheap model and hard questions to a stronger one.

## How it works
```
caller ─► Twilio ─► media server ─► STT ─► LLM (RAG + tools + guardrails) ─► TTS ─► caller
                                 │                    │
                          VAD / turn detection    handoff to human
```

## Tech stack (planned)
- Python, LiveKit Agents (self-hosted) or ElevenLabs Agents (managed)
- Twilio telephony
- Deepgram or Cartesia speech-to-text, ElevenLabs text-to-speech
- LLM with tool calling and model routing
- Retrieval layer reused from enterprise-rag

## How it will be evaluated
- Task success on scripted test calls (FAQ, order status, booking, handoff)
- Voice-to-voice latency p50/p95 and time to first audio
- Turn-taking errors: talking over the caller, cutting them off
- Answer faithfulness against the knowledge base
- Cost per call by model route

## Roadmap
- [ ] Choose LiveKit vs ElevenLabs
- [ ] Text-only dialogue loop with RAG and tools
- [ ] Speech in/out
- [ ] Twilio phone number
- [ ] VAD, turn detection and interruption handling
- [ ] Model routing
- [ ] Human handoff
- [ ] Scripted call test suite
- [ ] Web call demo

## Project layout
```
src/voice_agent/
├── telephony/
├── speech/
├── dialogue/
├── tools/
├── evaluation/
├── serving/
tests/
```

## Related projects
- [enterprise-rag](https://github.com/sifact/enterprise-rag): company assistant with role-based access, hybrid search, guardrails and evals.
