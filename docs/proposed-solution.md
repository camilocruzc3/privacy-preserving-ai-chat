# Proposed Solution

The proposed system is a local privacy gateway positioned between the chat interface and external AI model providers.

## Processing sequence

1. The user submits a text request.
2. The detector identifies configured categories of sensitive information.
3. The pseudonymizer replaces each value with a scoped placeholder.
4. The mapping is stored inside the local trust boundary.
5. Only the protected prompt is sent through the model adapter.
6. The model returns a response that may contain placeholders.
7. The response validator verifies every placeholder.
8. The restorer replaces valid placeholders with the original local values.
9. The final response is shown to the user.

## Fail-closed behavior

The design should block transmission when:

- Detection raises an error.
- The privacy pipeline is unavailable.
- A protected prompt cannot be produced.
- The provider response contains unknown placeholders.
- Required placeholders are missing or malformed.

A privacy feature that silently disables itself during failure would create a false sense of protection.

## Local trust boundary

The following information remains local:

- Original user values.
- Placeholder mappings.
- Encryption keys.
- Restoration logic.
- Privacy policy configuration.

The external provider receives only the protected prompt and returns protected content.

## Planned MVP technologies

- Python.
- Streamlit for the first interface.
- Regular expressions for structured sensitive values.
- A provider-neutral model adapter.
- SQLite for local development storage.
- Encryption for reversible mappings before real data is considered.
- Automated tests for privacy invariants.

This repository documents the design only. It does not yet contain the executable MVP.
