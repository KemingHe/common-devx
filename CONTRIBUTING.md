# Contributing

> **Last Updated**: 2025-08-08 by Keming He

Development workflow for contributors using conventional commits, quality gates, issue-driven development, and AI-assisted automation.

## Getting Started

### Initial Setup

```shell
# Clone and setup
git clone <repo-url> && cd <project-name>
[package-manager] install

# Configure environment (if applicable)
cp .env.example .env
```

> [!IMPORTANT]
>
> Follow project-specific environment setup documentation to configure required variables and dependencies.

## Project Structure

```text
project-root/
├── .github/                     # GitHub templates and workflows
├── docs/                        # Documentation
├── prompts/                     # AI-assisted development prompts
├── src/                         # Source code
├── tests/ or __tests__/         # Test files
├── [config-files]               # Package manager and tool configs
└── README.md                    # Project overview
```

## Development Workflow

### Essential Commands

- `[package-manager] verify` - Combines format + lint + type-check + test
- `[package-manager] build` - Production build

> [!TIP]
>
> See `package.json` or project documentation for comprehensive list of commands.

### Pre-Commit Requirements

```shell
[package-manager] verify  # Comprehensive quality checks
```

## Git Conventions

**Types**: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `perf`, `ci`, `build`

### Branch Naming

Format: `<type>/<scope>/<assignee>`

```text
feat/auth/username
fix/api-validation/username
docs/readme-update/username
```

### Commit Messages

Format: `<type>(<scope>): <description>`

```text
feat(auth): add JWT token validation
fix(api): resolve CORS configuration
docs(readme): update installation instructions
```

> [!TIP]
>
> **AI-assisted approach**: Use [commit message generation prompt](./prompts/prompt-commit-msg-gen.md) for structured, conventional commits with automated repository analysis.

## Issue and PR Workflow

### Creating Issues

- **Manual approach**: Use GitHub [issue templates](./.github/ISSUE_TEMPLATE/) for bug reports and feature requests.
- **AI-assisted approach**: Use [issue generation prompt](./prompts/prompt-issue-gen.md) with AI assistant for structured, comprehensive issues.

### Creating Pull Requests

1. **Issue linkage**: Every PR must reference an issue
2. **Quality gates**: All checks must pass (`[package-manager] verify`)
3. **Code review**: Minimum one approval required
4. **Testing**: Comprehensive test coverage for changes

- **Manual approach**: Use [pull request template](./.github/pull_request_template.md) to ensure complete information.
- **AI-assisted approach**: Use [PR generation prompt](./prompts/prompt-pull-request-gen.md) with AI assistant for automated PR descriptions with git analysis.

## Code Quality Standards

### General Guidelines

- Write self-documenting code with clear naming
- Include comprehensive error handling
- Follow project-specific style guides and best practices
- Maintain test coverage for all changes

### Testing Requirements

- **Unit tests**: Core logic and utilities (`*.unit.test.[js|ts]`)
- **Integration tests**: API endpoints and workflows (`*.integration.test.[js|ts]`)
- **E2E tests**: Critical user paths (`*.e2e.test.[js|ts]`)

**Test structure**: Tests co-located with source files or organized in `__tests__/` directories

## Troubleshooting

### Common Issues

- **Lint/format issues**: Run `[package-manager] format` then `[package-manager] lint --fix`
- **Test failures**: Check environment setup and dependencies
- **Build errors**: Verify configuration files and dependencies
- **Dependency conflicts**: Clear cache and reinstall packages

### Getting Help

- **Environment setup**: Reference project-specific documentation and README.md
- **Issue and PR templates**: Use [GitHub templates](./.github/) for consistent formatting
- **AI automation**: Leverage [prompts](./prompts/) for automated documentation generation
- **Team workflows**: Reference [meeting templates](./meetings/) for structured communication

---

> Contributing Guide Template v1.0.1 - KemingHe/common-devx
