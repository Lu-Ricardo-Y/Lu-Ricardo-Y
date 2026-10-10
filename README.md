# Hi, I'm Lu-Ricardo-Y 👋

I build practical AI agents that answer with evidence, take actions with human approval, and make their behavior measurable. My current focus is RAG, tool-using agents, and reliable execution with Python and Go.

我关注能引用依据、在关键写操作前请求人工确认，并能通过评测检验效果的 AI Agent 系统。

## Featured projects

### 🛍️ [Merchant Support Agent](https://github.com/Lu-Ricardo-Y/merchant-support-agent) · RAG → answer → approved action

An end-to-end e-commerce support Agent using sample policy documents and a local ticket store. It connects knowledge retrieval, evidence-grounded responses, ticket workflows, and evaluation in one inspectable system.

- **Grounded answers:** Combines BM25 and Qdrant vector retrieval with RRF. Qwen responses are tied to retrieved policies with backend-controlled citations; the system can decline when evidence is insufficient.
- **Human-approved actions:** The Agent can check ticket status and prepare ticket creation. A new SQLite ticket is written only after explicit user confirmation, with parameter validation and idempotency checks.
- **Evaluation and delivery:** Includes separate development/test data, retrieval and generation checks, Agent run traces, Docker setup, and [demo screenshots](https://github.com/Lu-Ricardo-Y/merchant-support-agent/tree/main/docs/images).

This is the project that best represents my interest in building useful AI agents with clear evidence, controlled tools, and testable behavior.

### 🔐 [AgentGate](https://github.com/Lu-Ricardo-Y/AgentGate) · safer Agent execution

A Go-based reference implementation using a local Ollama model. It explores tenant-aware authorization, human approval for writes, audit trails, replay protection, and explicit failure handling. Developed collaboratively with [@kimzclandi](https://github.com/kimzclandi); [contributions are documented](https://github.com/Lu-Ricardo-Y/AgentGate/blob/main/AUTHORS.md).

### 📈 [Bearing Fault Diagnosis](https://github.com/Lu-Ricardo-Y/bearing-fault-diagnosis) · reproducible applied ML

A collaborative fork built around CWRU vibration data, signal processing, Random Forest and 1D CNN diagnosis, physical-frequency features, robustness tests, and a Streamlit demo. Its health index describes deviation within recordings; it does not claim remaining-useful-life prediction.

---

**Interests:** AI Agents · RAG · evaluation · human-in-the-loop systems · Python · Go
