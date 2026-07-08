# uktrade/.github

This is the [`.github` repository](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file) for the [`uktrade`](https://github.com/uktrade) organisation. It holds organisation-wide defaults that GitHub applies automatically to any `uktrade` repository that does not define its own.

## What's here

| Path | Purpose |
|---|---|
| [`SECURITY.md`](SECURITY.md) | DBT GitHub Security Policy — inherited by every repository without its own `SECURITY.md` |
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | Default pull request template |
| [`templates/SECURITY_CHECKLIST.md`](templates/SECURITY_CHECKLIST.md) | Security checklist to copy into a repository root |
| [`workflow-templates/`](workflow-templates/) | Organisation [workflow templates](https://docs.github.com/en/actions/using-workflows/creating-starter-workflows-for-your-organization) offered when creating a new Action |
| [`docs/`](docs/) | Step-by-step setup guides referenced from the security policy |

## Contributing

Changes here affect every `uktrade` repository, so raise a PR against this repo rather than copying files elsewhere.

This repo requires the organisation-approved pre-commit hooks. See the [github-standards instructions](https://github.com/uktrade/github-standards/blob/main/README.md#usage) to install them.

The code security diagram (`assets/code_sec_workflow.excalidraw.svg`) is an SVG with the [Excalidraw](https://excalidraw.com/) scene embedded inside it, so it renders as a plain image in `SECURITY.md` while staying editable. Edit it with the [Excalidraw VS Code extension](https://marketplace.visualstudio.com/items?itemName=pomdtr.excalidraw-editor), which reads and writes the embedded scene directly.
