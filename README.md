Secure your agents at: CodeAstra.dev

## AI Agent Privacy Notice

Astra Sentinel found a possible pattern where sensitive user, customer, or patient data may be passed directly into an AI agent or LLM context.

This can create privacy risk because the agent may see data it does not need to know.

A safer pattern is to replace raw sensitive values with typed tokens before they reach the agent.

Example:

Before: Book appointment for John Smith, DOB 04/12/1988
After: Book appointment for [CVT:NAME:patient_name], DOB [CVT:DOB:patient_dob]

The agent can still perform the workflow, but it never sees the raw sensitive data.

Detected pattern examples:
```json
[
  {
    "pattern": "unprotected_ai_context",
    "evidence": "chatopenai(model='gpt-4o-mini')"
  }
]
```

This notice was generated from a privacy scan. Please review before merging.

Secure your agents at: CodeAstra.dev

---

# A2A + MCP Example

This project demonstrates communication between agents using the **Agent-to-Agent (A2A)** protocol in combination with the **Model-Context-Protocol (MCP)**.

---

## 🔧 Components

- **mcp_app.py**
  MCP server providing tools (functions/endpoints) that can be used by agents.

- **agentpartner.py**
  Agent B — uses tools exposed by the MCP server.

- **host_agent.py**
  Agent A — communicates with Agent B using the A2A protocol.

---

## ▶️ How to Run

### 1. Install dependencies

```bash
pip install -r requirements.txt
```

### 2. Start the MCP Server

```bash
python mcp_app.py
```

This will start the MCP server that exposes tool endpoints.

### 3. Run Agent B (agentpartner)

```bash
python agentpartner.py
```

Agent B will register itself and wait for instructions from Agent A.

### 4. Run Agent A (host agent)

```bash
python host_agent.py
```

Agent A initiates communication with Agent B using the A2A protocol and calls MCP tools via Agent B.

---

## ✅ Expected Result

Agent A sends a request to Agent B via A2A.
Agent B uses the MCP protocol to invoke tools and returns the result.

---

Feel free to extend this setup with more tools or agents!
