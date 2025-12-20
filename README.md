<!-- This file is generated. Do not edit directly. See .docs/README.md for details. -->

# Auto Tag and Release

Automatically create Git tags and GitHub releases for new versions

## Features

- **Idempotent** – Safely checks if the tag and release already exist before creating them, preventing duplicate releases
- **Immutable Releases** – Uses immutable version tags (e.g., `v1.2.3`) rather than mutable tags that can be moved, ensuring your releases are trustworthy and auditable
- **Version Change Detection** – Compares current version against a previous version to skip unnecessary operations when nothing has changed
- **Auto-generated Release Notes** – Automatically generates release notes from your commits using GitHub's built-in release notes feature
- **Dry Run Mode** – Test your release workflow without creating actual tags or releases
- **Job Summaries** – Provides detailed, formatted summaries in the GitHub Actions UI showing exactly what happened
- **Simple Interface** – Just provide a version string and the action handles the rest
- **Lightweight** – A composite action with no external dependencies, runs entirely via GitHub's API

## How It Works

1. **Version Check** – If a `previous-version` is provided, the action compares it against the current `version`. If they match, all subsequent steps are skipped.

2. **Tag Existence Check** – Queries the GitHub API to determine if a tag with the specified version already exists.

3. **Release Existence Check** – Queries the GitHub API to determine if a release for the specified version already exists.

4. **Tag Creation** – If the version changed and the tag doesn't exist (and not in dry-run mode), creates a new Git tag pointing to the current commit.

5. **Release Creation** – If the version changed and the release doesn't exist (and not in dry-run mode), creates a new GitHub release with auto-generated release notes.

6. **Summary Output** – Generates a detailed summary table in the GitHub Actions job summary showing the version, what was created or skipped, and why.

## Usage

```yaml
- uses: freerangebytes/auto-tag-and-release@v0.2.0
  with:
    # If true, skip creating tags and releases (useful for testing)
    dry-run: "false"
    # The previous version for the release
    previous-version: "v1.0.0"
    # If true, output a summary to the job summary
    summary: "true"
    # The version for the release
    version: "v1.0.0"
```

## Inputs

| Name | Description | Required | Default |
| ---- | ----------- | -------- | ------- |
| `dry-run` | If true, skip creating tags and releases (useful for testing) | `false` | `false` |
| `previous-version` | The previous version for the release | `false` | - |
| `summary` | If true, output a summary to the job summary | `false` | `true` |
| `version` | The version for the release | `true` | - |

## Outputs

| Name | Description |
| ---- | ----------- |
| `previous-version` | The previous version for the release |
| `released` | Whether a new release was created |
| `version` | The version for the release |

## Contributing

### Development Environment

This project includes a [devcontainer](https://containers.dev/) configuration for a consistent development experience. You can use it with:

- [GitHub Codespaces](https://github.com/features/codespaces)
- [VS Code Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers)
- Any IDE that supports the devcontainer specification

The devcontainer comes pre-configured with all required tools and recommended VS Code extensions.

### Commit Messages

This project uses [commitlint](https://commitlint.js.org/) with the [Conventional Commits](https://www.conventionalcommits.org/) specification. All commit messages must follow the format:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

Common types include: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`.

For more information, see the [commitlint documentation](https://github.com/conventional-changelog/commitlint/#what-is-commitlint).

## License

MIT
