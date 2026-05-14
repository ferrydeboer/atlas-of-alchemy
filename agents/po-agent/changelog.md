# PO Agent Changelog

All notable changes to the PO Agent skill definition, schemas, or configuration.

---

## [1.0.0] - 2025-05-14

### Added
- Initial PO Agent definition
- Trigger schema for minimal human input (just issue number)
- Input schema with issue reference, fetched content, and conversation context
- Output schema with three states: `work_item`, `needs_clarification`, `rejected`
- Structured acceptance criteria with slug IDs for traceability
- Decision log capturing rationale for key decisions
- SKILL.md with role definition, bootstrap flow, decision framework, and output format
- Three example runs demonstrating success, clarification, and rejection flows
- agent.yml with Haiku model, issue tracker read/write capabilities
- factory.yml for repository-level configuration

### Design Decisions
- **Single-concern enforcement**: PO agent rejects multi-concern requests rather than attempting to split them automatically. Splitting requires human judgment about priority and sequencing.
- **Fail-fast on ambiguity**: After 3 turns of clarification, reject rather than assume. Assumptions propagate errors downstream.
- **Decision log over conversation transcript**: Capture the "why" concisely rather than full conversation history to optimize token costs.
- **Issue enrichment**: Append refined requirements to issue body, post decision log as comment. Issue becomes single source of truth.
- **Host-agnostic design**: Uses `issue` instead of `githubIssue`; repository URL in factory.yml determines the issue tracker.