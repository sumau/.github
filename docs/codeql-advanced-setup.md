# Setting Up Advanced CodeQL for Fork-Based PRs

These instructions support the [CodeQL for Fork-Based PRs](https://github.com/uktrade/.github/blob/main/SECURITY.md#codeql-for-fork-based-prs-optional) control in the DBT GitHub Security Policy. Switching to [**Advanced** CodeQL](https://docs.github.com/en/code-security/how-tos/find-and-fix-code-vulnerabilities/configure-code-scanning/configuring-advanced-setup-for-code-scanning) generates a `codeql.yml` workflow:

1. Navigate to **Settings → Advanced Security** in your repository
1. Scroll down to the **Code scanning** section; under the **Tools** sub-section there will be an item for CodeQL analysis
1. Click the **...** button next to the **Default** setup text, then choose **Switch to advanced** from the menu
1. On the popup, click the **Disable CodeQL** button. This only disables the *default* CodeQL setup — a branch protection rule remains in place that blocks PRs unless a CodeQL scan is detected, so PRs still cannot be merged without the advanced workflow you create in the next step
1. GitHub will then open its online editor to create a new file called `codeql.yml`, prefilled with the languages CodeQL has detected in your repository. You can modify the contents of this file if needed, however you must leave the workflow name as `CodeQL Advanced`
1. Once happy with the workflow file contents, click the green **Commit changes** button to trigger a PR to merge this into the default branch
1. Approve and merge the PR with this workflow file. Once merged, CodeQL will perform an initial scan that can take a while; you can track the progress in the **Actions** tab for your repository
