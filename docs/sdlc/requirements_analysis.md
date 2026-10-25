# Requirements analysis: customer password reset

**Stage:** `requirements_analysis` · **Schema version:** `1.0`

## Provenance

The complete story is: “As a customer I want to reset my password. Apply the curated recovery standard.” The following are the source references used by this analysis; the two knowledge results independently return the same ACC-STD-01 through ACC-STD-03 excerpt.

| Key | Source type | Source ID | Locator |
| --- | --- | --- | --- |
| Story | `user_story` | `user_story` | `characters 0-16000` |
| Standard A | `knowledge` | `59efeb19-83f2-4ec6-bfd3-b4aeb7142930` | `v1, chunk 0` |
| Standard B | `knowledge` | `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3` | `v1, chunk 0` |

No attachments or approved prior-stage outputs were supplied. There is no story end marker or attachment marker.

## Requirements and acceptance criteria

### REQ-001 — Reset the password

A customer can complete a password reset, replacing the password used to access the account.

- **Given** a customer is completing a valid password reset, **when** the customer sets a new password and completes the reset, **then** the new password can be used to sign in and the former password cannot.
- **Source references:** Story (`user_story`, `user_story`, `characters 0-16000`).

### REQ-002 — Start a reset from sign-in

The sign-in page offers a "Forgot password?" link that starts a password reset request.

- **Given** the sign-in page is displayed, **when** a customer selects "Forgot password?", **then** the password reset request process starts.
- **Source references:** Standard A (`knowledge`, `59efeb19-83f2-4ec6-bfd3-b4aeb7142930`, `v1, chunk 0`); Standard B (`knowledge`, `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3`, `v1, chunk 0`). ACC-STD-01.

### REQ-003 — Do not disclose account existence in the request response

The response to a password reset request is identical whether or not the account exists.

- **Given** an existing account and a nonexistent account, **when** an otherwise equivalent reset request is made for each, **then** the request responses are identical.
- **Source references:** Standard A (`knowledge`, `59efeb19-83f2-4ec6-bfd3-b4aeb7142930`, `v1, chunk 0`); Standard B (`knowledge`, `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3`, `v1, chunk 0`). ACC-STD-01.

### REQ-004 — Limit reset requests

Reset requests are limited to five per account per hour.

- **Given** five reset requests have already been made for an account within an hour, **when** a sixth request is made for that account within the same hour, **then** it does not issue an additional reset link.
- **Source references:** Standard A (`knowledge`, `59efeb19-83f2-4ec6-bfd3-b4aeb7142930`, `v1, chunk 0`); Standard B (`knowledge`, `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3`, `v1, chunk 0`). ACC-STD-01.

### REQ-005 — Use a reset link only once

A reset link is single-use.

- **Given** an unused, unexpired reset link, **when** it is used to complete a successful reset, **then** a subsequent attempt to reset a password with that same link cannot succeed.
- **Source references:** Standard A (`knowledge`, `59efeb19-83f2-4ec6-bfd3-b4aeb7142930`, `v1, chunk 0`); Standard B (`knowledge`, `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3`, `v1, chunk 0`). ACC-STD-02.

### REQ-006 — Expire reset links

A reset link expires 30 minutes after it is issued.

- **Given** an unused reset link and its issue time, **when** a reset is attempted with that link at or after 30 minutes from issue, **then** the link cannot complete the reset.
- **Source references:** Standard A (`knowledge`, `59efeb19-83f2-4ec6-bfd3-b4aeb7142930`, `v1, chunk 0`); Standard B (`knowledge`, `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3`, `v1, chunk 0`). ACC-STD-02.

### REQ-007 — Sign out active sessions after reset

Completing a password reset signs the account out of every active session.

- **Given** an account has multiple active sessions, **when** its password reset completes, **then** none of those sessions remains signed in.
- **Source references:** Standard A (`knowledge`, `59efeb19-83f2-4ec6-bfd3-b4aeb7142930`, `v1, chunk 0`); Standard B (`knowledge`, `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3`, `v1, chunk 0`). ACC-STD-02.

### REQ-008 — Notify the account owner

The account owner is notified after every successful password reset.

- **Given** an account owner and a successful password reset for that account, **when** the reset completes, **then** that owner is notified about that reset; each subsequent successful reset likewise results in an owner notification.
- **Source references:** Standard A (`knowledge`, `59efeb19-83f2-4ec6-bfd3-b4aeb7142930`, `v1, chunk 0`); Standard B (`knowledge`, `467a71ce-c5f8-4557-8f1e-a8ff1b01ecc3`, `v1, chunk 0`). ACC-STD-03.

## Assumptions

- acceptance-20261025221654-2fb546-skill-sentinel — the acceptance requirements skill produced this output.
- For the non-blocking question about reset-link delivery and customer identification, leave both mechanisms unspecified; require only the link behavior established by the curated standard.
- For the non-blocking question about owner notification, leave the notification channel and content unspecified; require only notification after every successful reset.
- For the non-blocking question about the request limit, assume a sixth request for the same account within the hour issues no additional reset link. Leave hour-window interpretation, storage, and response wording unspecified; the identical-response requirement still applies.

## Open questions (all non-blocking)

1. How is the reset link delivered, and how is the customer identified for a reset request? **Working assumption:** Leave delivery and identification mechanisms unspecified.
2. How is the account owner notified after a successful reset? **Working assumption:** Leave notification channel and content unspecified.
3. How are further requests handled after five requests per account per hour, and how is the hour measured? **Working assumption:** A sixth request within the hour issues no additional reset link; do not specify storage, response wording, or a fixed versus rolling window. The identical-response requirement still applies.
