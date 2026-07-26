# Roadmap

## Phase 0 — Concept and architecture

Current phase.

- Define the privacy problem and trust boundary.
- Document the pseudonymization flow.
- Identify threats, limitations and technical decisions.
- Use only synthetic examples.

## Phase 1 — Text MVP

- Build a local Python application.
- Add a minimal Streamlit chat interface.
- Implement structured-data detection with regular expressions.
- Generate conversation-scoped placeholders.
- Add a model-provider adapter and a local mock adapter.
- Validate and restore exact placeholders.
- Add tests proving that original values never reach the adapter.

## Phase 2 — Protected local storage

- Add SQLite storage for conversations and mappings.
- Encrypt reversible mapping values.
- Define retention and deletion rules.
- Prevent sensitive data from reaching logs and exceptions.

## Phase 3 — Stronger privacy detection

- Evaluate Microsoft Presidio, spaCy or specialized PII models.
- Add configurable entity categories and confidence thresholds.
- Add Spanish and English test datasets with synthetic values.
- Measure false positives and false negatives.

## Phase 4 — Multiple providers and policy controls

- Support multiple model adapters.
- Add provider and model selection policies.
- Add per-category blocking rules.
- Add user-visible warnings and manual-review paths.
- Track token usage without logging sensitive content.

## Phase 5 — Multi-user application

- Move the backend to FastAPI when needed.
- Add authentication, authorization and conversation isolation.
- Add encrypted secret management.
- Add structured audit events and rate limits.

## Phase 6 — Multimodal research

- Explore documents and images only after the text boundary is proven.
- Evaluate OCR redaction, faces, signatures and metadata.
- Treat audio and video as separate privacy projects because they introduce voice, face and temporal information.

## Definition of a successful first MVP

The first MVP is successful when automated tests can demonstrate that:

1. Configured sensitive values are replaced before the model adapter is called.
2. The adapter never receives the original values.
3. The mapping remains local.
4. Exact placeholders can be restored correctly.
5. Unknown or malformed placeholders are rejected.
6. Privacy-pipeline errors block external transmission.
