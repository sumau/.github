# DBT GitHub Security Policy

## Summary
This policy explains how the public can responsibly [report vulnerabilities](#reporting-a-vulnerability) to the Department for Business and Trade (DBT), and how DBT developers must protect [sensitive information](#handling-secrets), [handle vulnerabilities](#handling-vulnerabilities) and follow DBT’s required [security controls](#security-controls) when working in GitHub.

It is defined in DBT's [`.github` repository](https://github.com/uktrade/.github) as a [community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file), so every `uktrade` repository without its own `SECURITY.md` inherits it automatically. Do not add a `SECURITY.md` to your own repository — to suggest changes, raise a PR against the [`.github` repository](https://github.com/uktrade/.github) instead.

---

## Reporting a Vulnerability

This section is for members of the public and external security researchers. DBT staff should instead report vulnerabilities directly to the Cyber Security team.

If you believe you have found a security vulnerability, please submit a report via our [HackerOne form](https://hackerone.com/2680e4cd-0436-42a5-bd2a-37fd86367276/embedded_submissions/new).

Please include:
- Where the issue can be observed (URL, IP address or page)
- A brief description (e.g. “XSS vulnerability”)
- Safe, non-destructive reproduction steps

**Disclosure guidelines**
- Do **not** share vulnerability details beyond DBT and the asset owner
- HackerOne accounts are optional, but allow you to receive updates on your report
- You must agree to HackerOne’s Terms, Privacy Policy, and Disclosure Guidelines
- NCC Group, DBT’s external triage partner, triages reports within **five working days**
- DBT’s Cyber Security team assists with coordination, but the asset owner is responsible for remediation

---

## Handling Secrets

These requirements apply to DBT developers. Leaked secrets (API keys, tokens, passwords) are one of the most common causes of security breaches, and because a secret committed to Git remains in the history even after deletion, it must be treated as compromised and rotated. Two internal documents cover this topic in detail:

- The [GitHub Security Standards](https://dbis.sharepoint.com/:w:/r/sites/DDaTDirectorate/Shared%20Documents/Work%20-%20GitHub%20Security/Github%20Security%20Framework/Guidelines%20and%20Policies/GitHub%20Security%20Standards%20v0.6.docx?d=w022dea8105074e36af5450797083c297&csf=1&web=1&e=SR5out) (DBT staff access only) explain what counts as a secret and how to manage secrets securely
- The [GitHub Repository Incident Playbook](https://dbis.sharepoint.com/:w:/r/sites/DDaTDirectorate/Shared%20Documents/Work%20-%20GitHub%20Security/Github%20Security%20Framework/Incident%20Response/GitHub%20Repository%20Incident%20Playbook.docx?d=w9ba04ffa4a7c4ff38faaaf12ff030c94&csf=1&web=1&e=yZF5dO) (DBT staff access only) explains what to do in the event of a leak

**In summary, developers must:**
- Never commit secrets or sensitive data to GitHub
- Use secure storage for managing secrets
- Ensure no secrets appear in pull requests (PRs), logs or config files
- Follow incident-response steps immediately if a leak occurs

---

## Handling Vulnerabilities

These requirements apply to DBT developers. CodeQL and Dependabot alerts appear in your repository's **Security** tab and must be triaged, not ignored:

- Fix the vulnerability, or dismiss the alert with a documented reason (e.g. false positive, not exploitable in this context)
- A PR blocked by a failing security check should be fixed, not bypassed
- Administrators who do bypass a check must record the justification on the PR and raise an issue to resolve the vulnerability

Do not discuss unfixed vulnerability details anywhere public — alerts are only visible to users with write access, but PR comments and issues on public repositories are not.

---

## Security Controls

DBT uses several processes to strengthen the security posture of our GitHub repositories.

Copy the checklist below into a `SECURITY_CHECKLIST.md` file in the root of your repository, then work through it from top to bottom, ticking each item once you have confirmed it is true and recording the date you last checked it against this policy. This gives your team, reviewers and auditors a visible record of the repository's security posture. Each item links to detailed guidance below, in the same order.

**1. Understand the controls** — everyone contributing to the repository knows what the controls are and why they exist

- [ ] [All internal contributors have completed security training](https://github.com/uktrade/.github/blob/main/SECURITY.md#security-training)
- [ ] [All internal contributors have reviewed the GitHub Safety Tips](https://github.com/uktrade/.github/blob/main/SECURITY.md#github-safety-tips)
- [ ] [All internal contributors have reviewed the code security workflow](https://github.com/uktrade/.github/blob/main/SECURITY.md#code-security-workflow)

**2. Apply organisation-level protections** — these enforce security checks centrally and cannot be weakened at repository level (requires an organisation administrator)

- [ ] [The DBT GitHub security configuration is applied to the repository](https://github.com/uktrade/.github/blob/main/SECURITY.md#github-security-configuration)
- [ ] [The mandatory custom GitHub properties are set](https://github.com/uktrade/.github/blob/main/SECURITY.md#custom-github-properties)

**3. Verify the enforced controls are active** — applying the security configuration should enable these automatically, but confirm rather than assume

- [ ] [Branch protection rules apply to the default branch](https://github.com/uktrade/.github/blob/main/SECURITY.md#branch-protection-rules)
- [ ] [Push protection is enabled and blocking secrets](https://github.com/uktrade/.github/blob/main/SECURITY.md#push-protection)

**4. Configure repository-level controls** — defences that must be set up within the repository itself

- [ ] [All contributors run the organisation-approved pre-commit hooks](https://github.com/uktrade/.github/blob/main/SECURITY.md#pre-commit-hooks)
- [ ] [A `CODEOWNERS` file exists so the right people review changes](https://github.com/uktrade/.github/blob/main/SECURITY.md#codeowners)
- [ ] [The pull request template reminds reviewers to check for secrets](https://github.com/uktrade/.github/blob/main/SECURITY.md#pull-request-template)
- [ ] [Advanced CodeQL is set up if the repository accepts PRs from forks (optional)](https://github.com/uktrade/.github/blob/main/SECURITY.md#codeql-for-fork-based-prs-optional)

---

### Security Training

All internal contributors must complete at least **one** of the following free courses. Each provides a good overall grounding in code security and none is tied to specific tooling — pick whichever best suits your experience level and available time:

| Course | Time | Notes |
|---|---|---|
| [Snyk Learn: OWASP Top 10](https://learn.snyk.io/learning-paths/owasp-top-10/) | ~2.5 hrs | 10 lessons covering the 2025 OWASP Top 10 categories. Free account required; completion certificate available. Examples available in multiple languages |
| [Kontra: OWASP Top 10 for Web](https://application.security/free/owasp-top-10) | ~2.5 hrs | 28 short interactive exercises based on real-world vulnerabilities. Browser-based, nothing to install. Requires signup with a work email |
| [Snyk Learn: Security for Developers](https://learn.snyk.io/learning-paths/security-for-developers/) | ~4 hrs | 16 lessons going deeper into specific attack techniques (injection variants, SSRF, prototype pollution etc.). Free account required; completion certificate available |

For those who want to go further, the [PortSwigger Web Security Academy](https://portswigger.net/web-security) offers free, in-depth hands-on labs across the full range of web vulnerabilities, and the [Snyk Learn hardcoded secrets lesson](https://learn.snyk.io/lesson/hardcoded-secrets/) (~20 mins) is a recommended supplement that reinforces the [Handling Secrets](#handling-secrets) requirements above.

---

### GitHub Safety Tips

Internal contributors should review the [GitHub Safety Tips](https://uktrade.atlassian.net/wiki/x/n4AEKQE) (DBT staff access only) to understand how to protect themselves when coding in the open.

---

### Code Security Workflow

The diagram below shows where each control applies as code moves from your workspace to GitHub, following the secure development lifecycle principle of “shifting left” — catching issues at the earliest possible point.

![Code security workflow](/assets/code_sec_workflow_v2.excalidraw.svg)

---

### GitHub Security Configuration

DBT has introduced an organisation-wide GitHub [security configuration](https://docs.github.com/en/code-security/how-tos/secure-at-scale/configure-organization-security/establish-complete-coverage/apply-custom-configuration), **Default DBT security**, that applies the required security checks to every repository. New repositories get this configuration by default, but existing ones must have it enabled before they can be made public. Over time, it will fully replace the old configuration across the `uktrade` organisation.

**You must be an organisation administrator to apply this configuration**

To apply it, follow these instructions:

1. As an organisation administrator, navigate to the [security configurations page](https://github.com/organizations/uktrade/settings/security_products)
1. Scroll down to the **Apply configurations** section, and enter the name of the repository to be made public in the filter input field
1. Use the checkbox next to the results list to select all repositories being made public, then use the **Apply configuration** button to select the **Default DBT security** configuration
1. A confirmation modal will appear displaying a summary of the action being made. Click the **Apply** button
1. To confirm the configuration has been applied, navigate to **Settings → Advanced Security** in the repository. At the top of the page there should be a banner message **Modifications to some settings have been blocked by organization administrators**

---

### Custom GitHub Properties

DBT uses [custom GitHub properties](https://docs.github.com/en/organizations/managing-organization-settings/managing-custom-properties-for-repositories-in-your-organization) to enforce branch protection rules and run organisation-level GitHub Actions workflows. They describe what kind of repository this is, so the organisation's automation can apply the checks relevant to it — if they are missing or wrong, your repository may not get the right protections.

View or set custom properties under **Settings → Custom properties**:
`https://github.com/uktrade/REPO_NAME/settings/custom-properties`

**Mandatory**
- `reusable_workflow_opt_in` — set to `true`
- `scs_portfolio` — the portfolio associated with your CSC. If your portfolio is missing, this can be added by raising a ticket with the Site Reliability Engineering (SRE) team

**Optional**
- `is_docker` — for repositories that build Docker images
- `language` — select all languages used by the repository, so the organisation-level workflows run language-specific checks

---

### Branch Protection Rules

Branch protection stops unreviewed code reaching the default branch — the version of the code that gets deployed and that others build on. An organisation [ruleset](https://docs.github.com/en/repositories/configuring-branches-and-merges-in-your-repository/managing-rulesets/about-rulesets) has been created to apply a minimum set of branch protection rules:

- A PR is required for merges into the default branch (usually `main`)
- At least 1 approver is required before a PR can be merged
- Any conversations on the PR must be marked as resolved

Organisation administrators and repository administrators have been added to the bypass list for this branch protection ruleset.

Repository administrators may add additional rules to their own repositories, but cannot weaken the organisation ruleset: where rules overlap, the most restrictive rule applies. For example, a repository ruleset that drops the required number of approvers to 0 would have no effect, while one that raises it to 3 would apply.

---

### Push Protection

[Push protection](https://docs.github.com/en/code-security/concepts/secret-security/push-protection) is required for all repositories using the DBT GitHub security configuration. It scans every push for known secret formats and rejects it before the secret can enter the repository's history.
DBT also defines [custom secret-scanning patterns](https://docs.github.com/en/code-security/how-tos/secure-your-secrets/customize-leak-detection/define-custom-patterns) to catch DBT-specific secrets that GitHub's built-in patterns would miss.

You should confirm that push protection is enabled on your repository. Please raise a ticket with the SRE team if you need additional patterns.

---

### Pre-Commit Hooks

DBT requires all contributors to use the organisation-approved [pre-commit](https://pre-commit.com/) hooks before committing. A GitHub Actions workflow blocks PRs where the hooks have not run.

Hooks catch secrets and other issues on your machine, before a commit is even created — the earliest and cheapest point to stop a leak, since anything that reaches GitHub must be treated as compromised.

For more information and setup guidance, see the [uktrade/github-standards](https://github.com/uktrade/github-standards) repository.

---

### CODEOWNERS

Repositories must include a [`CODEOWNERS`](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-code-owners) file. GitHub automatically requests a review from the listed owners when a PR touches their code, ensuring changes are seen by people who understand their security implications.

---

### Pull Request Template

PR review is the last human check before code is published, so the template prompts reviewers to look for secrets explicitly rather than relying on automated scanning alone.

If your repository does not already contain a `pull_request_template.md` file, you will inherit the DBT template as a [community health file](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file). If you are already using your own template, you should add this section to remind reviewers they should be ensuring no secret values are visible:

```
### Reviewer Checklist

- [ ] I have reviewed the PR and ensured no secret or sensitive data is present
```

---

### CodeQL for Fork-Based PRs (Optional)

The DBT GitHub security configuration does not currently support scanning PRs raised from a fork of a repository. Fork PRs typically come from contributors outside the organisation, so leaving them unscanned would create a gap in coverage.
If PRs from forks must be supported, switch to [**Advanced** CodeQL](https://docs.github.com/en/code-security/how-tos/find-and-fix-code-vulnerabilities/configure-code-scanning/configuring-advanced-setup-for-code-scanning) to generate a `codeql.yml` workflow:

1. Navigate to **Settings → Advanced Security** in your repository
1. Scroll down to the **Code scanning** section; under the **Tools** sub-section there will be an item for CodeQL analysis
1. Click the **...** button next to the **Default** setup text, then choose **Switch to advanced** from the menu
1. On the popup, click the **Disable CodeQL** button. This only disables the *default* CodeQL setup — a branch protection rule remains in place that blocks PRs unless a CodeQL scan is detected, so PRs still cannot be merged without the advanced workflow you create in the next step
1. GitHub will then open its online editor to create a new file called `codeql.yml`, prefilled with the languages CodeQL has detected in your repository. You can modify the contents of this file if needed, however you must leave the workflow name as `CodeQL Advanced`
1. Once happy with the workflow file contents, click the green **Commit changes** button to trigger a PR to merge this into the default branch
1. Approve and merge the PR with this workflow file. Once merged, CodeQL will perform an initial scan that can take a while; you can track the progress in the **Actions** tab for your repository