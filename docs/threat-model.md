# Threat Model

This document identifies the main assets, trust boundaries, threats and planned controls for the concept.

## Assets

- Original user prompts.
- Sensitive values detected in prompts.
- Placeholder-to-value mappings.
- Encryption keys.
- Provider credentials.
- Restored model responses.
- Privacy policy configuration.

## Trust boundaries

1. User device and chat interface.
2. Local privacy-processing environment.
3. Local mapping store.
4. External model provider.
5. Logs, telemetry and backup systems.

## Primary threats

### Sensitive data bypasses detection

A detector may miss names, addresses, contextual identifiers or unusual formats.

**Planned controls:** fail-closed behavior where appropriate, configurable rules, confidence thresholds, representative tests and later integration of specialized PII detection.

### Mapping store disclosure

Anyone who obtains the reversible mapping can reconstruct the original values.

**Planned controls:** encryption at rest, user and conversation isolation, minimal retention, restricted access, secret management and no mapping values in logs.

### Placeholder manipulation

The model may alter, omit or invent placeholders.

**Planned controls:** exact placeholder grammar, response validation, rejection of unknown tokens and no approximate restoration.

### Prompt injection

User content or imported text may attempt to bypass privacy rules or request internal mappings.

**Planned controls:** treat all content as untrusted, keep policy enforcement outside the prompt, never expose mappings as model context and restrict external actions.

### Sensitive logging

Raw prompts, responses or mappings may leak through application logs or exceptions.

**Planned controls:** structured metadata-only logs, redaction, safe exception handling and explicit tests for logging behavior.

### Cross-conversation mapping access

A placeholder from one user or conversation may be restored using another mapping.

**Planned controls:** conversation-scoped identifiers, authorization checks and isolated storage namespaces.

### Provider or network compromise

Protected prompts may still reveal context or be intercepted.

**Planned controls:** TLS, provider due diligence, data-minimization rules and recognition that pseudonymization reduces but does not eliminate disclosure risk.

## Out of scope for the first concept

- Formal regulatory compliance certification.
- Protection against a fully compromised local host.
- Multimodal redaction.
- Production-grade identity and access management.
- Enterprise key-management infrastructure.
- Guaranteed detection of every sensitive entity.

## Security claim boundary

This project describes a privacy-preserving architecture. It does not claim that the future implementation will be completely secure, compliant or suitable for real sensitive data without independent testing and review.
