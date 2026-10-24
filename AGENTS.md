# Project instructions

## Commit signatures

- The user requires all commits in this repository to be signed and to show **Verified** on GitHub.
- Keep `commit.gpgsign=true` enabled for this repository and use signed commits (`git commit -S`).
- Use the user's configured signing key and signing agent. Never bypass a signing failure with `--no-gpg-sign` or `commit.gpgsign=false`; restore the signing agent or explain the blocker.
- After pushing, check GitHub's commit verification result. A local signature alone is not sufficient; require `commit.verification.verified=true` before reporting a commit as Verified.
- If GitHub cannot be reached, report verification as pending and verify it when access is restored.
- Rewriting previously published commits requires user authorization. For the initial unsigned commit, the user explicitly authorized adding a signature on 2026-10-24. Use an explicit `--force-with-lease` expectation when updating that history.

## Repository presentation

- Keep the repository private unless the user explicitly requests otherwise.
- Use the language labels `English | 繁體中文 | 简体中文` in that order.
- Maintain the README and repository description in English, Traditional Chinese, and Simplified Chinese.
- The project license is `GPL-3.0-only`; third-party components retain their respective licenses.
