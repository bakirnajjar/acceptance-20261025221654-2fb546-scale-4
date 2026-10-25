# Password recovery requirements map (internal working artifact)

## Evidence and coverage

The complete pinned story is “As a customer I want to reset my password. Apply the curated recovery standard.” It has no end marker. There are no attachments or approved prior-stage outputs. The two curated results contain identical excerpts of ACC-STD-01 through ACC-STD-03. All eight identifiers below are independently observable: one story capability and seven standard controls. Evidence objects retain the exact source type, ID, and locator for later contract transcription.

### REQ-001 — Reset the password

**Draft statement:** A customer can complete a password reset, replacing the password used to access the account.

**Draft check:** Given a customer is completing a valid password reset, when the customer sets a new password and completes the reset, then the new password can be used to sign in and the former password cannot.

**Evidence:** `{ "source_type": "user_story", "source_id": "user_story", "locator": "characters 0-16000" }`

### REQ-002 — Start a reset from sign-in

**Draft statement:** The sign-in page offers a “Forgot password?” link that starts a password reset request.

**Draft check:** Given the sign-in page is displayed, when a customer selects “Forgot password?”, then the password reset request process starts.

**Evidence:** `{ "source_type": "knowledge", "source_id": "59efeb19-83f2-4ec6-bfd3-b4aeb7142930", "locator": "v1, chunk 0" }`; `{ "source_type": "knowledge", "source_id": "467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3", "locator": "v1, chunk 0" }` (ACC-STD-01).

### REQ-003 — Do not disclose account existence in the request response

**Draft statement:** The response to a password reset request is identical whether the account exists or not.

**Draft check:** Given an existing account and a nonexistent account, when an otherwise equivalent reset request is made for each, then the request responses are identical.

**Evidence:** `{ "source_type": "knowledge", "source_id": "59efeb19-83f2-4ec6-bfd3-b4aeb7142930", "locator": "v1, chunk 0" }`; `{ "source_type": "knowledge", "source_id": "467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3", "locator": "v1, chunk 0" }` (ACC-STD-01).

### REQ-004 — Limit reset requests

**Draft statement:** Reset requests are limited to five per account per hour.

**Draft check:** Given five reset requests have already been made for an account within an hour, when a sixth request is made for that account within the same hour, then it does not issue an additional reset link.

**Evidence:** `{ "source_type": "knowledge", "source_id": "59efeb19-83f2-4ec6-bfd3-b4aeb7142930", "locator": "v1, chunk 0" }`; `{ "source_type": "knowledge", "source_id": "467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3", "locator": "v1, chunk 0" }` (ACC-STD-01).

### REQ-005 — Use a reset link only once

**Draft statement:** A reset link is single-use.

**Draft check:** Given an unused, unexpired reset link, when it is used to complete a successful reset, then a subsequent attempt to reset a password with that same link cannot succeed.

**Evidence:** `{ "source_type": "knowledge", "source_id": "59efeb19-83f2-4ec6-bfd3-b4aeb7142930", "locator": "v1, chunk 0" }`; `{ "source_type": "knowledge", "source_id": "467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3", "locator": "v1, chunk 0" }` (ACC-STD-02).

### REQ-006 — Expire reset links

**Draft statement:** A reset link expires 30 minutes after it is issued.

**Draft check:** Given an unused reset link and its issue time, when a reset is attempted with that link at or after 30 minutes from issue, then the link cannot complete the reset.

**Evidence:** `{ "source_type": "knowledge", "source_id": "59efeb19-83f2-4ec6-bfd3-b4aeb7142930", "locator": "v1, chunk 0" }`; `{ "source_type": "knowledge", "source_id": "467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3", "locator": "v1, chunk 0" }` (ACC-STD-02).

### REQ-007 — Sign out active sessions after reset

**Draft statement:** Completing a password reset signs the account out of every active session.

**Draft check:** Given an account has multiple active sessions, when its password reset completes, then none of those sessions remains signed in.

**Evidence:** `{ "source_type": "knowledge", "source_id": "59efeb19-83f2-4ec6-bfd3-b4aeb7142930", "locator": "v1, chunk 0" }`; `{ "source_type": "knowledge", "source_id": "467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3", "locator": "v1, chunk 0" }` (ACC-STD-02).

### REQ-008 — Notify the account owner

**Draft statement:** The account owner is notified after every successful password reset.

**Draft check:** Given an account owner and a successful password reset for that account, when the reset completes, then that owner is notified about that reset; each subsequent successful reset likewise results in an owner notification.

**Evidence:** `{ "source_type": "knowledge", "source_id": "59efeb19-83f2-4ec6-bfd3-b4aeb7142930", "locator": "v1, chunk 0" }`; `{ "source_type": "knowledge", "source_id": "467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3", "locator": "v1, chunk 0" }` (ACC-STD-03).

## Evidence gaps, assumptions, and non-blocking questions

- **Assumption:** acceptance-20261025221654-2fb546-skill-sentinel — the acceptance requirements skill produced this working output.
- **Evidence gap / non-blocking question:** How is a reset link delivered, and how is the customer identified for a reset request? **Assumption:** Leave delivery and identification unspecified; require only the link behavior established by the standard.
- **Evidence gap / non-blocking question:** How is the account owner notified? **Assumption:** Leave notification channel and content unspecified; require only notification after each successful reset.
- **Evidence gap / non-blocking question:** What happens to further requests after the five-per-account-per-hour limit, and how is the hour measured? **Assumption:** A sixth request within the same hour issues no additional reset link; do not specify storage, response wording, or a rolling versus fixed window. The identical-response requirement remains applicable.
- **Evidence gap:** Neither the story nor the standard specifies a token implementation, reset delivery mechanism, or numeric targets other than five requests per account per hour and 30-minute link expiry. No such implementation or additional targets are assumed.
