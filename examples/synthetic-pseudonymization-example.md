# Synthetic Pseudonymization Example

This example uses fictional information and demonstrates the intended transformation boundary.

## Original user request

```text
Draft a payment reminder for Laura Perez.
Her email is laura.perez@example.com and her reference number is 12345678.
```

## Detected entities

| Entity type | Original value | Placeholder |
| --- | --- | --- |
| Person | Laura Perez | `[[PERSON_A7F2]]` |
| Email | laura.perez@example.com | `[[EMAIL_C29D]]` |
| Reference | 12345678 | `[[REFERENCE_81C4]]` |

## Protected prompt sent to the model

```text
Draft a payment reminder for [[PERSON_A7F2]].
Their email is [[EMAIL_C29D]] and their reference number is [[REFERENCE_81C4]].
```

## Example protected response

```text
Subject: Payment reminder

Dear [[PERSON_A7F2]],

This is a reminder regarding reference [[REFERENCE_81C4]].
Please contact us through [[EMAIL_C29D]] if you need assistance.
```

## Validation

Before restoration, the local application should confirm that:

- All three placeholders are known.
- No unknown placeholder appears.
- Placeholder syntax remains exact.
- The provider response does not contain the original values.

## Locally restored response

```text
Subject: Payment reminder

Dear Laura Perez,

This is a reminder regarding reference 12345678.
Please contact us through laura.perez@example.com if you need assistance.
```

## Mapping boundary

The following mapping remains local and is never sent to the model provider:

```json
{
  "[[PERSON_A7F2]]": "Laura Perez",
  "[[EMAIL_C29D]]": "laura.perez@example.com",
  "[[REFERENCE_81C4]]": "12345678"
}
```

A future implementation should encrypt this mapping, scope it to the conversation and delete it according to a retention policy.
