# README - Common DevX

Ready-to-use [AI skills](#available-skills) and [human guides](#human-guides) for consistent documentation, standardized `git` workflows, and streamlined project management. [MIT licensed](./LICENSE), zero dependencies.

> [!TIP]
>
> For background, see the [official agent skills documentation](https://agentskills.io/what-are-skills).

## Repository Structure

```plaintext
common-devx/
├── .agents/skills/        # AI skills (see catalog below)
├── .github/               # GitHub issue and PR templates
├── .gitlab/               # GitLab issue and MR templates
├── human-guides/          # Developer guides
├── CONTRIBUTING.md        # How to contribute
├── LICENSE                # MIT license
├── README.md              # This file
└── SECURITY.md            # Security guidance
```

## Available Skills

| Skill | Category | Description |
| :--- | :--- | :--- |
| [Commit Message Creation](./.agents/skills/commit-message-creation/README.md) | ⚙️ Git Workflow | Generate conventional commit messages following project standards |
| [GitLab Sync](./.agents/skills/dot-gitlab-sync/README.md) | ⚙️ Git Workflow | Sync .github/ and .gitlab/ template directories with platform-specific transformations |
| [Issue Creation](./.agents/skills/issue-creation/README.md) | ⚙️ Git Workflow | Generate issues following repository templates for GitHub or GitLab |
| [Pull/Merge Request Creation](./.agents/skills/pull-merge-request-creation/README.md) | ⚙️ Git Workflow | Generate PR (GitHub) or MR (GitLab) descriptions following repository templates |
| [Contacts Management](./.agents/skills/contacts-management/README.md) | 📁 Project Management | Manage contact information by adding, updating, or validating entries |
| [Documentation Review](./.agents/skills/documentation-review/README.md) | 📁 Project Management | Review and correct documentation for consistency, correctness, and drift |
| [Living Design Documents](./.agents/skills/living-design-documents/README.md) | 📁 Project Management | Create and maintain structured design documentation that drives development |
| [Meeting Agenda Creation](./.agents/skills/meeting-agenda-creation/README.md) | 📁 Project Management | Generate meeting agendas with topics, timing, and preparation requirements |
| [Meeting Memo Creation](./.agents/skills/meeting-memo-creation/README.md) | 📁 Project Management | Generate meeting memos capturing decisions, actions, and key discussions |
| [README Creation](./.agents/skills/readme-creation/README.md) | 📁 Project Management | Generate self-contained README files that enable instant developer onboarding |
| [Next Session Handoff](./.agents/skills/next-session-handoff/README.md) | 🧠 Meta | Generate structured handoff documents for context transfer across AI session boundaries |
| [Senior Mentor](./.agents/skills/senior-mentor/README.md) | 🧠 Meta | Transform into a senior mentor for guided learning through Socratic questioning |
| [Skill Creation](./.agents/skills/skill-creation/README.md) | 🧠 Meta | Create or refactor Agent Skills following the agentskills.io specification |

> **Note**: Emojis in this table are a deliberate exception to the project's no-emoji convention, used here to aid visual scanning of skill categories.

## How to Use

### Install via npx (Recommended)

The [skills CLI](https://github.com/vercel-labs/skills) installs to a canonical location and auto-symlinks to detected agents. The interactive installer prompts you to select which skills and agents to install.

| Scope | Flag | Location | Use Case |
| :--- | :--- | :--- | :--- |
| Project | (default) | `.agents/skills/` | Shared with team, version-controlled |
| Global | `-g` | `~/.agents/skills/` | Install once, use across all projects |

```shell
# Project: committed with your repo (recommended for teams)
npx skills add KemingHe/common-devx

# Global: available in all projects
npx skills add KemingHe/common-devx -g
```

> [!IMPORTANT]
>
> - **Review skills before use** - they run with full agent permissions!
>
> - During installation, the CLI displays Security Risk Assessments from [Gen Agent Trust Hub](https://ai.gendigital.com/ath), [Socket](https://socket.dev/), and [Snyk](https://snyk.io/).
>
> - To remove skills, see [`skills remove` documentation](https://github.com/vercel-labs/skills#skills-remove).

### Alternative 1 - Manual Copy

For customization, copy any skill directly (MIT licensed):

```shell
git clone https://github.com/KemingHe/common-devx.git

mkdir -p .agents/skills
cp -r common-devx/.agents/skills/commit-message-creation .agents/skills/
```

### Alternative 2 - GitHub Template

Create a new repository with all skills and guides included. Click **Use this template** (green button, top right) or use [this direct link](https://github.com/new?template_name=common-devx&template_owner=KemingHe).

## Human Guides

Developer reference docs for common workflows and troubleshooting. See [`human-guides/README.md`](./human-guides/README.md) for naming conventions and how to add new guides.

### Diagnosis

- [Terraform State Migration](./human-guides/diagnosis-terraform-state-migration.md) - investigation procedures for state migration issues

### Use Cases

- [Git](./human-guides/use-cases-git.md) - command-line workflows
- [Git-crypt](./human-guides/use-cases-git-crypt.md) - transparent file encryption
- [GPG Commit Signing](./human-guides/use-cases-gpg-commit-signing.md) - signing commits with GPG
- [Shell](./human-guides/use-cases-shell.md) - shell operations
- [SSH Authentication](./human-guides/use-cases-ssh-authentication.md) - Git and server authentication

## References

- [`CONTRIBUTING.md`](./CONTRIBUTING.md) - How to contribute
- [`SECURITY.md`](./SECURITY.md) - Security guidance
- [GitHub Issues](https://github.com/KemingHe/common-devx/issues) - Questions and requests
