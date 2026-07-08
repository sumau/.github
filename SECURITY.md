# DBT GitHub Security Policy

## Summary

This policy explains:
- how members of the public can responsibly [report vulnerabilities](#reporting-a-vulnerability) to the Department for Business and Trade (DBT)
- how DBT developers can follow [secure development practices](#secure-development-practices)
- how DBT developers can apply DBT's required [security controls](#security-controls) in GitHub

---

## Reporting a Vulnerability

This section is for members of the public and external security researchers. DBT staff should instead report vulnerabilities directly to the Cyber Security team.

If you believe you have found a security vulnerability, please submit a report via our [HackerOne form](https://hackerone.com/2680e4cd-0436-42a5-bd2a-37fd86367276/embedded_submissions/new).

Please include:
- Where the issue can be observed (URL, IP address or page)
- A brief description (e.g. “XSS vulnerability”)
- Safe, non-destructive reproduction steps

**Scope**
- In scope: digital services operated by DBT, including repositories in the [`uktrade` GitHub organisation](https://github.com/uktrade)
- Out of scope: denial of service, social engineering, physical attacks, and reports from automated scanners without a working proof of concept

**Disclosure guidelines**
- Do **not** share vulnerability details beyond DBT and the asset owner
- HackerOne accounts are optional, but allow you to receive updates on your report
- You must agree to HackerOne’s Terms, Privacy Policy, and Disclosure Guidelines
- NCC Group, DBT’s external triage partner, triages reports within **five working days**
- DBT’s Cyber Security team assists with coordination, but the asset owner is responsible for remediation

**Safe harbour**

DBT will not seek prosecution of researchers who act in good faith: stay within the scope above, avoid destructive testing, and do not access, modify or retain other users’ data.

---

## Secure Development Practices

These requirements apply to all DBT developers.

### Handling Secrets and Sensitive Data

Leaked secrets (API keys, tokens, passwords) are among the most common causes of security breaches, and personal or otherwise sensitive data must be kept out of GitHub just as carefully. Sensitive data includes operational details — such as internal hostnames, IP ranges and security thresholds — that would make DBT systems easier to attack. Developers must:

- Never commit secrets or sensitive data to GitHub
- Use secure storage for managing secrets
- Ensure no secrets or sensitive data appear in pull requests (PRs), logs or config files

The [GitHub Security Standards](https://dbis.sharepoint.com/:w:/r/sites/DDaTDirectorate/Shared%20Documents/Work%20-%20GitHub%20Security/Github%20Security%20Framework/Guidelines%20and%20Policies/GitHub%20Security%20Standards%20v0.6.docx?d=w022dea8105074e36af5450797083c297&csf=1&web=1&e=SR5out) (DBT staff access only) explain what counts as a secret and how to manage secrets securely.

If a secret or sensitive data is pushed to GitHub follow the [GitHub Repository Incident Playbook](https://dbis.sharepoint.com/:w:/r/sites/DDaTDirectorate/Shared%20Documents/Work%20-%20GitHub%20Security/Github%20Security%20Framework/Incident%20Response/GitHub%20Repository%20Incident%20Playbook.docx?d=w9ba04ffa4a7c4ff38faaaf12ff030c94&csf=1&web=1&e=yZF5dO) (DBT staff access only)

### Handling Vulnerabilities

Vulnerabilities can enter through your own code or through the dependencies it relies on. Several GitHub scans guard against them:

- [CodeQL](https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning-with-codeql) analyses your own code, both on pull requests and on a scheduled basis
- [Dependabot](https://docs.github.com/en/code-security/dependabot/dependabot-alerts/about-dependabot-alerts) flags vulnerable dependencies already in your project, and [Dependabot security updates](https://docs.github.com/en/code-security/dependabot/dependabot-security-updates/about-dependabot-security-updates) raise PRs to fix them automatically
- [Dependency review](https://docs.github.com/en/code-security/supply-chain-security/understanding-your-software-supply-chain/about-dependency-review) flags vulnerable dependencies a pull request would add before it is merged

We are also investigating IDE scanning and non-GitHub native code security scanning solutions.

Any alerts these scans raise must be triaged, not ignored:

- Fix the vulnerability, or dismiss the alert with a documented reason (e.g. false positive, not exploitable in this context)
- A PR blocked by a failing security check should be fixed, not bypassed
- Administrators who do bypass a check must record the justification on the PR and raise an issue to resolve the vulnerability

Alerts must be resolved — fixed or dismissed with a reason — within the following timescales, measured from when the alert is first raised and based on the severity GitHub assigns:

| Severity | Resolve within |
|---|---|
| Critical | 7 days |
| High | 30 days |
| Medium | 90 days |
| Low | 180 days |

Do not discuss unfixed vulnerability details anywhere public — vulnerability alerts are visible only to users with write access, but comments on PRs and issues in public repositories are visible to everyone.

---

## Security Controls

DBT uses several processes to strengthen the security posture of our GitHub repositories. The diagram below shows where some of these controls apply as code moves from your workspace to GitHub, following the secure development lifecycle principle of “shifting left” — catching issues at the earliest possible point.

![Code security workflow](/assets/code_sec_workflow.excalidraw.svg)

### Security Checklist

The security checklist turns those controls into concrete steps to confirm for your own repository. Copy [`SECURITY_CHECKLIST.md`](https://github.com/uktrade/.github/blob/main/templates/SECURITY_CHECKLIST.md) into your repository root and work through it from top to bottom, ticking each item once you have confirmed it and noting the date you checked. Its items follow the same order as the detailed guidance below, and each says who can action it. The result is a visible record of your repository's security posture for your team, reviewers and auditors.

---

### Contributor Controls

Actions each contributor takes for themselves.

#### Security Training

All internal contributors must complete at least **one** of the following free courses. Each provides a good overall grounding in code security and none is tied to specific tooling — pick whichever best suits your experience level and available time:

| Course | Time | Notes |
|---|---|---|
| [Snyk Learn: OWASP Top 10](https://learn.snyk.io/learning-paths/owasp-top-10/) | ~2.5 hrs | 10 lessons covering the 2025 OWASP Top 10 categories. Free account required; completion certificate available. Examples available in multiple languages |
| [Kontra: OWASP Top 10 for Web](https://application.security/free/owasp-top-10) | ~2.5 hrs | 28 short interactive exercises based on real-world vulnerabilities. Browser-based, nothing to install. Requires signup with a work email |
| [Snyk Learn: Security for Developers](https://learn.snyk.io/learning-paths/security-for-developers/) | ~4 hrs | 16 lessons going deeper into specific attack techniques (injection variants, SSRF, prototype pollution etc.). Free account required; completion certificate available |

For those who want to go further, the [PortSwigger Web Security Academy](https://portswigger.net/web-security) offers free, in-depth hands-on labs across the full range of web vulnerabilities, and the [Snyk Learn hardcoded secrets lesson](https://learn.snyk.io/lesson/hardcoded-secrets/) (~20 mins) is a recommended supplement that reinforces the [Handling Secrets and Sensitive Data](#handling-secrets-and-sensitive-data) requirements above.

#### GitHub Safety Tips

Internal contributors should review the [GitHub Safety Tips](https://uktrade.atlassian.net/wiki/x/n4AEKQE) (DBT staff access only) to understand how to protect themselves when coding in the open.

---

### Organisation-Applied Controls

An organisation administrator applies these centrally, and they cannot be weakened at repository level. The security configuration and custom properties are the mechanism; branch protection and push protection are the enforced results — verify they are active rather than configuring them yourself.

#### GitHub Security Configuration

DBT has introduced an organisation-wide GitHub [security configuration](https://docs.github.com/en/code-security/how-tos/secure-at-scale/configure-organization-security/establish-complete-coverage/apply-custom-configuration) that applies the required security checks to every repository. New repositories get this configuration by default, but existing ones must have it enabled before they can be made public. Over time, it will fully replace the old configuration across the `uktrade` organisation.

An organisation administrator must apply it — follow the [step-by-step instructions](https://github.com/uktrade/.github/blob/main/docs/github-security-configuration.md).

#### Custom GitHub Properties

DBT uses [custom GitHub properties](https://docs.github.com/en/organizations/managing-organization-settings/managing-custom-properties-for-repositories-in-your-organization) to enforce branch protection rules and run organisation-level GitHub Actions workflows. They describe what kind of repository this is, so the organisation's automation can apply the checks relevant to it — if they are missing or wrong, your repository may not get the right protections.

View or set custom properties under **Settings → Custom properties**:
`https://github.com/uktrade/REPO_NAME/settings/custom-properties`

**Mandatory**
- `reusable_workflow_opt_in` — set to `true`
- `scs_portfolio` — the portfolio associated with your Senior Civil Servant (SCS). If your portfolio is missing, this can be added by raising a ticket with the SRE team

**Optional**
- `is_docker` — for repositories that build Docker images
- `language` — select all languages used by the repository, so the organisation-level workflows run language-specific checks

#### Branch Protection Rules

Branch protection stops unreviewed code reaching the default branch — the version of the code that gets deployed and that others build on. An organisation [ruleset](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets) has been created to apply a minimum set of branch protection rules:

- A PR is required for merges into the default branch (usually `main`)
- At least 1 approver is required before a PR can be merged
- Any conversations on the PR must be marked as resolved

Organisation administrators and repository administrators have been added to the bypass list for this branch protection ruleset.

Repository administrators may add additional rules to their own repositories, but cannot weaken the organisation ruleset: where rules overlap, the most restrictive rule applies. For example, a repository ruleset that drops the required number of approvers to 0 would have no effect, while one that raises it to 3 would apply.

#### GitHub Secret Protection

The DBT GitHub security configuration enables two complementary features. [Push protection](https://docs.github.com/en/code-security/concepts/secret-security/push-protection) blocks pushes containing high-confidence secret formats, stopping them before they reach the repository's history. [Secret scanning](https://docs.github.com/en/code-security/secret-scanning/introduction/about-secret-scanning) covers a broader range, detecings secrets already committed and raising alerts in the **Security** tab. Both can apply [custom patterns](https://docs.github.com/en/code-security/how-tos/secure-your-secrets/customize-leak-detection/define-custom-patterns) for DBT-specific secrets.

Confirm both features are enabled on your repository. Never bypass a push-protection block — remove the secret from your commit instead. If you need additional custom patterns, raise a ticket with the SRE team.

#### Vulnerability Scanning

The DBT GitHub security configuration also enables the features described under [Handling Vulnerabilities](#handling-vulnerabilities) — CodeQL, Dependabot, Dependabot security updates and dependency review. Confirm these are active on your repository.

---

### Repository-Level Controls

Defences set up within the repository itself.

#### Pre-Commit Hooks

Repositories must include a `.pre-commit-config.yaml` that runs the organisation-approved [pre-commit](https://pre-commit.com/) hooks, and each contributor must install them locally. The hooks use [Trufflehog](https://github.com/trufflesecurity/trufflehog) to detect secrets and [Presidio](https://microsoft.github.io/presidio/) to detect sensitive data. They run on your machine before a commit is even created — the earliest and cheapest point to stop a leak, since anything that reaches GitHub must be treated as compromised.

As a backstop, a GitHub Actions workflow (applied via the repository's custom properties) re-runs the same scans and blocks any PR where the hooks were skipped locally. Repository administrators can still merge past a failing check.

For more information and setup guidance, see the [uktrade/github-standards](https://github.com/uktrade/github-standards) repository.

#### CODEOWNERS

Repositories must include a [`CODEOWNERS`](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) file. GitHub automatically requests a review from the listed owners when a PR touches their code, ensuring changes are seen by people who understand their security implications.

#### Pull Request Template

A [pull request template](https://docs.github.com/en/communities/using-templates-to-encourage-useful-issues-and-pull-requests/creating-a-pull-request-template-for-your-repository) pre-fills the PR description with a standard checklist. PR review is the last human check before code is published, so the [DBT template](https://github.com/uktrade/.github/blob/main/.github/pull_request_template.md) prompts reviewers to look for secrets explicitly rather than relying on automated scanning alone.

If your repository does not already contain a `pull_request_template.md` file, you will inherit the DBT template as a [community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file). If you are already using your own template, copy its Reviewer Checklist section across so reviewers are still reminded to check for exposed secrets:

```
## Reviewer Checklist

- [ ] I have reviewed the PR and ensured no secret values are present
```

#### CodeQL for Fork-Based PRs (Optional)

The DBT GitHub security configuration does not currently support scanning PRs raised from a fork of a repository. Fork PRs typically come from contributors outside the organisation, so leaving them unscanned would create a gap in coverage.

If PRs from forks must be supported, switch to [**Advanced** CodeQL](https://docs.github.com/en/code-security/how-tos/find-and-fix-code-vulnerabilities/configure-code-scanning/configuring-advanced-setup-for-code-scanning) — follow the [step-by-step instructions](https://github.com/uktrade/.github/blob/main/docs/codeql-advanced-setup.md).

## About This Policy

This policy is defined in DBT's [`.github` repository](https://github.com/uktrade/.github) as a [community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file), so every `uktrade` repository without its own `SECURITY.md` inherits it automatically. Do not add a `SECURITY.md` to your own repository — to suggest changes, raise a PR against the [`.github` repository](https://github.com/uktrade/.github) instead.
