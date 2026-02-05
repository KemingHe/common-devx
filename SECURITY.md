# Security Policy

> **Last Updated**: 2026-02-05 by Keming He

Security considerations for using and contributing to common-devx.

## Scope

This repository contains documentation templates and AI agent skills - not executable code with traditional security vulnerabilities. This policy covers:

- Content accuracy and safety
- Responsible use of AI-generated content
- Reporting issues with skills or templates

## Content Verification

> [!IMPORTANT]
>
> Always review AI-generated content before use.

When using skills from this repository:

1. **Read the skill** - Understand what the AI will do before invoking it
2. **Review output** - Verify AI-generated content is accurate and appropriate
3. **Check for sensitive data** - Ensure no credentials, secrets, or PII are exposed
4. **Validate links and paths** - Confirm references point to correct locations

## Reporting Issues

### Content Problems

For inaccurate, misleading, or problematic content:

- Open a [GitHub issue](https://github.com/KemingHe/common-devx/issues) with details
- Use the bug report template for specific problems
- Include the file path and description of the issue

### Security Concerns

For issues that could cause harm if publicly disclosed:

1. **Do not open a public issue**
2. Use GitHub's [private vulnerability reporting](https://docs.github.com/en/code-security/how-tos/report-and-fix-vulnerabilities/report-a-vulnerability/privately-reporting-a-security-vulnerability)
3. Or email the maintainer directly (see repository profile)

Response time: Best effort, typically within 7 days.

## Best Practices for Contributors

When adding or modifying content:

- [ ] No hardcoded credentials, API keys, or secrets in examples
- [ ] No real personal information in templates (use placeholders)
- [ ] No instructions that could enable harmful actions
- [ ] Clear warnings where caution is needed

## Supported Versions

This repository follows a rolling release model. The `main` branch always contains the current supported version.

## Coordinated Disclosure

If you discover a security issue:

1. Report privately (see above)
2. Allow reasonable time for response and fix
3. Do not disclose publicly until addressed

---

> Security Policy v1.0.0 - KemingHe/common-devx
