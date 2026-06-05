# 🛡️ Secure AI Chat Gateway
### Lightweight Prompt Injection Detection & AI Governance Middleware for Organizational Chatbot Systems

![Status](https://img.shields.io/badge/Status-FYP%20Part%201%20%7C%20Design%20Phase-yellow)
![Project Type](https://img.shields.io/badge/Project-Final%20Year%20Project-blue)
![Domain](https://img.shields.io/badge/Domain-AI%20Security%20%7C%20Governance-purple)
![Stack](https://img.shields.io/badge/Stack-React%20%7C%20Node.js%20%7C%20MongoDB%20%7C%20Ollama-green)

A prototype-focused security middleware designed to sit between users and an AI chatbot, evaluating prompts before they reach the model. The project explores how organizations can add their own governance layer on top of LLM-based chatbot systems through prompt monitoring, policy checks, risk scoring, session-aware detection, and audit logging.

> **Current stage:** This repository currently represents the first half of the Final Year Project, focusing on problem formulation, literature review, system architecture, requirements analysis, and early interface/architecture visualization. Full implementation will be developed in the next phase.

---

## 📌 Project Overview

Large Language Model (LLM)-powered chatbots are increasingly used in organizational environments for internal support, knowledge retrieval, workflow assistance, and customer-facing automation. However, these systems also introduce security and governance risks, especially when users attempt to manipulate chatbot behavior through prompt injection, role escalation, or multi-turn semantic attacks.

Most built-in AI moderation systems are designed for broad public use. They may not fully reflect an organization’s internal policies, confidentiality rules, audit requirements, or acceptable-use boundaries.

**Secure AI Chat Gateway** proposes a lightweight middleware-based approach where prompts are evaluated before being forwarded to the AI model. Instead of trying to replace enterprise-grade AI security tools, this project focuses on demonstrating a transparent, customizable, and prototype-scale governance layer for organizational chatbot systems.

---

## 🎯 Problem Background

Organizations adopting AI chatbot systems may face several practical issues:

- **Prompt injection attacks** — crafted prompts may attempt to override system instructions or manipulate AI behavior.
- **Semantic manipulation** — attackers may paraphrase suspicious prompts to bypass simple keyword filters.
- **Multi-turn attacks** — malicious intent may be built gradually across multiple conversation turns.
- **Limited organization-specific control** — public moderation systems may not understand internal policies or sensitive data boundaries.
- **Low audit visibility** — black-box moderation makes it difficult to explain why a prompt was allowed, blocked, or flagged.

This project addresses these concerns through a layered gateway that combines rule-based checks, semantic similarity analysis, session monitoring, risk scoring, output validation, and audit logs.

---

## 💡 What Makes This Project Different

This project is not positioned as a “perfect AI firewall.” Instead, it focuses on a more realistic and explainable governance layer that can be adapted to organizational needs.

| Focus Area | How This Project Approaches It |
|---|---|
| Prompt Injection Detection | Combines regex rules, semantic similarity, and contextual session tracking |
| Organization-Specific Governance | Allows custom policies and restricted prompt patterns to be defined |
| Explainability | Stores risk indicators, similarity scores, detection reasons, and logs |
| Lightweight Deployment | Designed for prototype-scale local deployment rather than heavy enterprise infrastructure |
| Multi-Turn Awareness | Uses recent conversation history to detect gradual manipulation attempts |
| Educational Value | Built to demonstrate AI security concepts clearly in a controlled environment |

---

## ✨ Planned Core Features

### 🔎 Prompt Interception
All user prompts pass through the middleware layer before reaching the AI model.

### 🧱 Rule-Based Filtering
Detects obvious suspicious patterns such as jailbreak attempts, role escalation phrases, restricted command structures, and prompt leakage requests.

### 🧠 Semantic Similarity Analysis
Uses embedding-based similarity checking to detect paraphrased or semantically similar prompt injection attempts that may bypass simple keyword matching.

### 📚 Retrieval-Assisted Policy Checking
Compares prompts against stored organizational policy references and suspicious prompt patterns using a vector database.

### 🧵 Session-Aware Monitoring
Tracks recent prompts in a lightweight sliding context window to detect suspicious behavior across multiple conversation turns.

### ⚠️ Risk Scoring
Generates a risk score based on regex matches, semantic similarity, policy retrieval results, and session behavior.

### ✅ Output Validation
Checks AI-generated responses before returning them to the user to reduce policy violations, sensitive information exposure, or prompt leakage.

### 📋 Audit Logging
Stores prompts, risk scores, flags, decisions, and monitoring results for administrator review and traceability.

### 📊 Admin Monitoring Dashboard
Provides visibility into suspicious prompts, blocked requests, risk trends, and audit records.

---

## 🏗️ Proposed System Architecture

> Diagram placeholder — replace this with your actual architecture image later.

```md
![System Architecture](docs/system-architecture.png)
```

```text
User
 │
 ▼
Frontend Chat Interface
 │
 ▼
Secure AI Chat Gateway Middleware
 ├─ Regex-Based Filter
 ├─ Semantic Similarity Analyzer
 ├─ Retrieval-Assisted Policy Checker
 ├─ Session-Aware Monitor
 ├─ Risk Scoring Engine
 ├─ Audit Logger
 └─ Output Validation Layer
 │
 ▼
Local AI Model / Chatbot Engine
 │
 ▼
Validated Response Returned to User
```

The middleware acts as the central governance layer. It does not directly replace the AI model, but controls and monitors the interaction flow between the user and the chatbot.

---

## 🔄 Prompt Processing Workflow

> Diagram placeholder — replace this with your actual workflow image later.

```md
![Prompt Processing Workflow](docs/prompt-processing-workflow.png)
```

```text
1. User submits prompt
2. Middleware receives prompt
3. Regex filter checks known suspicious patterns
4. Semantic analyzer compares prompt with suspicious prompt embeddings
5. Policy checker retrieves related governance rules or attack patterns
6. Session monitor evaluates recent conversation context
7. Risk score is calculated
8. Prompt is either blocked, flagged, or forwarded to the AI model
9. AI response is validated
10. Interaction is logged for audit and monitoring
```

---

## 🧪 Detection Logic Concept

```python
risk_score = 0

# 1. Rule-based filtering
if regex_match(prompt, suspicious_patterns):
    risk_score += 30

# 2. Semantic similarity checking
similarity_score = compare_embedding(prompt, suspicious_prompt_vectors)
if similarity_score >= SEMANTIC_THRESHOLD:
    risk_score += 35

# 3. Session-aware monitoring
if detect_multi_turn_manipulation(session_history):
    risk_score += 25

# 4. Policy retrieval check
if violates_retrieved_policy(prompt, organization_policies):
    risk_score += 20

# 5. Decision
if risk_score >= BLOCK_THRESHOLD:
    block_prompt()
elif risk_score >= REVIEW_THRESHOLD:
    flag_for_review()
else:
    forward_to_ai_model()
```

The scoring model is intentionally transparent so that administrators can understand why a prompt was blocked or flagged.

---

## 🧰 Planned Technology Stack

| Layer | Planned Technology | Purpose |
|---|---|---|
| Frontend | React | Web-based chatbot interface and admin dashboard |
| Backend / Middleware | Node.js + Express.js | API gateway, filtering logic, risk scoring, and request routing |
| Operational Database | MongoDB | Stores users, prompts, logs, policies, and monitoring records |
| Vector Database | ChromaDB | Stores embeddings for suspicious prompts and policy references |
| Session Tracking | Redis | Maintains short-term conversation context for multi-turn analysis |
| Local AI Model | Ollama | Runs the chatbot model locally for prototype demonstration |
| Semantic Embeddings | Sentence Transformers | Converts prompts into embeddings for similarity analysis |
| Containerization | Docker | Improves portability and deployment consistency |

---

## 📊 Planned Evaluation Metrics

The system is planned to be evaluated using benign prompts, direct prompt injection attempts, paraphrased attacks, and multi-turn adversarial scenarios.

| Metric | Purpose |
|---|---|
| Detection Rate | Measures how many malicious prompts are correctly detected |
| False Positive Rate | Measures how often benign prompts are wrongly flagged |
| Precision | Measures how reliable flagged detections are |
| Recall | Measures how many actual attacks are successfully captured |
| F1-Score | Balances precision and recall |
| Semantic Robustness | Tests whether paraphrased attacks can still be detected |

---

## 📁 Repository Structure

```text
secure-ai-chat-gateway/
├── docs/
│   ├── system-architecture.png
│   ├── prompt-processing-workflow.png
│   └── research-notes.md
│
├── diagrams/
│   ├── attack-surface.png
│   └── middleware-flow.png
│
├── frontend/                 # Planned React chatbot UI
│
├── backend/                  # Planned Node.js/Express middleware
│
├── data/                     # Planned sample prompts and policy datasets
│
├── README.md
└── LICENSE
```

> The implementation folders are currently placeholders and will be populated during the development phase.

---

## 🚧 Current Development Status

### Completed / In Progress

- Problem background and motivation
- Literature review on AI chatbot security and prompt injection
- Existing system analysis
- Proposed middleware architecture
- Technology stack comparison
- Functional and non-functional requirements
- Initial system workflow and interface design
- Early architecture and monitoring dashboard visualizations

### Upcoming Development Work

- Build the React chatbot interface
- Implement Node.js/Express middleware
- Add regex-based filtering rules
- Integrate semantic similarity checking with embeddings
- Connect ChromaDB for suspicious prompt and policy retrieval
- Add Redis-based session tracking
- Implement risk scoring and output validation
- Build admin dashboard for logs and monitoring
- Prepare attack simulation test cases
- Evaluate detection performance using defined metrics

---

## 🔐 Scope and Limitations

This project is designed as a Final Year Project prototype and does not claim to fully eliminate all prompt injection or LLM security risks.

The current goal is to demonstrate how layered middleware controls can improve visibility, explainability, and organization-specific governance in AI chatbot systems.

The prototype focuses mainly on:

- Direct prompt injection attempts
- Role escalation prompts
- Suspicious semantic paraphrasing
- Multi-turn manipulation patterns
- Policy-based prompt monitoring
- Audit logging and administrator visibility

It does not aim to replace enterprise AI security platforms or provide complete protection against all possible AI-related threats.

---

## 🎓 Academic Context

**Project Title:** Secure AI Chat Gateway with Prompt Injection Detection for Organisation System  
**Project Type:** Final Year Project / Undergraduate Project  
**Institution:** Universiti Teknologi Malaysia (UTM)  
**Faculty:** Faculty of Computing  
**Programme:** Bachelor of Computer Science (Computer Networks & Security)  
**Author:** Mah Wilson  

---

## 📌 Repository Note

This repository is being uploaded early to document the project direction, design decisions, architecture planning, and research progress before the full development phase begins.

As implementation progresses, this repository will be updated with working source code, datasets, testing scripts, screenshots, and deployment instructions.

---

## 📄 License

License to be added.

---

**Secure AI Chat Gateway** — A lightweight step toward more transparent and organization-aware AI chatbot governance.
