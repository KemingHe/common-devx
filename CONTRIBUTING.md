# Contributing

> Updated on 2025-08-08 by @KemingHe

Development workflow guide for contributors using conventional commits, quality gates, issue-driven development, and AI-assisted automation.

## Getting Started

### Initial Setup

```shell
# Clone and setup
git clone <repo-url> && cd <project-name>
[package-manager] install

# Configure environment (if applicable)
cp .env.example .env
# Edit .env with project-specific values
```

### Development

```shell
[package-manager] dev  # Start development server
```

## Development Workflow

### Essential Commands

- `[package-manager] dev` - Development server
- `[package-manager] test` - Run all tests
- `[package-manager] lint` - Code linting
- `[package-manager] format` - Code formatting
- `[package-manager] type-check` - TypeScript validation (if applicable)
- `[package-manager] verify` - Combines format + lint + type-check + test
- `[package-manager] build` - Production build

### Pre-Commit Requirements

**⚠️ Always run before committing**:

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

**AI-assisted approach**: Use [commit message generation prompt](./prompts/prompt-commit-msg-gen.md) for structured, conventional commits with automated repository analysis.

## Issue and PR Workflow

### Creating Issues

- **Manual approach**: Use GitHub [issue templates](./.github/ISSUE_TEMPLATE/) for bug reports and feature requests.
- **AI-assisted approach**: Feed [issue generation prompt](./prompts/prompt-issue-gen.md) to AI assistant for structured, comprehensive issues.

### Creating Pull Requests

1. **Issue linkage**: Every PR must reference an issue
2. **Quality gates**: All checks must pass (`[package-manager] verify`)
3. **Code review**: Minimum one approval required
4. **Testing**: Comprehensive test coverage for changes

- **Manual approach**: Use [pull request template](./.github/pull_request_template.md) to ensure complete information.
- **AI-assisted approach**: Feed [PR generation prompt](./prompts/prompt-pull-request-gen.md) to AI assistant for automated PR descriptions with git analysis.

## Code Quality Standards

### General Guidelines

- Write self-documenting code with clear naming
- Include comprehensive error handling
- Follow project-specific style guides
- Maintain test coverage for all changes

### Testing Requirements

- **Unit tests**: Core logic and utilities
- **Integration tests**: API endpoints and workflows
- **E2E tests**: Critical user paths (if applicable)

**Test naming**: `*.[unit|integration|e2e].test.[js|ts]` or organized in `__tests__/` directories

## Project Structure Patterns

```text
project-root/
├── .github/               # GitHub templates and workflows
├── docs/                  # Documentation
├── src/                   # Source code
├── tests/ or __tests__/   # Test files
├── [config-files]         # Package manager and tool configs
└── README.md              # Project overview
```

## Troubleshooting

### Common issues

- **Dependency errors**: Clear cache and reinstall
- **Test failures**: Check environment setup and dependencies
- **Build errors**: Verify configuration files
- **Lint/format issues**: Run `[package-manager] format` then `[package-manager] lint --fix`

### Getting help

- **Documentation**: Reference project-specific README.md and existing issues
- **Templates**: Use [GitHub templates](./.github/) for consistent issue/PR formatting
- **AI automation**: Leverage [prompts](./prompts/) for automated documentation generation
- **Team workflows**: Reference [meeting templates](./meetings/) for structured communication

---

> Contributing Guide v1.0.0 - KemingHe/common-devx
