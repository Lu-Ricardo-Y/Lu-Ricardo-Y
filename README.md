**English** · [简体中文](./README.zh-CN.md)

# Lu-Ricardo-Y

I work on AI agents and RAG systems. The part that interests me most is what surrounds a model response: where the evidence came from, when the system should say it does not know, what an agent is allowed to change, and how to test those decisions. I mostly build with Python and Go.

## Merchant Support Agent

This is the project I would show first. I built an e-commerce support agent that goes from policy retrieval and answering to ticket handling, using sample policies, orders, and tickets. It is a local demonstration rather than an integration with a live commerce platform.

I started with policy documents that carry version, status, and section metadata, then assembled 120 hand-labeled cases covering ordinary questions, exceptions, conflicting policy versions, missing evidence, tool calls, and approval before writes. For retrieval, I use BM25 alongside a local BGE embedding model and Qdrant. BM25 handles exact policy terms, numbers, and version references well; vector search helps with conversational phrasing. RRF combines their rankings.

Qwen writes the answer, but it does not get to invent its sources. The backend checks whether the retrieved material supports the question and builds citations from the documents actually found. If a question adds a condition the policies do not cover, the system can decline instead of making a confident promise. On the action side, the agent can look up tickets and prepare a new one. Creation stays pending until the user confirms; the tool checks that state again before writing to SQLite, with parameter validation and an idempotency key to prevent duplicate writes.

I kept the rough edges in the evaluation report. On the first held-out test, hybrid retrieval reached **94.59% Recall@5**, while RAG behavior matching was **75%**. A request phrased as “create a high-priority ticket” also exposed a gap in intent routing. I added those failures to regression tests and kept the original test results visible instead of replacing them with post-fix numbers. The repository includes Docker setup, a demo page, run traces, and scripts for retrieval, answer, and agent-route evaluation.

[Code](https://github.com/Lu-Ricardo-Y/merchant-support-agent) · [Evaluation results and failure analysis](https://github.com/Lu-Ricardo-Y/merchant-support-agent/blob/main/docs/RESULTS.md) · [Demo screenshots](https://github.com/Lu-Ricardo-Y/merchant-support-agent/tree/main/docs/images)

## Other projects

**[AgentGate](https://github.com/Lu-Ricardo-Y/AgentGate)** is a Go reference implementation for safer agent execution with a local Ollama model. It focuses on tenant and resource permissions, approval for writes, audit records, and failure handling. I worked on it with [@kimzclandi](https://github.com/kimzclandi); the [contribution notes](https://github.com/Lu-Ricardo-Y/AgentGate/blob/main/AUTHORS.md) are in the repository.

**[Bearing Fault Diagnosis](https://github.com/Lu-Ricardo-Y/bearing-fault-diagnosis)** is a collaborative fork using CWRU vibration data for signal processing, bearing-fault classification, physical-frequency features, and robustness tests, with a Streamlit demo. Its health index describes changes within a recording; it is not presented as a remaining-useful-life predictor.
