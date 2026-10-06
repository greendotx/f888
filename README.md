# FLUX X888

**FLUX X888** is a model-agnostic cognitive operating system for AI agents.

The design treats the language model as one replaceable component and puts the real system value in:
- intent routing
- planning and replanning
- memory
- retrieval
- tools
- specialist agents
- verification
- policy/approval
- observability
- evaluation
- replay
- voice and multimodality
- provider routing

## X888 architecture

```text
User
  │
  ▼
Gateway / API
  │
  ▼
Intent + Risk Router
  │
  ├── Fast path ───────────────► Answer
  │
  └── Cognitive path
        │
        ├── Memory recall
        ├── Retrieval
        ├── Planner
        ├── Specialist agents
        ├── Tool execution
        ├── Synthesis
        └── Independent verification
                    │
                    ▼
                 Policy
                    │
                    ▼
                 Answer
                    │
          ┌─────────┴─────────┐
          ▼                   ▼
       Trace                Memory
          │
          ▼
     Evaluation
          │
          ▼
   Regression / Improvement
```

## Design principles

1. **Provider agnostic** — OpenAI-compatible, local, custom or future providers.
2. **Fail closed** — tools are explicitly registered and dangerous actions can require approval.
3. **Evidence aware** — answers can carry evidence and provenance.
4. **Bounded self-improvement** — failures produce eval cases; code is not silently self-modified.
5. **Replayable** — a run can be reconstructed from its trace.
6. **Local-first capable** — remote APIs are optional adapters.
7. **Progressive complexity** — easy questions stay cheap and fast.

## Planned capabilities

- LLM routing by quality / latency / cost
- short-term + episodic + semantic + procedural memory
- hybrid retrieval and reranking
- MCP tool interoperability
- specialist agents
- parallel task graphs
- sandboxed code execution
- approval workflows
- voice / TTS abstraction
- multimodal attachments
- OpenTelemetry traces
- evaluation harness and regression suite
- semantic cache
- durable job execution

## Development

```bash
python -m venv .venv
source .venv/bin/activate
pip install -e ".[dev]"
cp .env.example .env
pytest -q
```

Run API:

```bash
uvicorn flux.api:app --reload --port 8787
```

## Security note

Do not execute arbitrary generated code directly on the host. The code-execution interface in X888 is deliberately abstract so a hardened sandbox can be plugged in later.
