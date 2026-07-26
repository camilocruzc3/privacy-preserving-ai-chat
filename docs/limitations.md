# Limitations

This repository documents a concept and proposed MVP. It does not currently contain an executable privacy gateway.

## Detection limitations

- Rule-based detection will miss some names, addresses and contextual identifiers.
- Entity recognition may produce false positives and false negatives.
- No detector can be assumed to identify every sensitive value.
- Multilingual and domain-specific content may require additional models and rules.

## Pseudonymization limitations

- Pseudonymization is reversible and therefore not equivalent to anonymization.
- Protected text may still reveal sensitive context through surrounding details.
- A compromised mapping store can expose the original values.
- Placeholder consistency may allow some relationships to be inferred.

## Model limitations

- External models may alter, omit or invent placeholders.
- Model behavior remains probabilistic.
- Prompt injection cannot be solved only through system instructions.
- Provider policies and retention practices remain relevant even when values are pseudonymized.

## Implementation limitations

- Authentication and authorization are not yet designed in detail.
- Encryption and key management are not implemented.
- Retention and deletion workflows are not implemented.
- There is no production audit trail, monitoring or incident response process.
- The concept has not undergone an independent security review.

## Usage boundary

Do not use the current repository as evidence that real sensitive data can be processed safely. The design must first become an implementation, then be tested with synthetic data, reviewed and hardened before any real-world use is considered.
