## Overview

| Developed by | Guardrails AI |
| Date of development | Feb 15, 2024 |
| Validator type | Format |
| Blog |  |
| License | Apache 2 |
| Input/Output | Output |

## Description

### Intended Use
This validator checks that any URL generated by an LLM is valid

### Requirements

* Dependencies:
    - guardrails-ai>=0.4.0

## Installation

```bash
guardrails hub install hub://guardrails/valid_url
```

## Usage Examples

### Validating string output via Python

In this example, we use the `guardrails/valid_url` validator on any LLM generated URL.

```python
# Import Guard and Validator
from guardrails import Guard
from guardrails.hub import ValidURL

# Setup Guard
guard = Guard().use(ValidURL, on_fail="exception")
response = guard.validate("http://www.google.com")  # Validator passes

try:
    response = guard.validate("notalink.xyzq")  # Validator fails
except Exception as e:
    print(e)
```
Output:
```console
Validation failed for field with errors: URL notalink.xyzq is not valid.
```

# API Reference

**`__init__(self, on_fail="noop")`**
<ul>

Initializes a new instance of the Validator class.

**Parameters:**

- **`on_fail`** *(str, Callable):* The policy to enact when a validator fails. If `str`, must be one of `reask`, `fix`, `filter`, `refrain`, `noop`, `exception` or `fix_reask`. Otherwise, must be a function that is called when the validator fails.

</ul>

<br>

**`__call__(self, value, metadata={}) → ValidationResult`**

<ul>

Validates the given `value` using the rules defined in this validator, relying on the `metadata` provided to customize the validation process. This method is automatically invoked by `guard.parse(...)`, ensuring the validation logic is applied to the input data.

Note:

1. This method should not be called directly by the user. Instead, invoke `guard.parse(...)` where this method will be called internally for each associated Validator.
2. When invoking `guard.parse(...)`, ensure to pass the appropriate `metadata` dictionary that includes keys and values required by this validator. If `guard` is associated with multiple validators, combine all necessary metadata into a single dictionary.

**Parameters:**

- **`value`** *(Any):* The input value to validate.
- **`metadata`** *(dict):* A dictionary containing metadata required for validation. No additional metadata keys are needed for this validator.

</ul>
