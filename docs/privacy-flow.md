# Privacy Flow

## 1. Input classification

The application receives a text message and assigns it to a new request or conversation context. The raw message remains inside the trusted local environment.

## 2. Sensitive-data detection

The detector evaluates the text using configured rules. The first MVP should prioritize structured values that can be recognized deterministically, such as:

- Email addresses.
- Phone numbers.
- Identification numbers.
- Account or card-like references.
- IP addresses.

Names, addresses and contextual sensitive information require more advanced detection and should not be presented as fully solved by simple regular expressions.

## 3. Placeholder generation

Each detected value is replaced by an unpredictable, conversation-scoped placeholder.

Preferred format:

```text
[[ENTITY_RANDOM_ID]]
```

Example:

```text
[[PERSON_A7F2]]
[[DOCUMENT_81C4]]
```

Sequential placeholders such as `[PERSON_1]` are easier to predict and may collide across conversations, so random identifiers are preferred.

## 4. Local mapping

The application creates a mapping similar to:

```json
{
  "[[PERSON_A7F2]]": "Laura Perez",
  "[[DOCUMENT_81C4]]": "12345678"
}
```

This mapping must not be sent to the model provider. In a real implementation it should be encrypted, isolated by user and conversation, excluded from logs and deleted according to a retention policy.

## 5. External model call

The model adapter receives only the protected prompt. The adapter should expose a testable boundary so automated tests can prove that original sensitive values are absent from every outbound request.

## 6. Response validation

Before restoration, the application verifies that:

- Every placeholder in the response exists in the local mapping.
- Placeholder syntax has not been altered.
- No unknown placeholder was introduced.
- Required placeholders are not unexpectedly missing.
- The response does not contain original sensitive values that should have remained protected.

## 7. Local restoration

Only validated placeholders are replaced with their original values. Approximate matching should not be used because it can restore the wrong value or hide a malformed response.

## 8. Final delivery

The restored response is returned to the user. Logs should contain event metadata and status information, not raw prompts, original values or reversible mappings.

## Failure policy

```text
Successful detection and validation -> continue
Uncertain or incomplete detection -> warn or block
Privacy pipeline error -> block transmission
Unknown response placeholder -> block restoration and request review
```
