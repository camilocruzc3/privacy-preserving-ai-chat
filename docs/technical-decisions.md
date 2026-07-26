# Technical Decisions

## Start with a local monolith

The first MVP should remain a single Python application. This keeps the privacy flow understandable, reduces deployment complexity and makes it easier to test that every outbound model request passes through the same protection layer.

## Use pseudonymization, not claim anonymization

The system preserves a reversible mapping so original values can be restored. Therefore, the correct term is pseudonymization or tokenization, not irreversible anonymization.

## Begin with text only

Text allows the core privacy boundary to be tested without introducing OCR, face detection, voice processing, media metadata or document parsing.

## Prefer deterministic rules for structured values

Regular expressions are suitable for an initial set of structured entities such as email addresses and phone numbers. They are not sufficient for every person name, address or contextual identifier, and that limitation must remain explicit.

## Use a provider-neutral model adapter

Application code should not call an external model SDK from multiple modules. A single adapter creates a clear test boundary and makes it possible to replace the provider later.

## Generate unpredictable placeholders

Conversation-scoped random identifiers are preferred over global sequential placeholders. This reduces collisions and makes accidental or fabricated token reuse less likely.

## Restore by exact match only

Approximate token recovery can produce incorrect substitutions. The first implementation should restore only exact, validated placeholders.

## Fail closed

When the detector, pseudonymizer, validator or mapping store fails, the system should not silently send the original message.

## Separate logs from content

Operational logs should record event types, timestamps, status and correlation identifiers. Raw prompts, original values, mappings and complete restored responses should not be logged by default.

## Delay distributed architecture

Microservices, API gateways, queues and enterprise identity controls may be useful later, but they are not required to prove the central privacy pattern in the first MVP.
