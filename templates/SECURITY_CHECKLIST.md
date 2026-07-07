# Security Checklist

Work through this checklist from top to bottom, ticking each item once you have confirmed it is true. Each item links to detailed guidance in the [DBT GitHub Security Policy](https://github.com/uktrade/.github/blob/main/SECURITY.md).

Last checked against the policy: _add date_

## 1. Contributor controls — every contributor

Actions each contributor takes for themselves, so everyone knows what the controls are and why they exist.

- [ ] [All internal contributors have completed security training](https://github.com/uktrade/.github/blob/main/SECURITY.md#security-training)
- [ ] [All internal contributors have reviewed the GitHub Safety Tips](https://github.com/uktrade/.github/blob/main/SECURITY.md#github-safety-tips)
- [ ] [All internal contributors have reviewed the code security workflow](https://github.com/uktrade/.github/blob/main/SECURITY.md#code-security-workflow)
- [ ] [All contributors run the organisation-approved pre-commit hooks](https://github.com/uktrade/.github/blob/main/SECURITY.md#pre-commit-hooks)

## 2. Organisation-applied controls — an organisation administrator applies, a repository administrator verifies

These enforce security checks centrally and cannot be weakened at repository level. Applying the first two should enable the second two automatically, but confirm rather than assume.

- [ ] [The DBT GitHub security configuration is applied to the repository](https://github.com/uktrade/.github/blob/main/SECURITY.md#github-security-configuration)
- [ ] [The mandatory custom GitHub properties are set](https://github.com/uktrade/.github/blob/main/SECURITY.md#custom-github-properties)
- [ ] [Branch protection rules apply to the default branch](https://github.com/uktrade/.github/blob/main/SECURITY.md#branch-protection-rules)
- [ ] [Push protection is enabled and blocking secrets](https://github.com/uktrade/.github/blob/main/SECURITY.md#push-protection)

## 3. Repository-level controls — repository administrators and contributors

Defences set up within the repository itself.

- [ ] [A `CODEOWNERS` file exists so the right people review changes](https://github.com/uktrade/.github/blob/main/SECURITY.md#codeowners)
- [ ] [The pull request template reminds reviewers to check for secrets](https://github.com/uktrade/.github/blob/main/SECURITY.md#pull-request-template)
- [ ] [Advanced CodeQL is set up if the repository accepts PRs from forks (optional)](https://github.com/uktrade/.github/blob/main/SECURITY.md#codeql-for-fork-based-prs-optional)
